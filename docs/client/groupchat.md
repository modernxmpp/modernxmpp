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

# Bookmarks
