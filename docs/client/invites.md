# Registration through invitation

## Invitation types

### Account-only

Invitation to register an account on a given domain:
```
xmpp:example.com?register;preauth=3c7efeafc1bb10d034
```
or an invitation to register an account with a **specific** username
only:
```
xmpp:romeo@example.com?register;preauth=3c7efeafc1bb10d034
```

See the *Registration protocol* section of this document for how to
handle this type of invitation.

### Subscription-only

A potential contact invites you to communicate with them:
```
xmpp:contact@example.com?roster;preauth=3c7efeafc1bb10d034
```

The protocol to handle this type of invitation is specified in
[XEP-0379: Pre-authenticated Roster Subscriptions](https://xmpp.org/extensions/xep-0379.html).
After following the protocol, you will have a mutual presence subscription
with `contact@example.com`.

If the user does not currently have an account, the client must walk
them through the account registration process on a suitable XMPP service.

### Account-and-subscription

The same as a subscription-only invite, but it indicates you
are able to use the token to also register an account on the contact's
domain, signalled by the presence of `ibr=y` in the URI parameters:

```
xmpp:contact@example.com?roster;preauth=3c7efeafc1bb10d034;ibr=y
```

If the recipient of such an invite does not yet have an account, the
client should follow the *Registration protocol* section of this document.
After completing the registration, the user will automatically be subscribed
to the sender of the invitation.

If the recipient already has an XMPP account, the invitation should be
handled the same as a subscription-only invitation documented above,
and follow the protocol defined in [XEP-0379](https://xmpp.org/extensions/xep-0379.html).

# Registration protocol

Server sends stream features:

```xml
<stream:features>
  <mechanisms xmlns='urn:xmpp:sasl:0'>
    <mechanism>EXTERNAL</mechanism>
    <mechanism>SCRAM-SHA-1-PLUS</mechanism>
    <mechanism>SCRAM-SHA-1</mechanism>
    <mechanism>PLAIN</mechanism>
  </mechanisms>
  <register xmlns='urn:xmpp:invite'/>
  <register xmlns='http://jabber.org/features/iq-register'/>
</stream:features>
```

Client sees that registration through token is supported,
and initiates the registration flow:

```xml
<iq type="set" to="example.com" id="pa1">
  <preauth xmlns='urn:xmpp:pars:0' token='3c7efeafc1bb10d034' />
</iq>
```

Upon receiving the preauth request, the server should validate that the
token is acceptable for account registration. However single-use tokens
MUST NOT be considered used until the actual registration has succeeded.

In addition, if the token has an expiration time, it MUST only be checked
at this point. Subsequent actions performed by the client during the current
session that require a valid token MUST NOT be rejected due to token expiry.

Server responds with success, and indicates
the client may now proceed with account registration:

```xml
<iq type="result" from="example.com" id="pa1" />
```

If the token provided by the client was unknown, invalid or expired, the
server should return an appropriate error to the client:

```xml
<iq type="error" from="example.com" id="pa1">
  <error type='cancel'>
    <item-not-found xmlns='urn:ietf:params:xml:ns:xmpp-stanzas'/>
    <text>The provided token is invalid or expired</text>
  </error>
</iq>
```

In the success case, the client proceeds with registration using e.g.
XEP-0077 in the normal way.

# Creating an invitation

Users may request an invite (suitable for sharing to a desired new contact)
by using the ad-hoc command defined in [XEP-0401: Easy User Onboarding](https://xmpp.org/extensions/xep-0401.html#create-invitation).

The server will provide at minimum an `xmpp:` URI that can be interpreted by any compatible XMPP client. However this URI SHOULD NOT be shared directly by clients. It is generally likely that the recipient of an invite does not yet have an XMPP client installed and configured.

If the server provides a `landing-url` in the response, the client SHOULD share this URL with contacts. Otherwise it SHOULD use the URI in combination with a landing page (which may be hosted by the client developer or other entity) to generate a `https://` URL suitable for sharing. An example landing page can be found at [ge0rg/easy-xmpp-invitation](https://github.com/ge0rg/easy-xmpp-invitation).

Sharing the URL can be done by visually displaying a QR code on the user's screen (if the contact is in physical proximity) or e.g. through the platform's own sharing mechanism (to share via SMS, email, social apps, etc.)

## Guidance for landing pages

As well as embedding the XMPP URI in a visually obvious clickable/tappable element (e.g. a button), it should include text and download links for compatible XMPP clients.

If it is possible for a particular platform's download links to automatically relay the `xmpp:` URI to the installed app, that should be implemented. See for example [Google Play Install Referrer](https://developer.android.com/google/play/installreferrer/).

If possible, platform detection should be used to highlight download links relevant to the user's current platform.

If the detected platform is a desktop environment, consider also adding a QR code for easy transmission to a user's mobile device.