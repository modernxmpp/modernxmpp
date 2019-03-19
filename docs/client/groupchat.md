# Multi-user Chats

## Types of chat

There are two kinds of multi-user chat. Private group chats, and public channels.

### Properties

|                  | Group chat | Channel |
|:-----------------|:-----------|:--------|
| Persistent       | Yes        | Yes     |
| MAM enabled      | Yes        | Yes     |
| Subject editable | No         | No      |
| Members-only     | Yes (\*)   | No      |
| JIDs revealed    | Yes (\*)   | No      |
| Publicly listed  | No  (\*)   | Yes     |
| PMs              | No  (\*)   | Yes     |

(\*) Immutable for group chats.

### Terminology

People in the group chat / channel: Participants

Roles are not displayed and cannot be modified through the UI.


| Affiliations | In groupchats | In channels |
|:-------------|:-------------:|:-----------:|
| none         | N/A **        | Guest       |
| member       | -             | -           |
| admin        | *Admin* (\*)  | Admin       |
| owner        | Owner         | Owner       |

(\*) A group chat will display an existing admin as such but it will not encourage/allow
someone to be promoted to admin. UI options in group chats only allow a member to become
an owner but not admin. So admins are discouraged by the UI but will be displayed as such
if the end up being one for some reason.

(\*\*) Everybody is a member in groupchats

Clients MAY create an 'advanced view' that displays roles as well.

# User nickname

When joining a group chat, a client needs to select a nickname to use. There are multiple
sources from which this name may be selected. The client should use the following sources
in order:

Bookmark
: If the chat is present in the user's bookmarks and has a nickname present (as the resource).

Reserved name
: A chat [may be queried](https://xmpp.org/extensions/xep-0045.html#reservednick) to fetch the
    name that is registered by the user for that chat.

User nickname (PEP)
: The name stored in the user's account according to
    [XEP-0172](https://xmpp.org/extensions/xep-0172.html#manage).

User nickname (vCard)
: The name stored in the user's vCard as `NICKNAME`.

Local nickname
: (Optional, not recommended[^local-nickname]) A nickname previously configured by the user in this client instance.

JID username
: The username portion of the user's JID (i.e. before the '@').

# Bookmarks

!!! todo
    Bookmark management logic

<!-- Footnotes -->

[^local-nickname]: To avoid requiring the user to configure a nickname manually on each device, shared cross-device
    stores such as PEP and vCard should be preferred.
