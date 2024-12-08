# Uberspec

## Protobuf conventions

### Header section

1. Package should consists of:
- service goal (ex.: `api`) (lowercase)
- service name (ex.: `users`, `comments`) (plural, snakecase, lowercase)
- service version major.minor.patch (ex.: `v1_3_2`) (snakecase, lowercase)
Ex.: `api.users.v1.3.2`

2. Options:
- `java_outer_classname = "ServicenameProto"` (ex.: `UsersProto`) (plural, camelcase, uppercase first)
- `java_multiple_files = true`
- `java_generic_services = true`

### Imports section

All imports should be here

### RPC section

1. Service name should consist of ServicenameService (ex.: `UsersService`, `CommentsService`) (plural, camelcase, upcase first)
2. RPC should start from a verb - get, add, update, delete, custom verb (ex.: `getComments`, `addUser`, `updateUser`, `closeDeal`) (camelcase, lowercase first)
3. 

3.1. Request message should contain a word `Request` in the end (ex.: `GetUserByIdRequest`)

3.2. Response message should contain a word `Response` (ex.: `GetUserByIdResponse`)

3.3. Exclusion is a message that was defined as an entity (ex.: `rpc addUser(User) returns (Empty);`)

4. Successful empty request/response should contain `Empty` message
5. Message with a single message as a parameter should be avoided
Ex.:
```
rpc getDeal(GetDealRequest) returns (GetDealResponse);

message GetDealRequest {
  Empty empty = 1;
}

message GetDealResponse {
    Deal deal = 1;
}
```

should be replaced with

```
rpc getDeal(Empty) returns (Deal);
```

### Messages section

1. Message name should have only message topic (ex.: `User` instead of `UserMessage`) (camelcase, upcase first)
2. Repeated paramet should always be in a plural form (ex.: `repeated User users = 1`)
3. Parameter should be in a snake case (ex.: `UserType user_type = 1`)

### Authentication / Authorization

1. JWT authentication token should be passed in a header `x-client-authorization`. Only external authorization server should access this header. Header should be removed in a front proxy.
2. Authorized user ID should be propagated in the header `x-ext-auth-id-user` from external authorization server.

By [Dmytro Nasyrov, Founder, CTO at Pharos Production Inc.](https://www.linkedin.com/in/dmytronasyrov/)
And [Pharos Production Inc. - Web3, blockchain, fintech, defi software development services](https://pharosproduction.com)
