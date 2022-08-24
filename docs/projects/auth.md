# Modern Authentication and Authorization in XMPP

This project will bring the authentication and authorization layers of XMPP
up to date with current best practices for user account security. Although
many users are familiar with using passwords to access online services, they
have repeatedly proven to be a weak point in the security of a user's account.
On the web, multiple factors, the recent FIDO/WebAuthn standards and the
well-established OAuth2/OIDC protocols are being used to shore up defences
against phishing and unauthorized account access.

Meanwhile, single-factor password authentication unforunately remains the only
widely-available option for signing into XMPP accounts. Most XMPP services and
clients do not support requiring multiple factors to access an account.
Neither do they support securely granting access to your account to a third
party (e.g. a hosted web client, such as Movim) without exposing your
password, nor selectively revoking access if a device is lost, stolen or
compromised.

Over the coming months, this project will deliver:

- Support for multi-factor authentication in a widely-deployed XMPP server (Prosody)
- Mechanisms to make multi-factor authentication practical on non-persistent connections (i.e. securely reidentify a previously-authenticated device)
- A way for users to securely grant restricted and/or temporary account access to a third party (such as a web client) without exposing their password
- The ability for a user to view and manage what clients/entities currently have access to their account
- A mechanism through which the user can revoke access to their account for a client/entity

These achievements will be realized through implementation of existing standards
(such as [XEP-0388: Extensible SASL Profile](https://xmpp.org/extensions/xep-0388.html))
in Prosody, and by development and publication of new standards where
necessary. This project does not directly cover the client-side
implementations, but client developers in the community will be engaged and
encouraged to explore the new extensions at appropriate points in the project.

**Updates**

- **June 2022:** The project is just getting started! The primary source for updates will be [Prosody's blog](https://blog.prosody.im/modern-xmpp-auth/).
- **August 2022:** The first milestone has been completed - support for per-session [roles and dynamic permissions in Prosody](https://blog.prosody.im/role-auth/)..

<div style="display:flex; flex-direction: column;">
  <div>
    <h2>Credits</h2>
    <p>This project was funded through the NGI Assure Fund, a fund established
       by NLnet with financial support from the European Commission's Next
       Generation Internet programme, under the aegis of DG Communications
       Networks, Content and Technology under grant agreement No 957073.
    </p>
  </div>
  <div style="display:flex; flex-direction:row;">
    <a href="https://nlnet.nl/"><img src="/img/NLnet-foundation-logo.svg" alt="NLnet Foundation logo" style="border:none; height:5em;padding: 0.75em;"></a>
    <a href="https://nlnet.nl/assure/"><img src="/img/NGIAssure_tag.svg" alt="NGI Assure Logo" style="border:none;height: 5em;padding:0.75em;"></a>
    <a href="https://www.ngi.eu/"><img src="/img/Logo-NGI_Explicit-with-baseline-rgb.png" alt="NGI Logo (Next Generation Internet: Internet of Humans)" style="border:none;height: 5em; padding: 0.75em;"></a>
    <a href="https://europa.eu/"><img src="/img/EU%20emblem.jpg" alt="EU emblem" style="border:none;height:5em; padding: 0.75em;"></a>
  </div>
</div>
