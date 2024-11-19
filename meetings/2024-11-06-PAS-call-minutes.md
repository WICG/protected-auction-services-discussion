
# Protected Auction Services WICG Calls: Agenda & Notes

Calls take place on some Wednesdays, at noon New York = 9am California. Please
check
[https://github.com/WICG/protected-auction-services-discussion/issues/27][1]
for details.

That's 6pm Paris time and 4pm UTC (until the end of summer, when countries
fiddle with their clocks).

Notes repository:
[https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings][2]

(This notes doc will be editable by everyone, during the meeting)

**Next meeting: Nov 6, 2024**

Google Meet joining info

Video call link: [https://meet.google.com/htk-obgg-smb][3]

Or dial: ‪(US) +1 509-676-3166‬ PIN: ‪117 463 428‬#

More phone numbers:
[https://tel.meet/htk-obgg-smb?pin=4553130257370][4]

_To join the speaker queue_:

_Please use the "Raise My Hand" feature in Google Meet_.

## Attendees

1. David Roundy (NextRoll)
1. Brian May (Individual CLA commitment)
1. Martin Pal (Google Privacy Sandbox)
1. Sven May (Google Privacy Sandbox)
1. David Eilertsen (remerge)
1. Garrett McGrath (Magnite)
1. Isaac Foster (MSFT Ads)
1. Ashish Bhardwaj (Google Privacy Sandbox)
1. Andres Bordese (NextRoll)
1. Agustin Recouso (Nextroll)
1. Aditi Page (Google Privacy Sandbox)
1. Peter Meric (Google Privacy Sandbox)	
1. Yashaswini Kumar (Google Privacy Sandbox)
1. Akshay Pundle (Google Privacy Sandbox)
1. Paul Jensen (Google Privacy Sandbox)
1. David Dabbs (Epsilon)
1. Michael Kleber (Google Privacy Sandbox)
1. Michael Mihn-Jong Lee (Google Privacy Sandbox)
1. Joy Adeyemo (Google Privacy Sandbox)
1. Arthur Coleman (ThinkMedium)
1. Yanush Piskevich(Microsoft)
1. Mihir Gandhi (Google Privacy Sandbox)
1. Priyanka Chatterjee (Google Privacy Sandbox)
1. Xing Gao (Google Privacy Sandbox)
1. Peiwen Hu (Google Privacy Sandbox)

## Agenda

- Peiwen Hu will talk about [Seeking feedback on propagating contextual signals
  to TEE KV server][5]{:.external}
- Alonso Velasquez will talk about [Changes to B&A Monitoring services to
  support an environment with 3pc user choice in Chrome][6]{:.external}
- Akshay Pundle will talk about TEE Inference service on PA ([github
  issue][7]{:.external}, [explainer][8]

The following have been postponed:

- Fabian Höring to present
  [https://github.com/WICG/privacy-preserving-ads/blob/main/Open%20Discussions/20240924-WICG_TPAC_Criteo_OnDeviceVsServerSide.pdf][9]

**Note taker**: Yashaswini Kumar

### Notes

#### Propagating contextual signals to TEE KV server

- Chrome doesn't specify where signals come from: websites (full url) etc
- Not available to K/V service
- KV can only get this from the interest groups
- Challenges:
  - Contextual auction DSP will have to process it even if it doesn't need to
    use it.
  - If it can run in the TKV, flow would be similar
- Re: unnecessary generation of signals
  - In B&A, there is a new API to get encrypted bundled data. Does this allow
    the sellers get the buyer blob?
  - We don't want to provide this → information leak
- On-device Auction for DSP
  - In addition to the bidding signals that make it into the UDF inside TKV,
    per-buyer TKV signals are additional? Or is it a subset?
    - Yes. We don't modify per-buyer signals, but add TKV signals
  - Why don't we allow auction signals without the auction config? Adding the
    full bid request: sending more than we prefer
    - Mixing IG signals with contextual signals in TKV is ok?
  - Per-buyer TKV signals can be used for different things. Can be provided at
    different times.
    - Initiate TKV request right away
    - So we may want to have different signals not dependent on contextual
    - Difference in timing
  - If we can reduce how much send over the wire and be more flexible → great
  - Mixing in TEE should be good
  - Provider TKV signals can be used to generate the bid
  - Is the proposal for on-device usecase? What about B&A usecase?
    - Applies equally to both
- Parallelization
  - For B&A, call to TKV happens after the contextual auction finished for B&A
    - But On-prem, this can be parallel.
  - One TKV call only. If the per-buyer TKV signal contains only information
    from the page and not the auction -> simpler. Can be parallel
  - If per-buyer TKV signal requires information from the auction, buyer has to
    wait for contextual signal to come back
  - Tradeoff needs to be made: IF TKV call has to contain more info from the
    contextual auction, sequencing required.
- Can you have the full page URL when we have TEEs?
  - Yes, unlocks one usecase. There could be more
  - Can be seller url… but you can run bidding auction
- Is this only going to be available only in a cloud TEE?
  - Yes. Not BYOS
  - We are looking at a hybrid model

#### Changes to B&A Monitoring services to support an environment with 3pc user
choice in Chrome

- If 3PC is on, metrics will not be noised
- Discriminating between what is noised and not-noised?

#### B&A Monitoring Services Custom Metrics

- We are proposing that UDF can collect custom metrics
- Are these RTM (Real time metrics)?
  - Not precisely.
  - Each server collects metrics, aggregates and noises them and exports it out
    of the TEE
  - Noise depends on the sensitivity of the metrics
  - The more often you export, there will be more noise
  - Min: 1 minute
  - 1-min interval data has more noise than 10-min interval data
- RTM API: no penalty
- Configure collecting different metrics at different intervals?
  - No flexibility at this time
  - Private aggregation: not in B&A yet
- Optimizing for detection
- Request: For every x number of samples in an interval: give me data
  - Brian May can reply to the github post
  - For example: every 1000 requests
  - Threat model: TBD
  - When traffic is low: quality of data is different than when traffic is high
  - This should not be sampling
- If I have 0 errors, I don't need to know that it is 0. Inform when it is
  noised?
  - Confidence interval of the result

#### TEE Inference service on PA (github issue, explainer)

- Previously only available on Protected App Signals. But now available for
  Protected Audience as well.
- We will have more detailed guides and have another WICG call in the future
- Code is now available

### Chat log

Reminder: Please note your attendance in
[https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8_EbPnzcptnhV9mxBP5Mo/edit?tab=t.0][15]
Isaac Foster

12:22 PM

there's a separate TKV call?

Martin Pál

12:23 PM

I think call happens a bit differently if the auction runsdd on device vs in B&A

Isaac Foster

12:39 PM

apologies i need to drop for an internal meeting, thanks for today, very excited
about increased data flow into TEE KV, will meditate with both a bit more

[1]: https://github.com/WICG/protected-auction-services-discussion/issues/27
[2]: https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings
[3]: https://meet.google.com/htk-obgg-smb
[4]: https://tel.meet/htk-obgg-smb?pin=4553130257370
[5]: https://github.com/privacysandbox/protected-auction-key-value-service/issues/72
[6]: https://github.com/privacysandbox/protected-auction-services-docs/issues/173
[7]: https://github.com/WICG/protected-auction-services-discussion/issues/55
[8]: https://github.com/privacysandbox/protected-auction-services-docs/blob/main/inference_overview.md)
[9]: https://github.com/WICG/privacy-preserving-ads/blob/main/Open%20Discussions/20240924-WICG_TPAC_Criteo_OnDeviceVsServerSide.pdf
[10]: https://github.com/privacysandbox/protected-auction-key-value-service/tree/release-0.17/tools/benchmarking
[11]: https://github.com/privacysandbox/bidding-auction-servers/tree/main/tools/load_testing
[12]: https://github.com/privacysandbox/data-plane-shared-libraries/tree/main/src/roma/benchmark
[13]: https://github.com/privacysandbox/data-plane-shared-libraries/blob/main/docs/roma/byob/Benchmarking.md
[14]: https://github.com/privacysandbox/protected-auction-key-value-service/issues/66
[15]: https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8_EbPnzcptnhV9mxBP5Mo/edit?tab=t.0
