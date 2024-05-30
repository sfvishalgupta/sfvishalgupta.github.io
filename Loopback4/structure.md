#### [Back](./README.md)

# Project Folder Structure

```bash
public/
  index.html

src/
  __tests__/
    README.md
    acceptance/
      home-page.acceptance.ts
      ping.controller.acceptance.ts
      test-helper.ts
  
  controllers/
    index.ts
    README.md
    ping.controller.ts
  
  datasources/
    README.md
  
  models/
    README.md
  
  repositories/
    README.md
  
  application.ts
  index.ts
  migrate.ts
  sequence.ts

node_modules/
  ***

LICENSE
README.md
package.json
tsconfig.json
.eslintrc.js
.prettierrc
.mocharc.json
```

| File          | Purpose    |
| ------------- | --------   |
| package.json              |   Your application’s package manifest.
| tsconfig.json             |   The TypeScript project configuration.
| .eslintrc.js              |   ESLint Configuration
| .prettierrc               |   Prettier configuration
| README.md                 |   The Markdown-based README generated for your application.
| LICENSE                   |   A copy of the MIT license. If you do not wish to use this license, please delete this file.
| src/application.ts        |   The application class, which extends RestApplication by default. This is the root of your application, and is where your application will be configured. It also extends RepositoryMixin which defines the datasource.
| src/index.ts              |   The starting point of your microservice. This file creates an instance of your application, runs the booter, then attempts to start the RestServer instance bound to the application.
| src/sequence.ts           |   An extension of the Sequence class used to define the set of actions to take during a REST request/response.
| src/datasources/README.md |   Provides information about the datasources directory, how to generate new datasources, and where to find more information.
| src/models/README.md      |   Provides information about the models directory, how to generate new models, and where to find more information.
| src/repositories/README.md |  Provides information about the repositories directory, how to generate new repositories, and where to find more information.
| .mocharc.json             | Mocha configuration for running your application’s tests.
