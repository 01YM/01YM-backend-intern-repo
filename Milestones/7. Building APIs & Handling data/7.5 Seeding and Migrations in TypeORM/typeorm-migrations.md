## Reflection

### What is the purpose of database migrations in TypeORM?

- to keep the database structure updated in an organized way. Instead of changing tables by hand, you save each schema change in a migration file. Every dev and every environment can apply the same changes in the same order. For example, if I add a new description column to a Task table, the migration makes sure PostgreSQL gets that same new column correctly.

### How do migrations differ from seeding?

- Migrations change the structure of the database, while seeding adds example or starter data into the tables. A migration might create a tasks table or add a new column, but seeding would insert rows like “Learn migrations” or “Finish project”. In simple terms, migrations build or change the container, and seeding puts things inside the container.

### Why is it important to version-control database schema changes?

- If schema changes are saved in version control, the whole team can track what changed, when it changed, and who changed it. This also makes deployment safer because the database in testing, development, and production can follow the same history. For example, if one teammate adds a new column and another teammate pulls the project, the migration file tells the second teammate exactly how to update their database too.

### How can you roll back a migration if an issue occurs?

- By using the migration:revert command. This runs the down() part of the latest migration and undoes the last database change. If more than one migration needs to be undone, you run the command again for each one

## Task 

- Created a data-source.ts file in the project root so TypeORM knows how to connect to PostgreSQL and where to find entities and migration files. 

![dataSource](image.png)

- Added migration scripts in package.json to make it easier to generate, run, and revert migrations from the terminal 

![MigrationScripts](image-1.png)

- Installed TypeORM and related packages  

![installingTypeORM](image-2.png)

- Used migration:generate and migration:run after adding a new field to the entity so TypeORM could create and apply a schema change to the database

![generate/run migration](image-3.png)

- Added sample seed data so the database would already contain example tasks when the app starts

![sampleseed](image-4.png)

- Started the development server and used a GET request to check that the seeded tasks were being returned from PostgreSQL 

![Get](image-5.png)

- Ran migration:revert to undo the latest migration and test that rollback works correctly!! 

![Reverting](image-6.png)
