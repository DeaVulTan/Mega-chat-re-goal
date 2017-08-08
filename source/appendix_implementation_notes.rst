Implementation Notes
====================

Notifications
-------------

There are different notification systems available, which serve
different purposes.  They may work together to "escalate"
notifications, though.

* Incoming message marker(s) in UI

* Desktop notifications issued by the browser (needs approval from the
  user to allow such notifications to the system). These result in
  short lived pop up windows and a sound to be played.

* "External notifications", e. g. email, push notifications, etc.

Message markers are directly implemented in the UI of the chat client.
Desktop notifications are already in use and are using specific
browser features.  For external notifications additional support is
needed.  In the case of the chat, mostly such notifications can be
need to be triggered by chatd (for offline messages), and can trigger
sending out such notifications (e. g. an email on offline messages not
read).


Implementation Support
----------------------

The following issues probably need some implementation support
*outside* the scope of the messaging client (A), cryptography (B) and
chat server infrastructure (C).

API
^^^

* Support for screen names of contacts in contact list. [Redmine
  ticket #359.]
* Support for sending files or folders from own cloud drive [Redmine
  ticket #357: previously rejected out of frustration.]
 

General Web Client
^^^^^^^^^^^^^^^^^^

* Additional configurable user settings.



..
    Local Variables:
    mode: rst
    ispell-local-dictionary: "en_GB-ise"
    mode: flyspell
    End:
