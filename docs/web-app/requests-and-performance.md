# Requests and Performance

The **Requests** page is your performance hub. It helps you find slow endpoints, compare services over time, and define custom service groupings.

## Search and Filters
1. Open **Requests**.
2. Select a time range.
3. Use filters for:
   - Request fields (method, URL, status, response time)
   - Tags
   - Replay search
   - Emotional indicators
4. Click **Search** to load results.

## View Modes
You can switch between three views:

### Raw Results
See individual request occurrences, including:
- Timestamp, method, URL, status
- Elapsed time
- Request details (payload/response)
- Nearby logs
- Replay links

### Aggregated Stats
Group requests by service and URL pattern to identify hot spots:
- Average and median response times
- Percentiles (P90/P95/P99)
- Count and impact score

**Bottleneck filters** help focus on slow, frequent endpoints:
- Min response time
- Min requests per hour

### Time Series
Compare performance trends over time:
- Select services
- Choose a metric (count, average, median, P95, error rate)
- Choose an interval (minute, hour, day)
- Load time series to compare services side by side

## Service Filters
Service filters let you focus analytics on specific services:
1. Expand **Service Filter**.
2. Select one or more services from the list.
3. Click **Search** to apply the filter.

You can also hide **system fallback** services (auto-created from requests) to focus on your curated definitions.

## Manage Service Definitions
Service definitions let you group endpoints using URL patterns.

1. Expand **Manage Service Definitions**.
2. Click **Add Service**.
3. Provide:
   - **Name** (e.g., "Payments API")
   - **Description** (optional)
   - **HTTP methods**
   - **URL pattern** (glob)

### URL Pattern Rules
- Use `*` to match a single path segment.
- Use forward slashes to separate segments.
- `**` is not supported.

Examples:
- `/api/*/users/*`
- `/api/orders/*/items/*`
- `/api/*/v1/*`

After saving, the service may show a brief **backfilling** status while historical requests are processed.
