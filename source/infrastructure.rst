(C) Chat Infrastructure
=======================

To enable the chat, a hybrid system consisting of XMPP servers and
"chatd" servers are used.  The XMPP servers' purpose is to allow for
presence and typing notifications, as well as enabling signalling for
the voice and video calls via the XMPP/Jingle protocol.  Chatd is an
additional custom Mega-designed and built chat server system that
allows for message storage and forwarding as well as managing
individual chats and chat rooms (for group chats).

XMPP services are in place and operational (though subject to
continuous improvement).  The specifications of "chatd" are not part
of this particular document, but are contained in Mathias Ortmann's
specific design document.


..
    Local Variables:
    mode: rst
    ispell-local-dictionary: "en_GB-ise"
    mode: flyspell
    End:
