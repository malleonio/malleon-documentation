# Tests and Alerts

This guide covers creating tests from replays, using test contexts, approving candidate tests, and configuring alerts.

## Create a Test from a Replay
1. Open **Test Definitions**.
2. Select your app.
3. Click **Create New Test**.
4. Provide:
   - **Name**
   - **Replay ID** (copy from Replays, Logs, or Errors)
   - Optional description
   - Optional failure conditions (see below)
5. Save the test definition.

### Failure Conditions
Tests can fail based on:
- **LOG/WARN/ERROR/THROW** regex patterns
- **DOM** selectors (present or missing, with timeout)

If you add no conditions, the test uses **implied test mode** and fails on console errors or exceptions automatically.

## Run a Test Locally
1. Make sure the **Replay Client** is running.
2. Open the test definition.
3. Click **Run Test**.
4. Review the results (pass/fail and captured logs).

## Test Contexts (Overrides and Fixed Builds)
Test contexts let you run a test against a specific set of resources or API responses.

### Create a Test Context
1. Open **Test Contexts**.
2. Select your app.
3. Click **Create New Test Context**.
4. Optionally set a **Resource Replay ID** to load CSS/JS from a specific replay.
5. Add **Request Overrides** for API responses if needed.
6. Save the context.

### Use a Context in a Test Run
1. Open **Test Definitions** and select a test.
2. Choose a context under **Test Context Selection**.
3. Click **Run Test**.

### Workflow Example: Verify a Fix
1. Identify a failing replay from **Errors** or **Logs**, and create a test definition using its Replay ID.
2. Fix the bug locally.
3. Run your app and produce a new replay (now on the fixed build).
4. Copy the new Replay ID and create/update a **Test Context** with this Replay ID as the **Resource Replay ID**.
5. Run the original test using the new context to validate the fix.

## Candidate Tests (Unique Errors)
Candidate tests are generated from unique errors:
1. Open **Test Candidates**.
2. Review the candidate details and error description.
3. Click **Approve** to turn it into an active test definition.

## Alerts
Alerts notify you when logs match a pattern.

### Create an Alert
1. Open **Alerts**.
2. Click **Create New Alert**.
3. Provide:
   - Alert name and description
   - Regex pattern (applied to log messages)
   - Log levels (log, warn, error)
   - Email recipients
4. Save the alert.

### Manage Alerts
- Enable or disable alerts as needed.
- Edit or delete alerts from the list.
- Review **execution stats** for the current hour.
