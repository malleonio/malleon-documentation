# Getting Started with the Malleon Web App

Sign up, log in, create an app, integrate the SDK, and start seeing data.

## 1) Sign Up and Verify
1. Open the Malleon website and click **Start Free**.
2. Enter your organization name and admin email.
3. Check your inbox for the verification email and follow the link.

## 2) Log In and Select a Tenant
1. Go to **Login** and enter your credentials.
2. If you belong to multiple tenants, select the one you want to use.

## 3) Create Your First App
1. Open **Apps**.
2. Click **Add App** and give it a name.
3. Open the app details panel to see:
   - **App ID** (used by the SDK)
   - **Source Map Token** (used for uploads)
   - **Source Map Matching Strategy** (how replays match to source maps)

## 4) Integrate the Replay SDK
You will need the **App ID** from the previous step.

### SDK Integration Checklist
- Install `@malleon/replay` in your app.
- Initialize the SDK with your App ID.
- Add user metadata and tags as needed.

See the SDK guide for steps and examples:
- [../sdk/replay-sdk.md](../sdk/replay-sdk.md)

Example integrations:
- Angular: https://github.com/malleonio/malleon-example-angular
- React: https://github.com/malleonio/malleon-example-react
- Svelte: https://github.com/malleonio/malleon-example-svelte
- Vue: https://github.com/malleonio/malleon-example-vue

## 5) Upload Source Maps (Optional but Strongly Recommended)
Source maps turn minified stack traces into readable source file locations.

1. In **Apps → App Details**, generate a **Source Map Token**.
2. Build your web app so `.map` files are produced.
3. Use Replay CLI to upload source maps.

See the CLI guide:
- [../cli/replay-cli.md](../cli/replay-cli.md)

## 6) Start Exploring Your Data
Once users interact with your site, data will appear in:
- **Replays** for session playback
- **Errors** for error aggregates and occurrences
- **Logs** for structured log search
- **Requests** for API performance

Next steps:
- [replays-and-debugging.md](replays-and-debugging.md)
- [errors-and-logs.md](errors-and-logs.md)
- [requests-and-performance.md](requests-and-performance.md)
- [tests-and-alerts.md](tests-and-alerts.md)
