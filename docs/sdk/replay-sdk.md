# Replay SDK (JavaScript)

The Replay SDK captures user sessions and enriches them with context (user info, tags, and custom metadata). This guide focuses on common usage patterns.

## Install
```bash
npm install @malleon/replay
```

## ES Module Usage (Recommended)
Initialize the SDK once when your app starts (as early as possible in your app bootstrap).

```javascript
import { initReplay } from "@malleon/replay";

initReplay("your-app-id", { release: "1.0.0", dist: "production" });
```

ES module imports do not auto-initialize, so you must call `initReplay()` explicitly—typically in your main entry point, router setup, or app initialization logic.

## UMD Script Tag Usage
When loading the Replay SDK via a script tag (using `replay.umd.js`), the library **auto-initializes** as soon as it finds an `appId`. You can pass configuration in several ways.

### Script URL Parameters
Add query parameters to your script `src` attribute:

```html
<script src="https://malleon.io/assets/replay.umd.js?appId=your-app-id&release=1.0.0&dist=production"></script> (or your CDN)
```

| Parameter | Description |
|-----------|-------------|
| `appId` | (Required) Your application ID |
| `release` | (Optional) Release or version string (e.g. `1.0.0`) |
| `dist` | (Optional) Distribution or environment (e.g. `production`, `staging`) |
| `skipReplayAutoInit` | If present, disables auto-initialization so you can call `initReplay()` manually when ready |

Example: skip auto-init and manually initialize later:

```html
<script src="https://malleon.io/assets/replay.umd.js?skipReplayAutoInit"></script> (or your CDN)
<script>
  // Your code sets appId when ready, then:
  window.waitForAppIdAndInitReplay();  // polls until appId found, then inits
  // Or call directly when you have the values:
  window.initReplay('your-app-id', { release: '1.0.0', dist: 'production' });
</script>
```

### Auto-Initialization
When loaded via a UMD script tag **without** `skipReplayAutoInit`, the SDK automatically calls `waitForAppIdAndInitReplay()`, which polls every 100ms until it finds an `appId`, then initializes. No manual `initReplay()` call is needed.

### Configuration Sources (Priority Order)
The SDK looks for `appId`, `release`, and `dist` in this order (first match wins):

1. **Script URL** — query params on the script tag’s `src` (`appId`, `release`, `dist`)
2. **Window** — `window.__replay__appId`, `window.__replay__release`, `window.__replay__dist`
3. **Page URL** — search params `replayAppId`, `replayRelease`, `replayDist`
4. **Hash URL** — same param names in the URL hash (e.g. `#/path?replayAppId=xyz`)
5. **localStorage** — keys `__replay__appId`, `__replay__release`, `__replay__dist`
6. **sessionStorage** — same keys

Example: set before the script loads for late-binding of appId:

```html
<script>
  window.__replay__appId = 'your-app-id';
  window.__replay__release = '1.0.0';
  window.__replay__dist = 'production';
</script>
<script src="https://malleon.io/assets/replay.umd.js"></script> (or your CDN)
```

## Add User Metadata
User metadata makes replays searchable and understandable.
```javascript
import { updateReplayUserData } from "@malleon/replay";

await updateReplayUserData({
  userId: "user-123",
  username: "jane_doe",
  userEmail: "jane@example.com",
  userRole: "admin"
});
```

## Add Tags
Tags help you filter sessions by feature, state, or environment.
```javascript
import { addTagToReplay, addTagsToReplay } from "@malleon/replay";

await addTagToReplay("plan", "pro", "STR");
await addTagToReplay("checkoutStep", 2, "NUM");
await addTagToReplay("isLoggedIn", true, "BOOL");

await addTagsToReplay([
  { name: "browser", value: "chrome", type: "STR" },
  { name: "release", value: "1.4.2", type: "STR" }
]);
```

## Common Patterns
- **User identity:** set `userId`, `username`, and `userEmail` when a user logs in.
- **Feature flags:** add tags like `featureX=true`.
- **Funnels:** add tags when users reach key steps (signup, checkout, onboarding).
- **Environment:** add a `release` or `env` tag to separate staging vs production.

## Example Integrations (GitHub)
- Angular: https://github.com/malleonio/malleon-example-angular
- React: https://github.com/malleonio/malleon-example-react
- Svelte: https://github.com/malleonio/malleon-example-svelte
- Vue: https://github.com/malleonio/malleon-example-vue

## Tips
- Always call `initReplay()` before using other SDK functions.
- Use consistent tag names for easier filtering.
- Upload source maps so stack traces show your real source files.
