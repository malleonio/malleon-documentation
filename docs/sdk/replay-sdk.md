# Replay SDK (JavaScript)

The Replay SDK captures user sessions and enriches them with context (user info, tags, and custom metadata). This guide focuses on common usage patterns.

## Install
```bash
npm install @malleon/replay
```

## Initialize
Initialize the SDK once when your app starts.
```javascript
import * as ReplaySDK from "@malleon/replay";

ReplaySDK.initReplay("your-app-id");
```

## Add User Metadata
User metadata makes replays searchable and understandable.
```javascript
await ReplaySDK.updateReplayUserData({
  userId: "user-123",
  username: "jane_doe",
  userEmail: "jane@example.com",
  userRole: "admin"
});
```

## Add Tags
Tags help you filter sessions by feature, state, or environment.
```javascript
await ReplaySDK.addTagToReplay("plan", "pro", "STR");
await ReplaySDK.addTagToReplay("checkoutStep", 2, "NUM");
await ReplaySDK.addTagToReplay("isLoggedIn", true, "BOOL");

await ReplaySDK.addTagsToReplay([
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
