# Multi-user Chats

## Types of chat

There are two kinds of multi-user chat. Private *group chats*, and public *channels*[^rationale-gc].

### Properties

|                         | Group chat | Channel |
|:------------------------|:-----------|:--------|
| Persistent              | Yes        | Yes     |
| MAM enabled             | Yes        | Yes     |
| Subject editable        | No         | No      |
| Members-only            | Yes (\*)   | No      |
| XMPP addresses revealed | Yes (\*)   | No      |
| Publicly listed         | No  (\*)   | Yes     |
| PMs                     | No  (\*)   | Yes     |

(\*) Immutable for *group chats*.

### Terminology

People in the *group chat* / *channel*: *Participants*

Roles are not displayed and cannot be modified through the UI.


| Affiliations | In group chats | In channels |
|:-------------|:--------------:|:-----------:|
| none         | N/A **         | Guest       |
| member       | -              | -           |
| admin        | *Admin* (\*)   | Admin       |
| owner        | Owner          | Owner       |

(\*) A *group chat* will display an existing admin as such but it will not encourage/allow
someone to be promoted to admin. UI options in *group chats* only allow a member to become
an owner but not admin. So admins are discouraged by the UI but will be displayed as such
if they end up being one for some reason.

(\*\*) Everybody is a member in *group chats*

Clients MAY create an 'advanced view' that displays roles as well.

## User nickname

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

XMPP address username
: The username portion of the user's XMPP address (i.e. before the '@').

### Other user's names

The display of other user's names is covered in the [general UI recommendations](design.md#names).

## Bookmarks

!!! todo
    Bookmark management logic

## Private messages

Clients must always use real XMPP addresses for messaging privately within a *group chat* if (and only if) XMPP addresses are publicly visible to all participants.[^pm-realjid]

<!-- Footnotes -->

[^rationale-gc]: Rationale [group chats](/rationale#group-chats)
[^local-nickname]: To avoid requiring the user to configure a nickname manually on each device, shared cross-device stores such as PEP and vCard should be preferred.
[^pm-realjid]: If real XMPP addresses are known to all participants, it is preferable to use that for private communication to avoid confusion. Through-MUC PMs have the following disadvantages:

    - Only work while connected to the group chat
    - Do not interact well with multiple devices (e.g. not all of a recipient's devices may be in a group chat)
    - Can cause confusion if talking to the same person through different views (e.g. if the person is already a contact in your roster, and you already have a chat open with them)

    However if the sending user is an admin of a room where XMPP addresses are hidden, using a real XMPP addresses will reveal the admin's private XMPP addresses to the recipient. Either warn the sender that their XMPP addresses will be revealed, or always use the in-room XMPP address in such channels.
