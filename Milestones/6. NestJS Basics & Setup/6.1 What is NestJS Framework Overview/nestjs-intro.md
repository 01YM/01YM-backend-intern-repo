## 6.1 Reflection 

### What are the key differences between NestJS and Express.js? 
- Both are backend frameworks for Node.js. Express is simplae and give devs a lot of freedom for creating routes, middleware, server logic. Its easier to use for smaller projects but can become very messy scaled. Nest is more structured, it forces devs split the project into modules, controllers, services. It has built in features like dependancy injection and decorators. Its just more organised and easier to manage when a lot of people work together. 

### Why does NestJS use decorators extensively?
- It makes the code really easy to read and understand. For example when you see @Controller() you know that this class is responsible for handling requests from users. Or @Injectable() tells that a class can be used as a service and injected into other classes. 

### How does NestJS handle dependency injection? 
- Automatically. instead of creating the service every class, Nest injects it where ever you need it automatically and passes it through the constuctor. So for example if you need to setup an inventory, you can create an InventoryService once and then inject it into any controller or other service that needs inventory logic. 

### What benefits does modular architecture provide in a large-scale app?
- Its easier to manage. Each feature has its own module, controller and service. All the related files stay together, teamwork becomes easier. Devs can be working on different modules without getting into eachothers way. Its also easeir to update and fix since everything is split into relevant sections.  
