# Replays and Debugging

Replays let you reconstruct user sessions and debug problems quickly. Search replays, start one locally, and correlate logs.

## Find and Filter Replays
1. Open **Replays**.
2. Select your app in the header selector.
3. Set a **time range** for the session start time.
4. Use filters to narrow results:
   - **Replay fields** (e.g., browser, OS, location, user)
   - **Tag search** (custom metadata from your SDK)
   - **Log search** (find sessions with specific log messages)
   - **Emotional indicators** (behavioral flags)
5. Click **Search** to refresh results.

## Start a Replay (Local Playback)
Malleon uses a local Replay Client to start replays on your machine.

1. Make sure the **Replay Client** is installed and running.
2. In the replay list, click **Start Replay** for the session you want to view.
3. The Replay Client will launch playback and render the session.

If you need to download / install the client:
1. Open **Replay Client Download** (https://malleon.io/#/replay-client-download).
2. Download the installer for your OS.
3. Install and launch it.
4. Once running, the header status badge turns green to show it is connected.

The Replay Client runs locally on port `9287`.

## Record a New Replay
Use **Record Replay** from the replay list to create a new recording session for a replay you want to inspect interactively.

## View Nearby Logs
From the replay table:
1. Click **Nearby Logs** to open logs around that replay.
2. Use this to see what happened immediately before and after a session.

## Add and Review Tags
Use **Tags** to view and manage replay tags set by the SDK. Tags help you quickly find sessions based on user or application context.

## Replay Player (Video + Logs)
The **Replay Player** page lets you open a recording video file and view synchronized log lines:
1. Select a replay recording file (for example, a file named `replay-recording-<uuid>.mp4`).
2. The player loads the matching replay data and log timeline.
3. Use the timeline markers to jump to logs and errors.

This is useful when you have a recording file and want a log-synced view of the session.
