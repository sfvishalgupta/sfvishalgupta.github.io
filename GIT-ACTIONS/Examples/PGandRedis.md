# PG and Redis in Runner
```yaml
name:  "Sourceloop CLI Run Automation Test Action"
on:
  push:
    branches: [ automation ]

permissions:
  contents: write

jobs:
  build-automation-test-for-sourceloop-cli:
    runs-on: ubuntu-latest
    services:
      postgres:
        image: postgres
        env:
          POSTGRES_USER: postgres
          POSTGRES_PASSWORD: admin
          POSTGRES_DB: microservices
        ports:
          - 5432:5432
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    permissions:
      id-token: write
      contents: write
      pull-requests: write

    steps:
      - name: Checkout
        uses: actions/checkout@v3
        with:
          persist-credentials: false
      
      - name: Install redis
        run: sudo apt-get install -y redis-tools redis-server
      
      - name: Verify that redis is up
        run: redis-cli ping

      - name: Use Node.js 18
        uses: actions/setup-node@v4
        with:
          node-version: 18
      
      - name: Setup SSH
        uses: MrSquaare/ssh-setup-action@v1
        with:
          host: github.com
          private-key: ${{secrets.SSH_PRIVATE_KEY}}
      
      - name: Install dependencies
        run: |
          npm i -g @loopback/cli
          npm i -g @sourceloop/cli
      
      - name: Start Sourceloop CLI Test
        run: ./scripts/start_sourceloop_cli.sh
```