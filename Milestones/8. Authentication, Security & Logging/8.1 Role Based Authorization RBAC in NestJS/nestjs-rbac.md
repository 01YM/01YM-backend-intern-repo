- Installed the packages needed for JWT token checking, Passport integration, and Auth0-style authorization after creating the new NestJS project

![installing packages ](image.png)

- Created the custom Roles decorator code. This decorator is used to mark routes with required roles such as admin, so the application knows which type of user is allowed to access a specific endpoint

![rolesDecorator](image-1.png)

- Created the roles.guard.ts file and added the role check logic. The guard reads the required role from the decorator and compares it with the roles stored on the current user. If the user does not have the correct role, access is denied

![guardCheckLogic](image-2.png)

- Created the mock-user.middleware.ts file to simulate a logged-in Auth0 user. This middleware adds a fake user object with an admin role so the RBAC logic can be tested without needing a real Auth0 login.

![mockUserMiddleware](image-3.png)

- Updated the tasks.controller.ts file to protect the admin route. The controller uses both the JWT guard and the roles guard, and only users with the admin role are allowed to access the /tasks/admin endpoint

![tasksController](image-4.png)

- Ran the NestJS application using npm run start:dev to start the local development server

![runningApp](image-5.png)

- Tested the protected admin endpoint successfully using a Bearer token. Because the mock user had the admin role, the request was allowed and returned the protected admin-only response

![successfulRequest](image-6.png)

- Changed the mock user role from admin to user and tested the protected endpoint again. This time the request was blocked and returned a forbidden error because the user no longer had the required role

![forbiddenError](image-7.png)

