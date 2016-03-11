## Problem

Your route needs to handle an error, stopping execution and returning an HTTP error code and message.

## Solution

Create a new NetworkError object from [errors](https://github.com/codecombat/codecombat/blob/master/server/commons/errors.coffee) (bottom of file). If you are in middleware or a synchronous function, throw it. If you are in an asynchronous function, call the callback with it.

## Details

Joyent has a [long document on proper error handling in Node](https://www.joyent.com/developers/node/design/errors), which is worth a read. In particular: functions should either handle errors synchronously or asynchronously. Be aware that functions you call may throw an exception, and are not called in a co-express wrapped function, need to be handled manually (co-express catches errors and passes them to express' next function to be handled by error middleware).

Invalid input errors, such as not providing a property or parameter that is required, are returned with status code 422, Unprocessable Entity.