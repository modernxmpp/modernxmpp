TODO: Provide rationale for recommendations as footnotes

# Client design guidelines

This document lays out a set of guidelines for designing Modern XMPP clients. For contributions,
please [open an issue or pull request](https://github.com/modernxmpp/modernxmpp) at Github for discussion.

## Registration

TODO.

## Initial configuration

At initial startup, a client should present a welcome screen, to prompt the user for their JID,
and a password. Optionally, a button or link to provide other forms of credentials may be included.

If the client has an out-of-band configuration mechanism, or it can query the OS for sensible defaults,
it may use these.

## Configuration options
List recommended configuration options.

### Account

| Option | Description           |
|:-------|:----------------------|
| JID    | The user's JID        |
| Password | The user's password |

### Network

Support for these options is OPTIONAL. If included in the client, they MUST NOT
be requested by default at startup, but should be accessible through an advanced options interface.

| Option       | Description                        |
|:-------------|:-----------------------------------|
| Connect host | The network hostname to connect to |
| Connect port | The network port to connect to     |

Both of the above should be automatically discovered from DNS, according to the [rules in RFC 6120](https://xmpp.org/rfcs/rfc6120.html#tcp-resolution).
Clients that support other connection mechanisms, such as BOSH, SHOULD also implement [XEP-0156](https://xmpp.org/extensions/xep-0156.html).

### Deprecated options

Support for these options is NOT RECOMMENDED.

| Option       | Description                              | Notes |
|:-------------|:-----------------------------------------|:--------|
| Resource     |  The resource to request from the server | see [Resource generation](protocol.md#resource-generation)  |
| Priority     |  The priority to include in presence     | 0       |

## User status

The client, by default, MUST NOT include any status messages in its presence, unless they are chosen by the user. Built-in status messages that
convey the same meaning as the user's selected 'show' value (e.g. "Available", "Do not disturb") are not allowed.

Allowing the user to set a status message is an OPTIONAL feature.

## Contact list

### Terminology
In its interface, the client MUST NOT use the technical term "roster", but MUST instead use the term "contact list" (or a suitable translation)
where necessary. See the main "Terminology" section for more information.

### Offline contacts

The client MUST display offline contacts by default, and allow sending messages to them, as for online contacts..

### Sorting of contact list

The client MUST sort the contact list. Either alphabetically [TODO: lexical] or chronologically by the time of the last message exchanged.

### Visualizing status

The client MUST display status messages of contacts when present. It MAY also provide visual indication of the contact's status ('show'), but
SHOULD NOT rely on colour alone to distinguish different status values. [TODO: colours citation]

If a contact has multiple resources, an overall FIXME

## Conversation view

### Message states

#### Outgoing messages

A client must be able to unambiguously display the following outgoing message states:

* Message pending delivery
* Message delivered to server
* Message delivered to contact
* Message read by contact
* Delivery error for message

TODO: Table or flowchart

## Notifications

Carbons, notifications for new messages in MAM

## Error handling

Obey error types (modify, cancel, wait, etc.)

Do display error text

## Multiple accounts

Support for multiple accounts is OPTIONAL.

TODO: Research recommendations for the best way to handle multiple accounts. E.g. merge contacts, or not.
Not required. Describe how to display multiple accounts in a single client?

## Group chat

TODO: Recommendations for MUC (call group chat), separate recommendations for MIX down the road (i.e. allow adding to contact list).

## Documentation

TODO: Recommended documentation topics

Clients should have documentation covering essential functionality, including: TODO

## Privacy

Clients must not reveal full JID. Don't query unsubscribed contacts.
