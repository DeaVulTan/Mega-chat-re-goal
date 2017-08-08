High Level Product Goals
========================

An easy to use, secure text chat with the normal features that a
normal user would expect, but with additional MEGA user controlled
privacy.  These include: message privacy, multiple devices, typing
progress, secure chat history, offline delivery and read
notifications.  More advanced privacy features will be made available
in the future using the full mpENC encryption ("whisper" mode) scheme.
It is to be determined whether it will supersede this initial
encryption scheme, or be an optional enhancement.

This is acknowledged as a refinement of the previous goals of the
company.  By relaxing some cryptography and privacy attributes, a
focus can be made more clearly on the user experience.  As such this
document describes an alternative architecture to achieve this goal
quickly and cost effectively.


User Experience Comes First
---------------------------

Users want "simplicity first" -- their primary aim is to communicate.
And with MEGAchat, they will be able to communicate securely. This
will be the default state.

For users that require a higher level of privacy, in the future an
optional mode of operation will be provided so the user will
explicitly know what state they are choosing, and the relevant
trade-offs that will take place due to their decision.

From a UX perspective, this is expected to be initially simpler and
more user friendly, while catering for the hard-core cryptographers
and privacy zealots in the future.


Product Components
------------------

The product under construction in this project will consist of three
distinctly complementary components:

A:
   Messaging (application and message payload)

B:
   Cryptography (chat message protection and authentication)

C:
   Chat Infrastructure (server side and wire protocols)

Each of these components deals with orthogonal concerns, however this
does not mean that there are no dependencies between them.


..
    Local Variables:
    mode: rst
    ispell-local-dictionary: "en_GB-ise"
    mode: flyspell
    End:
