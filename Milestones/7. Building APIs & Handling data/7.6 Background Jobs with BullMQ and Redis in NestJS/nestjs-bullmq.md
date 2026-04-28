
## Reflection 

### Why is BullMQ used instead of handling tasks directly in API requests?

- Some tasks can take time to finish. If the API handles everything directly, the user has to wait longer for the response. With BullMQ, the API can quickly add a job to a queue and return a response immediately while the real work happens in the background.
### How does Redis help manage job queues in BullMQ?

- Redis stores the queue data for BullMQ. It keeps track of jobs that are waiting, active, completed, or failed. In this task, Redis stored the messages queue and held the send message job until the processor picked it up and completed it.

### What happens if a job fails? How can failed jobs be retried?

- BullMQ marks it as failed and stores the failure information in Redis. Jobs can be retried automatically by setting the attempts option. In the example task below, the queue was configured with attempts: 3, which means BullMQ will try the job up to three times before marking it as permanently failed.

### How does Focus Bear use BullMQ for background tasks?

- BullMQ would be useful for background jobs related to timed and scheduled actions. For example, it can help run focus session timers, send reminders to start a habit, trigger break notifications, update progress after a session ends, and handle recurring routine tasks without making the main app wait. This is useful because the app needs many actions to happen at the right time in the background while the user is focusing on their tasks

## Task
- github link: https://github.com/01YM/nestjs-inventory-game
- installed bullmq and @nestjs/bullmq in the NestJS project so the app can create queues and process background jobs

![installingbullmq](image.png)

- started a Redis container with Docker using docker run -d --name redis-bullmq -p 6379:6379 redis to store and manage the BullMQ queue data

![redischeck](image-1.png)

- sent a POST request to the /messages endpoint to add a new job into the BullMQ queue 

 ![alt text](image-2.png)

- ran npm run start:dev and confirmed that the NestJS app processed the queued job in the background by showing Message job added to queue in the terminal

 ![alt text](image-3.png)