# Protected Auction Services WICG Calls: Agenda & Notes

Calls take place on some Wednesdays, at noon New York = 9am California. Please
check
[https://github.com/WICG/protected-auction-services-discussion/issues/27][1] for
details.

That's 5pm Paris time and 4pm UTC (until the end of March, when EU countries
fiddle with their clocks).

Notes repository:
[https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings][2]

(This notes doc will be editable by everyone, during the meeting)

**Next meeting: 3rd July 2024**

Google Meet joining info

Video call link: [https://meet.google.com/htk-obgg-smb][3]

Or dial: ‪(US) +1 509-676-3166‬ PIN: ‪117 463 428‬#

More phone numbers: [https://tel.meet/htk-obgg-smb?pin=4553130257370][4]

_To join the speaker queue_:

_Please use the "Raise My Hand" feature in Google Meet_.

## Attendees:

1. Akshay Pundle (Google Privacy Sandbox)
1. Alexander Tretyakov (Google Privacy Sandbox)
1. Brian May (Dstillery)
1. Agustin Recouso (NextRoll)
1. Andres Bordese (NextRoll)
1. Felipe Gutierrez (Microsoft Ads)
1. Peter Meric (Google Privacy Sandbox)
1. Matt Davies (Bidswitch | Criteo)
1. Abishai Gray (Google Privacy Sandbox)
1. Daniel Kocoj (Google Privacy Sandbox)
1. Suresh Chahal (Microsoft Ads)
1. Isaac Foster (MSFT Ads)
1. Matthew Atkinson (Samsung)
1. Josh Singh (Microsoft Ads)
1. Samantha Jung (Google Privacy Sandbox)
1. Vincent Minet (Criteo)
1. Robert Kubis (Google Privacy Sandbox)
1. Aditi Page (Google Privacy Sandbox)
1. Laura Morinigo (Samsung)

## Agenda

### Suggest agenda items here:

- Alexander Tretyakov (Google Privacy Sandbox)
    - Hybrid protocol – modify v2 protocol so that a single request can go to both
    BYOS and TKV servers. This is meant to be a temporary measure, and when the
    enforcement starts only TKV mode will be supported. The benefits of the
    hybrid protocol are:
      - enables piecemeal migration. AdTechs can migrate pieces of their logic and
      asses the cost/latency and other parameters before fully committing
    - allows keeping parts of the logic that are not currently supported by TKV
      in BYOS, while moving the rest to TKV.

### Notes

Note taker: Akshay Pundle

- Alex: Will send link to presentation after
  - 2 different modalities how kv can be used:
  - BYOS - run on your on server, no privacy guarantee
  - TEE-KV - runs in TEE, that's where we want to get
  - How do you get from byos to tee-kv, what is the migration path?
- Proposal: introduce hybrid. Start with byos, add tee-kv
  - Encrypted + plain text payload.
  - Encrypted visible only on tee-kv
  - Current byos acts as orchestration + lookup, can see plaintext only
  - Encrypted can be sent to TEE kv, and response is encrypted back as well
  - Additional signals will be encrypted, only accessible on tee-kv
- IssacF: In future we want extra signals, will they be on tee-kv only?
  - Alex: yeah- extra signals will be available only on tee kv
- Brian May: Will it be synchronous? How will it handle timeouts?
  - Alex: yup
  - Brian May: For example, what if tee-kv times out, and i still want to
    respond with byos
  - Alex: yeah, byos can still return it's result based on plaintext
  - Brian: What about failed updates?
  - Alex: there are no updates in tee-kv, it is read only
- Alex: This will be temp support
  - When tee-kv, then byos will be deprecated
  - Downside: latency and cost
  - Cost: New server, more money
  - Adding extra latency .. same rack / vpc can be quick
  - Really optional setup, not mandatory
- Itay:
  - Value 1: You can combine tee-kv and byos, incremental migration
  - Value 2: Enables extra signals on the buyer side (page url and couple of
    other things).
  - Value 3: Integration between 2 servers, the tee kv can be a different
    provider (e.g. branch safety etc.)
- Brian may:
  - Can see useful for some set, but not all
  - Folks might not want to deal with this, and call tee directly (2 calls from
    device)?
- Alex:
  - Probably yes, only byos, only tvk or both
- Itay:
  - Looking into debugging and monitoring
- Yanush:
  - Plaintext, will it have all the current signals?
  - Itay: yup
  - Alex:
- Itay:
  - One debate: level of use and need. We are wondering if there is interest in
    using this?
  - BrianM: very helpful tool for transition, we would likely use this for
    transitioning
- Issac:
  - Extremely interesting to see flexible design, useful to see this as a tool.
- Yanush
  - What scenario is being covered here? Contextual signals in plaintext, and
    extra signal encrypted?
  - Alex: Yup, extra stuff that we add is encrypted
    - BrianS: You get all the data that you normally get to byos, compute what you
    normally compute, and you have additional data, that can be viewed on the
    tee-kv, use that to modify, and return the final response.
- Issac:
    - Not being able to send request downstream? With ability to shard kv server …

  - Multiple types of data into kv server, is it strictly for b&a or is it
    on-device also?
    - Alex: this is for both on device and b&a
    - Itay: on kv side, features on kv on-device and b&a should be same
  - Interesting question: b&a announcing additional flexibility in how kv calls
    get routed.
- Itay: OK, seems overall positive. Extra signal to kv will be nice value prop.
  - Please ping us is you want to try it out.
- Viacheslav "Slava" Levshukov
  - When do you expect protected-auction-key-value-service will be available to
    test in TEE?
  - Alex: 2nd week of july
  - Integration with chrome: jan 2025

### Chat log

Alexander Tretyakov

9:02 AM

Am I the only one who couldn't here Akshay when he was talking?

Matt Davies

9:02 AM

can you post the meeting notes link to sign in?

please

Alexander Tretyakov

9:02 AM

https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8_EbPnzcptnhV9mxBP5Mo/edit

Andres Bordese

9:20 AM

Agreed. Looks really useful for the migration.

Viacheslav "Slava" Levshukov

9:27 AM

When do you expect protected-auction-key-value-service will be available to test
in TEE?

[1]: https://github.com/WICG/protected-auction-services-discussion/issues/27
[2]: https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings
[3]: https://meet.google.com/htk-obgg-smb
[4]: https://tel.meet/htk-obgg-smb?pin=4553130257370

