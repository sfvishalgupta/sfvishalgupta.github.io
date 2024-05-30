#### [Back](./README.md)

# Installing Loopback 4

1. Install Nodejs
2. Install Loopback 4 CLI
    ```bash
    npm install -g @loopback/cli
    ```
3. Create New Project
    ```bash
    lb4 app
    ```
4. Starting a Project
    ```bash
    cd project && npm start
    ```
5. Create Controller
    ```bash
    lb4 controller
    ```
    Copy below code to hello controller
    ```typescript
    import { get } from '@loopback/rest';
    export class HelloController {
        @get('/hello')
        hello(): string {
            return 'Hello world!';
        }
    }
    ```
