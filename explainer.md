# Response.json() Explained


## Introduction

The [Response
constructor](https://developer.mozilla.org/en-US/docs/Web/API/Response/Response)
is extremely flexible and can accept several different types for the “body”
argument. One notable omission is that it cannot accept an arbitrary object and
convert it to JSON. This would be ambiguous with the other types it accepts.

`Response.json()` is the solution to this functionality gap. It is a static
method that works very much like the Response constructor, but it converts the
first argument to JSON and sets the content type to “`application/json`”.

```javascript
const response = Response.json(object);
```

is roughly equivalent to

```javascript
const response = new Response(JSON.stringify(object),
                              {
                                headers: {
                                  "Content-Type": "application/json"
                                }
                              });
```

but significantly easier to use.

This is symmetric with the `Response.prototype.json()` method which converts
back the other way.

`Response.json()` takes an optional `ResponseInit` option object as the second
parameter, which is used in the same way as the second parameter to the Response
constructor.


## Goals

* Make working with JSON Responses easier and more ergonomic.


## Non-goals

* Adding static methods for other types than JSON. They can simply be passed to
  the Response constructor.


## Use cases

* Many web applications use JSON to exchange methods.
* This is particularly useful for synthesising JSON responses in service
  workers.


## End-user benefits

Web pages will, on average, be less buggy due to developers not having to
re-implement this functionality.


## Alternatives

As noted above, it is fully possible to implement this using `JSON.stringify()`,
but it is less elegant.


## Future work

None needed.
