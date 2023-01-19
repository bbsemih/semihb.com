---
title: Testing Asynchronous Code Using Vitest
date: 2023-01-19 20:25:00 +0800
categories: [test, javascript, vitest]
tags: [test, software, javascript, vitest]
---

In this blog post, I'll be explaining how we can implement unit tests for async JavaScript code using [Vitest](https://github.com/vitest-dev/vitest). In the example code, we will generate JSON Web Token to understand the logic behind the async testing easier. Note that since there are no major differences between Jest and Vitest, you can also use Jest to perform the same action.


## Functions To Generate JWT

```javascript
import jwt from 'jsonwebtoken';

export function generateToken(userEmail, doneFn) {
    jwt.sign({ email: userEmail }, 'secret123', doneFn);
}

export function generateTokenPromise(userEmail) {
    const promise = new Promise((resolve, reject) => {
        jwt.sign({ email: userEmail }, 'secret123', (error, token) => {
            if (error) {
                reject(error);
            } else {
                resolve(token);
            }
        });
    });

    return promise;
};
```


## Wrong Approach

We expect JWT to be defined and the first test actually passes but does it really work? 

As a matter of fact, no. Because it is not waiting for the `generateToken` function to complete before the test finishes. The `generateToken` function is async, therefore the test finishes before the generateToken function has had a chance to complete and call the callback function, which means that the `expect(token).toBeDefined()` assertion is never reached.

In the second test, we're trying to generate a JWT and this time expecting it to be 2. The test once again passes, doesn't give any error although it is pretty much impossible jsonwebtoken to generate a token which is 2.

```javascript
import { it, expect } from "vitest";
import { generateToken } from "./async-example";


it("test 1", () => {
    const userEmail = "random@random.com";

    generateToken(userEmail, (err, token) => {
        expect(token).toBeDefined();
    })
});


it("test 2", () => {
    const userEmail = "random@random.com";

    generateToken(userEmail, (err, token) => {
        expect(token).toBe(2);
    })
});
```

## How To Fix It?

In order to fix these problems, this time instead of putting the test in a function with an empty argument, we're gonna use a single argument called `done`. So in that way Vitest will wait for the `done` function to be called before considering the test complete and will execute the assertion inside the callback, giving it the chance to run.

```javascript
it("test 1", (done) => {
    const userEmail = "random@random.com";

    generateToken(userEmail, (err, token) => {
        expect(token).toBeDefined();
        done();
    })
});

//This time this doesn't pass as we expected.
//And doesn't timeout thanks to the try-catch block. 
it("test 2", (done) => {
    const userEmail = "random@random.com";

    generateToken(userEmail, (err, token) => {
        try {
            expect(token).toBe(2);
            done();
        }
        catch (err) {
            done(err);
        }
    })
})
```

# Promises and Async/Await

Alternatively, we can also use `async` and `await` or  adding `resolves` after `expect(token)` to wait for the promise to resolve and then perform the assertion without putting `done` as an argument.

```javascript
it("test 1 async/await", async () => {
    const userEmail = "random@random.com";
    const token = await generateTokenPromise(userEmail);
    expect(token).toBeDefined();
});

it("test 1 .resolves()", async () => {
    const userEmail = "random@random.com";
    return expect(generateTokenPromise(userEmail)).resolves.toBeDefined();
})
```



Sources:
* vitest.dev
* Academind