# Protected Auction Services WICG Calls: Agenda & Notes

Calls take place on some Wednesdays, at noon New York = 9am California. Please
check
[https://github.com/WICG/protected-auction-services-discussion/issues/27][1] for
details.

That's 6pm Paris time and 4pm UTC (until the end of summer, when countries
fiddle with their clocks).

Notes repository:
[https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings][2]

(This notes doc will be editable by everyone, during the meeting)

**Next meeting: 14 Aug 2024**

Google Meet joining info

Video call link: [https://meet.google.com/htk-obgg-smb][3]

Or dial: ‪(US) +1 509-676-3166‬ PIN: ‪117 463 428‬#

More phone numbers: [https://tel.meet/htk-obgg-smb?pin=4553130257370][4]

_To join the speaker queue_:

_Please use the "Raise My Hand" feature in Google Meet_.

## Attendees:

1. (ID Privacy)
1. Itay Sharfi (Google Privacy Sandbox)
1. Agustin Recouso (Nextroll)
1. Trenton Starkey (Google Privacy Sandbox)
1. Isaac Foster (MSFT Ads)
1. Yashaswini Kumar (Google Privacy Sandbox)
1. Martin Pal (Google Privacy Sandbox)
1. Matthew Atkinson (Samsung)
1. Viacheslav Levshukov (Microsoft)
1. Peter Meric (Google Privacy Sandbox)
1. Laura Morinigo (Samsung)
1. Brian Schneider (Google Privacy Sandbox)
1. Shruti Agarwal (Google Privacy Sandbox)
1. Vincent Minet (Criteo)
1. Kevin Naughton (Google Privacy Sandbox)
1.

## Agenda

### Suggest agenda items here:

Isaac:

- [Roma gVisor + KV Lookups: How ~Will~ Might Local KV Lookups Happen from an
  IPC Perspective, Possible Usage of Mapped Memory][5]

**Note taker**: Yashaswini Kumar

### Notes

[Roma gVisor + KV Lookups: How ~Will~ Might Local KV Lookups Happen from an IPC
Perspective, Possible Usage of Mapped Memory][5]

- [Itay] gVisor is being renamed to BYOB
- [Isaac] Explanation of ask:
    - What is gVisor currently doing for the structure of processes etc. How does a
    getValues call get handled from a process comms perspective? Will it be
    similar to IPC model?
  - Also, with advanced configuration, can we do optimizations with lookup
    times?
- [Brian] All the functionality that exists in the KV server:
    - Inline datastructures: Criteo has a bug opened up asking about it. Can array
    buffers be used as a mechanism?
  - Support for mmaps in v8 of KV server
- [Isaac] Looks like it would be declared in a file today?
  - [Peter] Current setup: Lets assume we mmap the file. On the v8 side, the
    mmap file is made available in the memory region. You can use arraybuffer.
    You can read it via javascript. Example code will be available. 10M
    key/value structures
- The adTech can provide a bunch of files that can get mmapped.
- New row: Mmapped blob?
  - Gets mapped to UDF
- Couldn't we in theory say that the AdTech can specify the writer code?
  - possibly a riegli record: "JS_variable_name".+ "blob"?
- Concern: Continuing to do business data syncing that we do today
  - How will you manage updates to the blob (several GB) even if we want to
    modify a small part? Is there an efficient way to do so
- Writing of business object vs writing at request time
-

### Chat log

Itay Sharfi

12:03 PM

[https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8_EbPnzcptnhV9mxBP5Mo/edit#heading=h.5xmqy05su18g][6]

Peter Meric

12:03 PM

I can talk to Roma BYOB too

but I'm on a train pulling into NYC soon, and the wifi tends to cut out in the
tunnels

Peter Meric

12:05 PM

BTW, gVisor is an implementation detail of Roma BYOB, and thus gVisor something
that _could_ change

David's Notetaker

12:07 PM

Hi, I'm an AI assistant helping David Tam take notes for this meeting. Follow
along the transcript here:
[https://otter.ai/u/bwk5tO5ru--DZm5_khVSSaHrUEw?utm_source=va_chat_link_1][7]

You'll also be able to see screenshots of key moments, add highlights, comments,
or action items to anything being said, and get an automatic summary after the
meeting.

Peter Meric

12:10 PM

want to get the CLs out today, it was held up on the ARM64 build

Peter Meric

12:17 PM

possibly a riegli record: "JS_variable_name".+ "blob"

David's Notetaker

12:19 PM

Hi, I'm an AI assistant helping David Tam take notes for this meeting. Follow
along the transcript here:
[https://otter.ai/u/bwk5tO5ru--DZm5_khVSSaHrUEw?utm_source=va_chat_link_2][8]

You'll also be able to see screenshots of key moments, add highlights, comments,
or action items to anything being said, and get an automatic summary after the
meeting.

Peter Meric

12:21 PM

I think we agree with Isaac

can we remove David's Notetaker?

I removed David's Notetaker from the meeting

Arthur Coleman

12:23 PM

well ok - I can find info about gVisor - but what is ROMA = ROMAS (Runtime
Object Management and Security)? - and what does BYOB stand for. There is a
github repository named that = but probably not related?

Peter Meric

12:24 PM

there's some preliminary info on Roma BYOB available here:

[https://github.com/privacysandbox/data-plane-shared-libraries/tree/main/docs/roma/byob/sdk/docs][9]

these docs say nothing much about gVisor, as they're written for the UDF
developer

Arthur Coleman

12:24 PM

thank you

Shruti Agarwal

12:24 PM

BYOB stands for Bring Your Own Binary.

[1]: https://github.com/WICG/protected-auction-services-discussion/issues/27
[2]: https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings
[3]: https://meet.google.com/htk-obgg-smb
[4]: https://tel.meet/htk-obgg-smb?pin=4553130257370
[5]: https://github.com/WICG/protected-auction-services-discussion/issues/83
[6]: https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8_EbPnzcptnhV9mxBP5Mo/edit#heading=h.5xmqy05su18g
[7]: https://otter.ai/u/bwk5tO5ru--DZm5_khVSSaHrUEw?utm_source=va_chat_link_1
[8]: https://otter.ai/u/bwk5tO5ru--DZm5_khVSSaHrUEw?utm_source=va_chat_link_2
[9]: https://github.com/privacysandbox/data-plane-shared-libraries/tree/main/docs/roma/byob/sdk/docs

