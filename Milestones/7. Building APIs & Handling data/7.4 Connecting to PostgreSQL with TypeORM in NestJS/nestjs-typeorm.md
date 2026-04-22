## Reflection

### How does @nestjs/typeorm simplify database interactions?

- It makes it easier to connect NestJS to the database by giving built-in module helpers and repository injection. Instead of manually opening database connections in different places, NestJS can provide the repository directly to the service.

### What is the difference between an entity and a repository in TypeORM?

- An entity is the class that describes the database table, while a repository is the object used to work with that table’s data. In this task, Task was the entity with fields like id, title, and completed, while the repository was used in tasks.service to find, save, update, and delete tasks.

### How does TypeORM handle migrations in a NestJS project?

- By generating and running database change files when the table structure changes. This is useful in real projects because it updates the database safely without relying only on automatic sync. In this task, synchronize: true was fine for learning, but in a bigger project migrations would be the safer way to track schema changes over time.

### What are the advantages of using PostgreSQL over other databases in a NestJS app?

- It is reliable, works well with relational data, and has good support in TypeORM through the pg driver. It is useful when your app has structured data and relationships between tables. In this task, PostgreSQL was a better long-term option than storing tasks in a simple array because the data can stay saved outside the app.

## Task 

- installed the TypeORM packages so the NestJS app could connect to PostgreSQL and work with database tables using TypeScript instead of only using a temporary array in the service. 

![typeorm](image.png)

- created task.entity to define the Task table structure, including the id, title, and completed fields that would be stored in PostgreSQL

![taskEntity](image-1.png)

- updated tasks.module, tasks.service, and app.module to use task.entity, set up the PostgreSQL connection, and inject the task repository so the tasks feature could read and write task data directly in the database

![updateAppModule](image-2.png)

- started the server and tested the basic CRUD operations to confirm that tasks could be created, read, updated, and deleted through PostgreSQL instead of only being stored temporarily in code. The output showed that GET returned the existing tasks, POST added a new task, PUT updated the selected task, and DELETE removed the selected task successfully 

![CRUDCheck](image-3.png)