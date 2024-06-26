#### [Back](./README.md)

# Database Migrations

In LoopBack, auto-migration helps the user create relational database schemas based on definitions of their models. Auto-migration can facilitate the synchronization of the backing database and models so that they match, such as in cases where the database needs to be changed in order to match the models. LoopBack offers two ways to do this:

* **Auto-migrate:** Drop schema objects if they already exist and re-create them based on model definitions. Existing data will be lost.

* **Auto-update:** Change database schema objects if there is a difference between the objects and model definitions. Existing data will be kept.

Part of the database schema definition can be specified via the model and/or property definition. For example, the following property setting is a common definition that indicates the schema, the table name, the data type and the length of a column, and also uses a column name that is different from the property name:

```typescript
@model({
  settings: {
    postgresql: {schema: 'quarter2', table: 'my_model'},
  },
})
export class MyModel extends Entity {
  @property({
    type: 'string',
    required: false,
    id: false,
    postgresql: {
      columnName: 'my_name',
      dataType: 'VARCHAR',
      dataLength: 20,
      nullable: 'YES',
    },
  })
  myName: string;
}
```

## Auto-update database at start
To automatically update the database schema whenever the application is started, modify your main script to execute app.migrateSchema() after the application was bootstrapped (all repositories were registered) but before it is actually started.

src/index.ts
```typescript
export async function main(options: ApplicationConfig = {}) {
  const app = new TodoListApplication(options);
  await app.boot();
  await app.migrateSchema();
  await app.start();

  const url = app.restServer.url;
  console.log(`Server is running at ${url}`);

  return app;
}
```

## Auto-update the database explicitly
It’s usually better to have more control about the database migration and trigger the updates explicitly. To do so, projects scaffolded using lb4 app come with a custom CLI script src/migrate.ts to run schema migration.

Besides the migration CLI, new projects come with a handy npm script to run the migration too.

The migration process consists of two steps now:

1. Build the project
```bash
npm run build
```

2. Migrate database schemas (alter existing tables):
```bash
npm run migrate
```
Alternatively, you can also tell the migration script to drop any existing schemas:

```bash
npm run migrate -- --rebuild
```

## Skipping a dataSource for migration
In some cases you do not want specific datasource(s) to be included in the migration process. For example, depending on the process.env.NODE_ENV you might be restricted to ALL or specific datasources from altering the table schemas.

For such scenarios, you can include the property disableMigration in the datasource configuration. The Datasource will only be skipped from the migration process if you set it to true.

If you do not include it or if you set it to false then your datasource will be migrated, this is to provide a non-breaking change with this new property.

src/datasources/db.datasource.ts
```typescript
const config = {
  name: 'db',
  connector: 'memory',
  localStorage: '',
  file: './data/db.json',
  disableMigration: true,
};
```

## Implement additional migration steps
In some scenarios, the application may need to define additional schema constraints or seed the database with predefined model instances. This can be achieved by overriding the **migrateSchema** method provided by the mixin.

src/application.ts
```typescript
import {TodoRepository} from './repositories';
// skipped: other imports

export class TodoListApplication extends BootMixin(
  ServiceMixin(RepositoryMixin(RestApplication)),
) {
  // skipped: the constructor, etc.

  async migrateSchema(options?: SchemaMigrationOptions) {
    // 1. Run migration scripts provided by connectors
    await super.migrateSchema(options);

    // 2. Make further changes. When creating predefined model instances,
    // handle the case when these instances already exist.
    const todoRepo = await this.getRepository(TodoRepository);
    const found = await todoRepo.findOne({where: {title: 'welcome'}});
    if (found) {
      todoRepo.updateById(found.id, {isComplete: false});
    } else {
      await todoRepo.create({title: 'welcome', isComplete: false});
    }
  }
}
```

