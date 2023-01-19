# ⚠️ Error Handling

### API Errors

We have set up an interceptor for handling errors. We use it to fire a notification toast to notify users that something went wrong, log out unauthorized users, or send new requests for refreshing tokens.

[API Errors Notification Example Code](../src/lib/axios.ts)
