Filtering Requests
==================

- Create `AuthenticationFilter`
	- Autowire `UserRepository` and `AuthenticationController`
	- Create whitelist
	- Override `preHandle` method
		- check for whitelisted URL
		- check for user in session
- Create `WebApplicationConfig`
	- `AuthenticationFilter` bean
	- `addInterceptors` call
