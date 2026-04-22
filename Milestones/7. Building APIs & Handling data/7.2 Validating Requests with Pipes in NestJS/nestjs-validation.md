## Reflection

### What is the purpose of pipes in NestJS?

- to check or change data before it reaches the controller method. They help make sure the data is valid and in the correct format. In the task below, ParseIntPipe was used in tasks.controller.ts to make sure the task ID in routes like /tasks/1 is treated as a number

### How does ValidationPipe improve API security and data integrity?

- ValidationPipe improves security by rejecting bad or unexpected data before it reaches the service. This helps keep the app data clean and prevents users from sending the wrong types of values. In this task, the DTO only allowed title as a string and completed as a boolean, so invalid requests were rejected automatically

### What is the difference between built-in and custom pipes?

- Built-in pipes already exist in NestJS and are ready to use, while custom pipes are created by the developer for special rules. In my example, ParseIntPipe and ValidationPipe were built-in pipes because NestJS already provides them

### How do decorators like @IsString() and @IsNumber() work with DTOs?

- they tell NestJS what type of value each field should contain. ValidationPipe reads those decorators and checks the request body against them. In the task below, @IsString() was used for the task title and @IsBoolean() was used for the completed field

## Task 

- installed class-validator and class-transformer packages to validate incoming request data using DTOs and validation decorators

![installing packages](image.png)

- added create-task.dto.ts file to define what data a task should contain, including a title as a string and completed as a boolean

![dtoFile](image-1.png)

- updated tasks.controller.ts so the POST and PUT routes use CreateTaskDto, and added ParseIntPipe to make sure task IDs are valid numbers 

![updateController](image-2.png)

- updated main.ts to use a global ValidationPipe so all DTO validation rules are automatically checked across the app

![validationPipe](image-3.png)

- tested both valid and invalid requests to confirm that correct task data was accepted and incorrect data was rejected by the DTO validation 

![testing](image-4.png)