#### error handling

```
Option
Try
Validate
Either
IO

```

#### domain error

- can be expressed in the language of the domain
- related to business logic
- shold be communicated in a friendly way to the user

```
- From/to account number can have invalid format
- amount may not be a number
- a required field may be missing
- from/to account may not exist
- amout to transfer can be more than what is available
- from/to account may be freezed
```

#### techical error

- can be expressed using technical terms
- related to implementation detail
- should be communicated to the programmers with as much detail as possible

```
- connection to the Db can fail
- dist of db server may be full
- server can run out of memory
```
