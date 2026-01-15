# Replay CLI (Sourcemap Upload)

Replay CLI uploads source maps so stack traces in Malleon show readable file names and line numbers.

## Install
```bash
npm install -g @malleon/replay-cli
```

## Get Your Source Map Token
1. Open **Apps**.
2. Select your app.
3. Open **App Details**.
4. Click **Generate Source Map Token**.

Keep this token secret. Anyone with it can upload source maps for your app.

## Basic Upload
```bash
replay-cli upload \
  --app-id YOUR_APP_ID \
  --token YOUR_SOURCE_MAP_TOKEN \
  --url https://yourapp.com \
  --release 1.2.3 \
  --source-map-dir dist
```

### Required Options
- `--app-id`: Your App ID from the Malleon web app.
- `--token`: Source map token from **App Details**.
- `--url`: The URL where your app is deployed. This should match the URL seen in replays.

### Common Options
- `--release`: Release version (recommended for tracking deployments).
- `--dist`: Distribution identifier (optional).
- `--source-map-dir`: Directory containing `.map` files (default: `.`).
- `--include`: Glob patterns to include (default: `**/*.map`).
- `--exclude`: Glob patterns to exclude.
- `--url-pattern`: Regex pattern to match multiple URLs.

## Typical Use Cases

### Single Production Site
```bash
replay-cli upload \
  --app-id YOUR_APP_ID \
  --token YOUR_SOURCE_MAP_TOKEN \
  --url https://yourapp.com \
  --release 1.2.3 \
  --source-map-dir dist
```

### App Hosted on a Subpath
```bash
replay-cli upload \
  --app-id YOUR_APP_ID \
  --token YOUR_SOURCE_MAP_TOKEN \
  --url https://yourapp.com/app/ \
  --release 1.2.3 \
  --source-map-dir dist
```

### Multiple Environments
Use different `--url` values for staging vs production:
```bash
replay-cli upload \
  --app-id YOUR_APP_ID \
  --token YOUR_SOURCE_MAP_TOKEN \
  --url https://staging.yourapp.com \
  --release 1.2.3-staging
```

## Verify Source Maps
1. Trigger an error in your app.
2. Open **Errors** in Malleon.
3. The stack trace should show original source files and line numbers.

If stack traces still look minified, re-check the URL you used during upload and confirm you are viewing errors that occurred after the upload.
