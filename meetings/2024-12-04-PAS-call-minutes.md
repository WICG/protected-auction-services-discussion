# Protected Auction Services WICG Calls: Agenda & Notes

Calls take place on some Wednesdays, at noon New York = 9am California. Please
check
[https://github.com/WICG/protected-auction-services-discussion/issues/27][1]{:.external}
for details.

That's 6pm Paris time and 4pm UTC (until the end of summer, when countries
fiddle with their clocks).

Notes repository:
[https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings][2]{:.external}

(This notes doc will be editable by everyone, during the meeting)

**Next meeting: Dec 4, 2024**

Google Meet joining info

Video call link: [https://meet.google.com/htk-obgg-smb][3]{:.external}

Or dial: ‪(US) +1 509-676-3166‬ PIN: ‪117 463 428‬#

More phone numbers:
[https://tel.meet/htk-obgg-smb?pin=4553130257370][4]{:.external}

_To join the speaker queue_:

_Please use the "Raise My Hand" feature in Google Meet_.

## Attendees:

1. David Roundy (NextRoll)
1. Brian May (Unaffiliated)
1. Joshua Prismon (Index Exostchange)
1. Yashaswini Kumar (Google / Privacy Sandbox)
1. Arthur Coleman(ThinkMedium)
1. Matt Kendall (Index Exchange)
1. Abishai Gray (Google Privacy Sandbox)
1. Fabian Höring (Criteo)
1. Peter Meric (Google Privacy Sandbox)
1. Yanush Piskevich(Microsoft Ads)
1. Suresh Chahal (MSFT)
1. Mihir Gandhi (Google Privacy Sandbox)
1. Ashish Bhardwaj ( Google Privacy Sandbox)
1. Isaac Foster (MSFT Ads)
1. Xing Gao(Google Privacy Sandbox)
1. Peiwen Hu (Google Privacy Sandbox)
1. Michael Mihn-Jong Lee (Google Privacy Sandbox)
1. Joy Adeyemo (Google Privacy Sandbox)
1. Martin Pál (Google Privacy Sandbox)
1. Akshay Pundle (Google Privacy Sandbox)
1.

## Agenda

- Fabian Höring to present
  [https://github.com/WICG/privacy-preserving-ads/blob/main/Open%20Discussions/20240924-WICG_TPAC_Criteo_OnDeviceVsServerSide.pdf][5]

  -
    [https://github.com/privacysandbox/bidding-auction-servers/issues/23][6]

**Note taker**:

### Notes

_Fabian will upload the slides to the repo later_

- ROMA: execution engine allows execution of JS code without logging/tracking
- K/V service deployed in Criteo's environment
- Executed Web load tests
- [Brian S.] Any tests where UDF does more than just proxying to the data store?

  - [Fabian] We plan to do this next, happy to share the results later
- [Fabian] Internal benchmarks with interprocess communication → not good enough
  to share at this time.
  - Do you make RPC for each data request?
    - No, Optimized
  - Need to follow-up
- [Isaac F] Re: IPC where you are seeing 5x increase. Brian S and Isaac have
  been discussing shared memory
  - [Fabian] Not using shared memory. We are also using ML workload
  - [Isaac] Expecting this is the reason for 5x increase
- [Akshay P] Can you give some more details about how you arrived at the 5x
  number for ML
    - [Fabian] More work is required here, but expect to still see increase due to
    IPC
  - [Akshay P] This overhead will depend on the ML models / workload, what kind
    of workload is it?
  - [Akshay P] Need to follow-up on this in the future
- [Brian S] Re: Inlines data structures. The suggested workaround is what you
  can do today. Side effects of large JS files; we are working on improving it
  without sacrificing functionality
  - [Fabian] Will try to make this more efficient with shared memory as well
- [Peter]
  - [Fabian] Used 16 cores and incrementally increased qps to get to a failure
    point
  - [Peter] Fabian will update the "In memory caching" slide. It is 4.2K QPS,
    not 4.2
- [Mihir] Can some of the benchmarking scripts be shared?
    - [Fabian] Not using real B&A scripts. Just dummy scripts. Will use obfuscated
    production script later
    - [Fabian] Test depends on the methodology. If there is consensus on using the
    methodology, Fabian can share the scripts. It will take some work to make
    this available
  - [Peiwen] What are the key aspects of the methodology you want to keep?
    - [Fabian] Prefer using what we have now.
    - [Peiwen] Which ones (micro benchmarks) do we want to prioritize and for
      which server?
      - Critero's tests have a particular use case touching upon both K/V and
        B&A.
      - [Fabian] A/B testing On-Device testing vs B/A to see if we are going to be
      profitable.
    - [Peiwen] Propose we start a draft on the methodology without proprietary
      B&A scripts.
    - Benchmarking with a dummy workload: Suggest that we focus on raw values
      than percentages
      - [Fabian] Need to compare across different platforms / machine
        configurations as well.
    - [Peiwen] Can Fabian start a GitHub issue noting the constraints and
      expectations?
- [Peter] Re: Shared cache. We put in a micro benchmarking for reading & binary
  search on a large structure (flatbuffer) memory-mapped into V8 (but not Roma
  V8). Just as an experiment, memory mapping. No need to deserialize flatbuffer.
  You can run these benchmarks in the data-plane-shared-libraries repo using
  this command:

`builders/tools/bazel-debian run
//src/roma/sandbox/js_engine/v8_engine:arraybuffer_benchmark --
--benchmark_time_unit=us`

- [Fabian] Looks interesting. Will explore. But also, need to compare against
  benchmark from before.
  - [Peter] Looks like we need more of a real world benchmarking
  - [Fabian] Would like to head from other AdTechs on this
-

[1]: https://github.com/WICG/protected-auction-services-discussion/issues/27
[2]: https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings
[3]: https://meet.google.com/htk-obgg-smb
[4]: https://tel.meet/htk-obgg-smb?pin=4553130257370
[5]: https://github.com/WICG/privacy-preserving-ads/blob/main/Open%20Discussions/20240924-WICG_TPAC_Criteo_OnDeviceVsServerSide.pdf
[6]: https://github.com/privacysandbox/bidding-auction-servers/issues/23
