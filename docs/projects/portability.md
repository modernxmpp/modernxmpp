# XMPP Account Portability

The _XMPP Account Portability project_ is standardizing a way to migrate a
user’s account data from one XMPP-based service provider or software to
another. The project will develop and publish a suitable protocol and data
format via the [XMPP Standards Foundation](https://xmpp.org/)’s standards
process, as well as a reference implementation. Finally, the work will be
integrated into [Snikket](https://snikket.org/), a suite of XMPP-based
open-source communication software.

This project was officially completed in January 2022. The results of the
project are all open-source and publicly available, now living on in their
various places:

- **Standards:** [XEP-0227: Portable Import/Export Format for XMPP-IM Servers](https://xmpp.org/extensions/xep-0227.html), [XEP-0283: Moved](https://xmpp.org/extensions/xep-0283.html)
- **Snikket:** The [January 2022 Snikket server release](https://snikket.org/blog/jan-2022-server-release/)
    added account import and export functionality.
- **Prosody:** The work resulted in creating/updating several modules: [mod_storage_xep0227](https://prosody.im/doc/modules/mod_storage_xep0227),
    [mod_http_xep227](https://modules.prosody.im/mod_http_xep227), [mod_auto_moved](https://modules.prosody.im/mod_auto_moved).
- **Web-based account migrator:** https://migrate.modernxmpp.org/ ([source](https://github.com/snikket-im/xmpp-account-exporter))

A detailed report of the project results, as submitted to DAPSI (who funded the project), is available as a PDF: [XPORTA Project Final Evaluation.pdf (75KB)](/files/XPORTA%20Project%20Final%20Evaluation.pdf)

**Timeline**

- **April 2021:** Read the project announcement on the [Snikket blog](https://snikket.org/blog/dapsi-fund-account-portability/)!
- **May 2021:** Research and document drafting.
- **June 2021:** XEP-0227 revision 1.1 [has been submitted](https://github.com/xsf/xeps/pull/1064) to the XSF. A new proto-XEP "Moved 2.0" [has also been submitted](https://xmpp.org/extensions/inbox/moved2.html). Both submissions are awaiting approval from the [XSF technical council](https://xmpp.org/about/xmpp-standards-foundation.html#council).
- **July 2021:** A beta web-based [XMPP account migrator](https://migrate.modernxmpp.org/) is now online!
- **August 2021:** Initial implementation in Prosody, as [mod_storage_xep0227](https://prosody.im/doc/modules/mod_storage_xep0227) and [mod_auto_moved](https://modules.prosody.im/mod_auto_moved).
- **September 2021:** Implementation work continues, meanwhile the XSF approved and published the updated version (1.1) of XEP-0227. Also ejabberd, another popular server implementation, [gains support for the new XEP-0227 features](https://github.com/processone/ejabberd/issues/3676).
- **October 2021:** The project is evaluated by the DAPSI team, and approved to continue to the second phase! Work on implementation and testing in Prosody continues.
- **Nov/Dec 2021:** Implementation in Snikket begins, including a friendly user interface to download and import account data.
- **January 2022:** Finish implementation and submit documentation for final evaluation by DAPSI.

<div style="display:flex; flex-direction: column;">
  <div>
    <h2>Credits</h2>
    <p>
      This project has received funding from the European Union's
      H2020 research and innovation programme under Grant Agreement
      no 871498
    </p>
  </div>
  <div style="display:flex; flex-direction:row;">
    <a href="https://www.ngi.eu/"><img src="/img/Logo-NGI_Explicit-with-baseline-rgb.png" alt="NGI Logo (Next Generation Internet: Internet of Humans)" style="border:none"></a>
    <a href="https://www.ngi.eu/"><img src="/img/NGI_DAPSI_Tag-color-positive.png" alt="NGI DAPSI Logo" style="border:none"></a>
    <a href="https://europa.eu/"><img src="/img/EU%20emblem.jpg" alt="EU emblem" style="border:none"></a>
  </div>
</div>
