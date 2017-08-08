(A) Messaging
=============

The messaging application needs to satisfy a number of feature
requirements to be implemented.  These have to be enacted via a client
side application (the Web-based chat client as part of the mega.nz
site) under support of the required cryptographic components (B) and
the chat server infrastructure (C).


Chat Client
-----------

A number of "user stories" outline the feature requirements
implemented by the chat client and its user experience (UX).  Some
technicalities may be added in square brackets.

User Stories for 1-on-1 chats:

* Alice can conduct a text chat with Bob confidentially.

* Alice can retrieve a chat history of her chat with Bob.
  [Chat history is to be stored on the server.]

* Alice can start a chat with Bob directly in the contact list (along
  with the view of incoming shares and contact info).  Depending on
  interface design it may be considered to view the most recent
  message(s) already in the contact view, which can be maximised to
  full screen.

* Alice can choose chat partners from contacts via their screen names
  (default will be the name entered during signup).

* Alice can see recent chats across multiple devices, with the most
  recently (active) on top.

* Alice sees a new message received indicator across all clients
  logged into that account. Once a message or multiple messages are
  being read on one client, they are being marked as read on all other
  clients.

* Messages are being marked as read by putting focus on the specific
  chat session while they are visible.

* Alice can configure the chat to notify on all incoming messages when
  the webclient is open in the background.

* Alice can edit or delete a previously sent message.  (Up until a
  certain age only.)

* Alice can send emoticons or insert manual line breaks into a
  message.

* Alice will be notified of another chat participant typing.

* Alice can paste text into chat messages.

* Alice can send files or folders from own cloud drive to a chat
  partner. Sharing is independent of the chat (just initiated through
  it) and will persist as an incoming share for the recipient.

* Alice sends one or multiple messages that are not read within X
  minutes, the message(s) go through a notification routine, which
  will for example (configurable by the user):

  * Send an email (without the message, obviously)

  * Send a push notification to all mobile apps

  * In the future, browsers could be woken up too,
    e.g. https://wiki.mozilla.org/WebAPI/SimplePush


User stories for chat history:

* Alice can disable chat logging for chats with Bob (for offline
  messages the message will not be stored beyond delivery, but still
  stored for forwarding once the recipient comes online).

* Recent chats will initially always only show the most recent chats
  (e. g. 50).

* Chat messages will be stored individually on the chat server.

* Full history for each chat is available, loaded dynamically by
  scrolling up (alternatively initially a "load more" button to work
  on the auto scroll-loading). Search is performed on the client side
  and requires the history to be searched to be loaded from the
  server.


User stories for group chats:

* When Alice adds a third user to an existing 1-on-1 session, a new
  group chat is automatically created for the group of three.

* When Alice adds a Charly to a group chat, Charly will be asked to
  join the existing group chat.  (The previous chat history is not
  available to Charly.)

* (All) previous group chat users can agree to give Charly (the new
  member) access to previous chat messages.

* Group chat sessions (are more transient) and will move down in the
  recent list once inactive, and eventually disappear.


User stories for retention policies:

* Retention policies are not enforceable, but they will be executed
  nonetheless by the server storing the chat history.  The
  configuration option should be limited by the system to a sensible
  range of values.  Pro accounts may be allowed for longer periods as
  an upgrade incentive.

* Once a chat retention policy has cleared all data of a recent chat,
  it will not be displayed on the list of recent chats.

* Each user can configure their global retention policy.

* The per chat retention policy is displayed somewhere in a chat, and
  can be changed for that specific chat.


Message Encoding
----------------

Messages are encoded for transport.  Every message is composed of a
message envelope, and (encrypted) content.  We are distinguishing
between chat and management messages.

* Message envelope: Encoded as TLV data (Tag, Length, Value),
  specifying the message protocol version used, the message signature
  as well as the payload.

* Message content: (Encrypted) content of the message, Base64 encoded.

* Message payload: Available after decryption.  JSON encoded content,
  containing some meta-data along with chat message and/or management
  information.

The message envelope is to be implemented in a manner similar to the
one already for the storage of private user attributes: Containing an
identifier for the encryption scheme, a message signature, nonce and
ciphertext.
  
Chat message payloads contain the actual message along with additional
meta-data, such as a message ID (that needs to be unique, e. g. when
in combination with the sender and a chat session ID), a time stamp.
Message contents can be one of the following: text content, file tree,
inline image or potentially third party embeddings (if allowed by CSP
of third party services like YouTube).  If a previous message is to be
edited/deleted, an optional meta-data field contains a unique
reference of the message to be overlaid by the replacement message.

A chat client will put the messages into an ordered representation for
a chat.  For assistance a time stamps, message ID and order of
receiving can be used.  Due to clock skew on different clients this
may introduce inaccuracies.

Management message payloads contain information that a chat client may
need to exchange with other clients to ensure the overall
functionality.  Such messages are generally not to be displayed by a
chat client and therefore do not trigger any new message notifications
or read notifications.


..
    Local Variables:
    mode: rst
    ispell-local-dictionary: "en_GB-ise"
    mode: flyspell
    End:
