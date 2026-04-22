## Reflection

### What is the difference between an interceptor and middleware in NestJS?

- Middleware runs before the controller and is usually used for checking or logging the request. An interceptor runs before and after the controller, so it can log both the request and the response. In this task, the middleware logged when /tasks was opened, while the interceptor also logged the returned task data.

### When would you use an interceptor instead of middleware?

- when you need to work with the controller result, response transformation, timing, or error handling. In this task, the interceptor was the better choice for logging response data because it runs around the controller method and can see what the route returns. Middleware cannot do that in the same way

### How does LoggerErrorInterceptor help?

- by catching errors in the request/response flow and logging them in one central place. This makes debugging easier and avoids repeating error logging inside each controller method. In a project like this one, it would be useful if a tasks route failed and you wanted a clear log of the error without changing every route handler.


## Task 

- created logging.interceptor.ts to log information before and after a request is handled. The interceptor logged the request method and route before the controller ran, then logged the response data and response time after the controller finished 

![interceptorts](image.png)

- created logger.middleware.ts to log each request before it reached the controller. The middleware logged the request method and route, then used next() so the request could continue 

![middleware](image-1.png)

- updated app.module.ts to apply LoggerMiddleware to the tasks routes so every request to /tasks would go through the middleware first

![applyMiddleware](image-2.png)

- started the NestJS server with npm run start:dev, sent a GET request to /tasks, and checked the terminal logs to confirm that the middleware ran first and the interceptor logged both the request and response.

![sendingGET](image-3.png)

