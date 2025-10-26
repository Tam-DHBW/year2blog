# Conventions

## API Error response
The API returns an error response if the response has a `4XX` or `5XX` status code.

This response adheres to the following schema:
```ts
{
    type: string?, // Fixed value indicating the type of error which occurred
    message: string // Detailed and possibly varying error message
}
```

While the `type` field is present on all errors returned by the API,
it is not included in errors originating from AWS.

**The `type` field is to be used for determining the kind of error that occurred.**
**The `message` field is for debugging purposes or displaying the error to a user.**

### Backend error response implementation
All fallible handler functions must return `crate::response::ApiResult<T>`,
which has a `Box<dyn ApiError>` error type.

This error trait is to be implemented using the `error_response!(...)` macro under normal circumstances.
Usage of this macro is as follows:
```rust
error_response!(ChatError {                     // Enum name

                                                // Error `message` field with
    /// Thing with ID {thing_id} was not found  // formatting support
    ThingNotFound {                             // Error `type` field
        thing_id: u32                           // Error debug and format data
    },
    
    /// The {xyz} went wront
    ThatWentWrong(String as xyz, u32)           // Tuple variant formatting names

    AnotherError,                               // `message` defaults to `type`

                                                // Specify `http::StatusCode`. 
    SomeInvalidInput[BAD_REQUEST],              // Defaults to `INTERNAL_SERVER_ERROR`
    
});
```

`5XX` errors are automatically logged, using error type, error message and the error's `Debug` representation.
