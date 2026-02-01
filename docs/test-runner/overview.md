# Test Runner

The Test Runner executes Malleon test definitions in parallel. Deploy it in your infrastructure to run automated tests against your applications.

## Getting Access

The test runner image requires authentication to pull. Contact **support@malleon.io** to request access and receive your Personal Access Token (PAT).

## Quick Start

### 1. Authenticate with GitHub Container Registry

Using your PAT provided by Malleon:

```bash
echo "YOUR_PAT_TOKEN" | docker login ghcr.io -u malleonsupport --password-stdin
```

### 2. Pull and Run

```bash
# Pull the image
docker pull ghcr.io/malleonsupport/test-runner:latest

# Run with your Malleon JWT token (connects to https://malleon.io by default)
docker run -d \
  -p 9287:9287 \
  -e TEST_RUNNER_JWT=your-malleon-jwt-token \
  ghcr.io/malleonsupport/test-runner:latest

# Verify it's running
curl http://localhost:9287/api/test-runner/health
```

## Deployment Options

### Docker Compose

For a complete setup with Selenium Grid (optional, only needed for headful tests), use the [docker-compose.example.yml](docker-compose.example.yml):

```bash
# Download the example file
curl -O https://raw.githubusercontent.com/malleonio/malleon-documentation/main/docs/test-runner/docker-compose.example.yml

# Log in to GitHub Container Registry (using your PAT from Malleon)
echo "YOUR_PAT_TOKEN" | docker login ghcr.io -u malleonsupport --password-stdin

# Create .env file with your Malleon JWT
echo "TEST_RUNNER_JWT=your-malleon-jwt-token" > .env

# Start all services
docker-compose -f docker-compose.example.yml up -d
```

### Kubernetes

For Kubernetes deployments, use the [k8s-deployment.example.yaml](k8s-deployment.example.yaml):

```bash
# Create namespace
kubectl create namespace test-runner

# Create secret for GitHub Container Registry authentication (using your PAT from Malleon)
kubectl create secret docker-registry ghcr-secret \
  --docker-server=ghcr.io \
  --docker-username=malleonsupport \
  --docker-password=YOUR_PAT_TOKEN \
  -n test-runner

# Create secret with your Malleon JWT
kubectl create secret generic test-runner-jwt \
  --from-literal=jwt=your-malleon-jwt-token \
  -n test-runner

# Apply the deployment
kubectl apply -f k8s-deployment.example.yaml
```

**Note**: Selenium Grid is **optional** and only needed for headful/visual tests. Headless tests automatically use local Chrome and do not require Selenium Grid. If you only run headless tests, you can set `SELENIUM_GRID_ENABLED=false` to simplify deployment.

## Configuration

### Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `TEST_RUNNER_JWT` | **Yes** | - | JWT token generated from Malleon |
| `REPLAY_SERVER_URL` | No | `https://malleon.io` | Malleon server URL |
| `TEST_RUNNER_MODE` | No | `service` | Mode: `service` or `single-test` |
| `SELENIUM_GRID_URL` | No | `http://selenium-hub:4444` | Selenium Grid URL (only needed for headful tests) |
| `SELENIUM_GRID_ENABLED` | No | `true` | Enable Selenium Grid (only needed for headful tests) |
| `APP_SERVER_HOST` | No | `test-runner` | Hostname for browser access |
| `JAVA_OPTS` | No | `-Xmx2g -XX:+UseG1GC` | JVM options |
| `LOG_LEVEL` | No | `INFO` | Logging level |

---

## Before You Start

You will need:
- A **PAT** (Personal Access Token) from Malleon to pull the image - contact **support@malleon.io**
- Your **App ID**
- A **Test Runner JWT** generated in the Malleon web app
- A **Replay ID** to use as the test context base (typically from a stable, fixed build)

### Generate a Test Runner JWT

1. Open **Test Definitions** at [https://malleon.io](https://malleon.io).
2. Select your app.
3. Click **Test Runner**.
4. Create a token and generate a JWT.
5. Store the JWT securely.

### Authentication

The test runner supports two authentication methods:
- **Environment variable** (recommended): Set `TEST_RUNNER_JWT` when deploying the runner. The JWT will be used automatically for all API calls.
- **Request header**: Include `Authorization: Bearer YOUR_TEST_RUNNER_JWT` in each request. This is only needed if `TEST_RUNNER_JWT` is not configured.

If both are provided, the environment variable takes precedence.

## Run Tests in Parallel

The runner accepts a **parallelism** setting:
- `1` = sequential (one test at a time)
- `> 1` = fixed number of concurrent tests
- `0` = unlimited (all tests at once)

### Example Request

Replace `RUNNER_URL` with your runner address (e.g., `http://localhost:9287`).

If `TEST_RUNNER_JWT` is configured (recommended):
```bash
curl -X POST "RUNNER_URL/api/test-runner/run?appId=YOUR_APP_ID&contextReplayId=YOUR_REPLAY_ID&parallelism=5" \
  -H "Content-Type: application/json" \
  -d '{ "pageNum": 1, "pageSize": 100, "searchRequest": {} }'
```

If `TEST_RUNNER_JWT` is not configured, include the Authorization header:
```bash
curl -X POST "RUNNER_URL/api/test-runner/run?appId=YOUR_APP_ID&contextReplayId=YOUR_REPLAY_ID&parallelism=5" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_TEST_RUNNER_JWT" \
  -d '{ "pageNum": 1, "pageSize": 100, "searchRequest": {} }'
```

### What This Does

- Uses your **contextReplayId** to load the resources for the test run.
- Runs active tests for the selected app.
- Returns a summary with pass/fail results.

## Health Check

Verify the test runner is running:

```bash
curl http://localhost:9287/api/test-runner/health
```

Returns `OK` if healthy.

## Tips

- Use a stable replay ID from a known-good build as the context.
- Start with low parallelism and increase as your runner capacity grows.
- Use the Malleon web app to manage test definitions and contexts.
- Pin to a specific image tag (e.g., `main-abc123`) for reproducible builds.

## Support

For questions or to request access, contact **support@malleon.io**.
