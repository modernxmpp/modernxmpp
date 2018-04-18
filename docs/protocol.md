# XMPP Protocol Guidelines

## Overview

The XSF has published nearly 400 XEPs over many years. However as technology,
user expectations and best practices evolve, the protocol too is always evolving.

This leads to confusion about which set of XEPs are "current", which are required
only for backwards-compatibility, and which serve only to document experimental
protocols that never made it off the drawing board.

Instead of focusing on XEP numbers, this document simply focuses on the different
areas of functionality, and describes the currently-recommended XEPs that should be
used to implement each.

Notes are provided to provide context about past and future versions of the protocol,
which may be helpful for backwards-compatibility or planning future development.

### Target audience

The protocols discussed here should be implemented in reusable libraries. Client developers
may use this document to assist them in choosing an XMPP library, or submitting feature
requests or contributions to their library of choice.

Reusing libraries whenever possible reduces fragmentation and duplicated effort.

## Core

### Service discovery

One of the unique features of XMPP is its ability to support a diverse range of software
on a single network, yet always allow basic functionality to work.

Either due to the ongoing evolution of technology, or due to constrained environments (e.g. IoT)
or usage restrictions (e.g. accessibility), different XMPP software may support different
sets of features on top of the core messaging and presence functionality described in the
RFCs.

It is often useful to know what features a remote entity supports before performing some operation.
For example when deciding whether to send formatted messages, or determining the best available
method of transferring a file.

- XEP-0030 is the basic mechanism for advertising and discovering features
- XEP-0115 is a strongly recommended extension that allows caching of these features

#### Notes

XEP-0115 may be revised or replaced at some point in the future, such as by XEP-0390, to allow
hash agility and making the algorithm more robust to cache poisoning attacks.

## Messaging

This section covers some protocols that are useful for general messaging.

### Formatting

Client developers may implement the rules in XEP-0369 for formatting message bodies that they
receive.

#### XHTML-IM

A previous formatting specification defined in XEP-0071 has been deprecated. Many implementations
failed to properly sanitize the formatted payload, leading to security issues (particularly in web
applications).

Implementation of XEP-0071 is not encouraged, but if formatting is a strong requirement, along with
backwards compatibility (many clients still implement it currently), it remains an option.

## Multi-device

- XEP-0280
- XEP-0313

## Reliability

- XEP-0184
- XEP-0198

## File transfer

Transferring a file from A to B is surprisingly a non-trivial problem for the internet, it seems.

A number of approaches have been tried in XMPP. They are documented here, and fall into two categories:
peer-to-peer and server-mediated.

It is strongly recommended for clients to implement HTTP upload to provide the best user experience.
The other mechanisms are optional (the advantages of implementing each one are documented in the
relevant section).

### HTTP upload

The newest file transfer mechanism available, described in XEP-0363. It is strongly recommended to
implement this mechanism to provide the best user experience.

#### Benefits

- Does not depend on the recipient supporting it (simply falls back to sending a URL)
- Works with group chats
- Works when the recipient is offline
- Allows the recipient to receive on multiple devices

#### Disadvantages

- Unsuitable for large files (server determines what the size limit is, and may enforce usage quotas)
- Does not support streaming (file must be entirely uploaded to the server before recipient can begin to receive it)
- Requires server support

#### Usage

After uploading the file successfully, the sender should communicate the URL to the recipient by sending a
`<message>` stanza with the "Get URL" provided by the server in the `<body>` of the message.

Additionally the sender should include a [jabber:x:oob](https://xmpp.org/extensions/xep-0066.html#x-oob)
element in the message stanza with the same URL.

!!! note

    To enable automatic display of media in the conversation view, Conversations (at least) currently requires
    that the `<body>` contain *just* the URL, and it must be identical to the URL in the `jabber:x:oob` payload.
    
    The `<desc>` element is not used or supported.
    
    This behaviour means that it is not possible for any text to directly accompany a media file, and must
    be sent separately.

### Jingle

Jingle is a generic framework that allows clients to negotiate a direct stream between themselves, which can
be used to transfer files (it is also used for voice/video and other p2p applications based on XMPP). It was
originally developed at Google and contributed to the XSF where it evolved into today's standard.

Because it is a generic framework that supports different underlying transports and different media types,
Jingle is split into multiple XEPs. For file transfer the following are relevant:

- XEP-0166 - the core Jingle framework
- XEP-0234 - the Jingle file transfer definition
- XEP-0260 - the most common transport mechanism for files (SOCKS5 bytestreams - may be directly peer-to-peer or server-mediated)
- XEP-0261 - a fallback transport for tunnelling the data directly over the XMPP stream (inefficient and slow, but always succeeds)

#### Advantages

- Supports streaming (recipient receives at the same time as the sender sends)
- Allows code re-use if the client also implements Jingle for audio/video streams
- No server-side storage required, and the data will pass directly between clients if firewalls/network conditions allow, which makes
it suitable for larger files.

#### Disadvantages

- Because it is a multi-purpose framework it can be complex.
- Not all clients support it.
- In the case of the recipient having multiple devices, only a single one can receive the file.
- Does not work for sharing a file with multiple people (e.g. in a group chat)
- Only works if the recipient is online

!!! note

Although it is the only recommended negotiation protocol for peer-to-peer streams today, note that Jingle
support is not nearly universal even among modern clients.

### Stream Initiation (pre-Jingle)

XEP-0096 describes the stream negotiation protocol that was used before Jingle. It is widely supported, and can use the same
transports:

- XEP-0065
- XEP-0047

It is not recommended to implement this mechanism in new clients, except for compatibility with older clients
is required (and HTTP Upload does not suffice for some reason).

#### Advantages

- Supports streaming (recipient receives at the same time as the sender sends)
- Widely supported in older clients

#### Disadvantages

- Deprecated. Modern clients are switching to Jingle negotiation.
- In the case of the recipient having multiple devices, only a single one can receive the file.
- Does not work for sharing a file with multiple people (e.g. in a group chat)
- Only works if the recipient is online

## Avatars

## Group chat

## Contact management

- XEP-0191

## Encryption

All XMPP streams must be encrypted using TLS as specified in RFC 6920.

Clients may additionally support encrypting messages within the XMPP
stream. This can prevent untrusted servers from viewing or modifying
the contents of exchanged messsages, and is known as 'end-to-end
encryption'.

The current preferred protocol for this in XMPP is OMEMO, specified
in XEP-0384. Client support is indicated at [https://omemo.top/].

### Notes

#### OTR

Prior to OMEMO, many clients implemented the protocol-agnostic
encryption protocol "OTR".

Although it sufficed for simple use cases (sender and recipient have
a single device connected, and both support OTR), it has a number of
drawbacks when used within XMPP. Traditionally it has not supported multiple devices
very well, nor group chats, and it only protects the message body.

These issues lead to a poor user experience.

#### MLS

The IETF is currently working on standardizing a new protocol for
['Message Layer Security'](https://datatracker.ietf.org/wg/mls/about/)
with support from a number of prominent members of the online communications
space. It is hopeful that it may one day allow messaging applications
of all protocols to share code and crypto reviewed by experts.

However this work is in its early days, and OMEMO is expected to be
the recommended approach for some time to come.
