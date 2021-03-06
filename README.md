# spring-boot-pre-authorize-issue-01

https://github.com/spring-projects/spring-security/issues/4020

https://gitter.im/spring-projects/spring-security?at=57a9d71346610f17394b8ed5

In `Application.java`

Uncomment the block below for have `@PreAuthorize` annotations defined in `TestRecordRepository`
**NOT be evaluated** (unexpected)

Comment out the block, and `@PreAuthorize` annotations in `TestRecordRepository` will work as expected

See: `MyPermissionEvaluator.java` which will be executed as evidence of the
`@PreAuthorize` annotations working or not (prints to STDOUT)

```
@Autowired
private TestRecordRepository testRecordRepository;
```


```
./gradlew bootRun
```

To invoke, hit `http://localhost:8080/testrecords/search/findByFirstname?fn=1`

If the `@PreAuthorize` annotations are being evaluated you will see entries like the following
on the console stdout on each request:

```
hasPermission() org.springframework.security.authentication.AnonymousAuthenticationToken@9055c2bc: Principal: anonymousUser; Credentials: [PROTECTED]; Authenticated: true; Details: org.springframework.security.web.authentication.WebAuthenticationDetails@b364: RemoteIpAddress: 0:0:0:0:0:0:0:1; SessionId: null; Granted Authorities: ROLE_ANONYMOUS target: 1 perm:READ
```
