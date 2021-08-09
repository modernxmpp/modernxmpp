# Syncing Message History

## MAM Strategies

Fetching history from the server is accomplished with [Message Archive
Management][MAM] (MAM).
New XMPP clients frequently use naïve methods of querying history that result in
long wait times for history, or frozen UIs.
However, a robust strategy for fetching history has not been previously
documented.
This section documents strategies used by clients in the wild, as well as
implementation recommendations for MAM.

### Requirements

- Allow the user to send a message in response to history fetched from the
  server as quickly as possible
- Do not generate dozens of notifications for old messages

### Implementation Notes

- Don't treat history like normal incoming messages.
  If querying lots of messages, aggregate and commit them to the data store
  (assuming a transactional database) as a group.
  Do the same for updating the UI and displaying notifications.
- Look up the last message _before_ sending initial presence, otherwise you
  may receive a message before you get the last ID and end up with a gap.
- If using paging, committing one page at a time to the DB/UI is a natural way
  to break up large transactions and provide the user with quicker feeling
  updates.

[MAM]: https://xmpp.org/extensions/xep-0313.html
