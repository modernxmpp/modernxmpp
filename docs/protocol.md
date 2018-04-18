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

## Mobile

- XEP-0286
- XEP-0352

## Multi-device

- XEP-0280
- XEP-0313

## File transfer

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
