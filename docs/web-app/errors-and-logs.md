# Errors and Logs

Use **Error Analytics** and **Logs** to find issues fast, see how often they happen, and jump directly into replays.

## Error Analytics
Error Analytics groups similar errors into aggregates so you can focus on impact and frequency.

### Search and Filter
1. Open **Errors**.
2. Select a time range.
3. Add filters using:
   - **Log fields** (message, level, details)
   - **Tags**
   - **Replay search**
   - **Emotional indicators**
4. Click **Search** to load aggregates.

### Drill into Occurrences
1. Click **View** on an aggregate to see individual occurrences.
2. Each occurrence shows:
   - Timestamp
   - Location (source-mapped when available)
   - Message and details
   - **Replay ID** to copy and replay locally

If you have uploaded source maps, stack traces will show original source files and line numbers instead of minified code.

## Logs
Logs provide a searchable timeline of console logs, warnings, and errors.

### Search Logs
1. Open **Logs**.
2. Set a time range.
3. Use filters for:
   - Log fields (message, level, details)
   - Tags
   - Replay search
   - Emotional indicators
4. Click **Search** to load results.

### Jump to a Replay
When a log entry has a replay ID:
1. Click **Replay ID** to copy it.
2. Click **Start Replay** to open that session in the Replay Client.

## Tips
- Use a short time window first (e.g., last hour) to avoid noisy results.
- Upload source maps to make stack traces actionable.
- Use tags to segment by user type, feature, or environment.
