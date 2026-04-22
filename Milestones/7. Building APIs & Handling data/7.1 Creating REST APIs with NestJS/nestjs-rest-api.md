## Reflection

### What is the role of a controller in NestJS?

- it receives requests from the user or client. It decides which function should run when someone sends a GET, POST, PUT, or DELETE request. 

### How should business logic be separated from the controller?

- Business logic should go into a service, not inside the controller. The controller should stay small and mostly handle the request and response. The service should do the real work, like creating data, updating it, checking rules, or talking to the database. This makes the code easier to read and manage.

### Why is it important to use services instead of handling logic inside controllers?

- Using services keeps the project neat. If everything is inside the controller, the file becomes too big and confusing. Services also make it easier to test your code because you can test the logic by itself. It also helps when you want to reuse the same logic in more than one place.

### How does NestJS automatically map request methods (GET, POST, etc.) to handlers?

- INestJS uses decorators. For example, @Get() means this function should run for a GET request, and @Post() means it should run for a POST request. Nest reads these decorators and builds the routes for you automatically. So if your controller says @Controller('tasks') and a method says @Get(), Nest makes that route work as GET /tasks.

## Task 

- created a new tasks folder with a controller, module, and service file so the project had a separate feature for managing tasks, similar to the existing player and inventory folders. The controller handled routes like getting, creating, updating, and deleting tasks.

![TasksController](image.png)

- added task logic inside tasks.service.ts, including functions to get all tasks, get one task by ID, create a new task, update an existing task, and delete a task from the array.

![TaskService](image-1.png)

- ran the NestJS server using npm run start:dev so the app would start in development mode and automatically refresh after file changes.

![Start NestJS](image-2.png)

- tested the task endpoints in PowerShell by sending GET, POST, PUT, and DELETE requests to make sure the new task routes were working correctly.

![Testing Endpoints](image-4.png)