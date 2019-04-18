# Translation discussion

Most XMPP clients are distributed in multiple languages. In the process of translating a client, people with various backgrounds (not necessarily XMPP-related) are contributing translations.

The following tables are gathering the various translations of key terms in (a limited set of) clients to give an overview about what is currently used. This document intends to serve as a basis to discuss recommendations for key term translations.


**Translation services used by clients**

Client        | Service
--------------|-------------------------------------------------------------------
Conversations | [Transifex](https://www.transifex.com/siacs/conversations/)
converse.js   | [Weblate](https://hosted.weblate.org/projects/conversejs/)
Dino          | [Weblate](https://hosted.weblate.org/projects/dino/)
Gajim         | [Pootle](https://translate.gajim.org/)
PSI(+)        | [Transifex](https://www.transifex.com/tehnick/psi-plus/)
Swift         | [swift.im git](https://swift.im/git/swift/tree/Swift/Translations)
yax.im        | ?


## German

### Terms currently used in clients

| Term \ Client        | Conversations                 | Converse.js                   | Dino                   | Gajim[^gajim-MR]          | PSI(+)                       | Swift.im            | yax.im |
|----------------------|-------------------------------|-------------------------------|------------------------|---------------------------|------------------------------|---------------------|--------|
| XMPP address         | XMPP-Adresse                  | XMPP-Adresse                  | JID                    | XMPP-Adresse              | JID                          | JID, Jabber-ID      |        |
| contact list         | Kontaktliste                  | Kontakte                      | Kontaktliste           | Kontaktliste              | Kontaktliste                 | Kontaktliste        |        |
| bookmarks            | Lesezeichen                   | Lesezeichen                   | -                      | Gespeicherte Gruppenchats | Lesezeichen                  | Lesezeichen         |        |
| auto join            | Auto-Join-Funktion            | automatisch beitreten         | -                      | automatisch beitreten     | automatisch beitreten        | -                   |        |
| channel              | Channel                       | Gruppenchat, Raum             | Kanal/Konferenz        | Gruppenchat               | Gruppenchat, Chatraum        | Chatraum            |        |
| group chat           | Gruppenchat                   | Gruppenchat                   | Raum                   | Gruppenchat               | Gruppenchat, Chatraum        | Chatraum            |        |
| role                 | ?                             | Rechte, Rolle                 | -                      | Rolle                     | Rolle, Funktion              | Rolle               |        |
| moderator            | Moderator                     | Moderator                     | -                      | Moderator                 | Moderator                    | Moderator           |        |
| participant          | Teilnehmer                    | Teilnehmer                    | members ?              | Teilnehmer                | Teilnehmer                   | Teilnehmer          |        |
| kick                 | ausschließen?                 | hinauswerfen                  | hinauswerfen           | rauswerfen                | rauswerfen                   | rausschmeißen       |        |
| ban                  | ausschließen?                 | entfernen                     | -                      | sperren                   | verbannen                    | verbannen           |        |
| affiliation          | Rechte?                       | Zugehörigkeit                 | -                      | Gruppenzugehörigkeit      | Mitgliedschaft, Angliederung | Zugehörigkeit       |        |
| owner                | Eigentümer                    | Eigentümer                    | Eigentümer             | Besitzer                  | Besitzer                     | Besitzer            |        |
| admin                | Administrator                 | Admin                         | Administrator          | Administrator             | Administrator                | Administrator       |        |
| member               | Mitglied                      | Mitglied                      | Mitglied               | Mitglied                  | Mitglied                     | Mitglied            |        |
| user                 | -                             | Besucher                      | Gast                   | -                         | -                            | -                   |        |
| nickname             | Nickname                      | Spitzname, Nickname           | Spitzname              | Spitzname                 | Spitzname                    | Spitzname, Nickname |        |
| history              | Verlauf                       | -                             | Gesprächsverlauf       | Unterhaltungsverlauf      | Nachrichtenchronik           | Verlauf             |        |
| fingerprint          | Fingerabdruck                 | Fingerabdruck                 | Fingerabdruck          | Fingerabdruck             | Fingerabdruck                | -                   |        |
| subscription request | Online-Status anfragen        | Kontaktanfrage[^sub-converse] | Kontaktanfrage         | Kontaktanfrage            | Anfrage                      | Anfrage             |        |
| subscription         | Online-Status                 | Anwesenheitsabonnement        | -                      | Abonnement                | Abonnement                   | Abonnement          |        |
| chat                 | Unterhaltung                  | Chat                          | Unterhaltung           | Chat                      | Chat                         | Chat                |        |
| read receipts        | Lese- und Empfangsbestätigung | -                             | Lesebestätigungen      | Empfangsbestätigungen     | Übermittlungsbestätigung     | Empfangsbestätigung |        |
| typing notifications | Tipp-Benachrichtigung         | -                             | Tippbenachrichtigungen | Chatstatus                | Tipp-Benachrichtigung        | -                   |        |
| avatar               | Avatar                        | Avatarbild                    | -                      | Kontaktbild               | Avatar                       | Bild                |        |

### Recommended translation

term         | translation
-------------|------------
XMPP address |
contact list |
bookmarks    |
auto join    |
...          |


## French

### Notes for french translations (from pep.)

English      | French
-------------|-----------------------
group chat   | groupe (de discussion)
channel      | salon (de discussion)
participant  | participant
XMPP address | Adresse XMPP
contact list | Liste de contact


<!-- Footnotes -->

[^gajim-MR]: Refers to current master and [this merge request](https://dev.gajim.org/gajim/gajim/merge_requests/384)
[^sub-converse]: Subscription requests in converse.js are called contact requests
