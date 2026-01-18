# Test Runner (Parallel Tests)

The Test Runner executes Malleon test definitions in parallel. This page assumes your runner is already deployed and reachable.

## Before You Start
You will need:
- Your **App ID**
- A **Test Runner JWT** generated in the Malleon web app
- A **Replay ID** to use as the test context base (typically from a stable, fixed build)

### Generate a Test Runner JWT
1. Open **Test Definitions**.
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
Replace `RUNNER_URL` with your runner address.

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

## Tips
- Use a stable replay ID from a known-good build as the context.
- Start with low parallelism and increase as your runner capacity grows.
- Use the Malleon web app to manage test definitions and contexts.
