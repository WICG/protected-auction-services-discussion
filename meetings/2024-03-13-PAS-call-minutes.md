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

**Wednesday 13th March, 2024**

Google Meet joining info

Video call link: [https://meet.google.com/htk-obgg-smb][3]

Or dial: ‪(US) +1 509-676-3166‬ PIN: ‪117 463 428‬#

More phone numbers: [https://tel.meet/htk-obgg-smb?pin=4553130257370][4]

_To join the speaker queue_:

_Please use the "Raise My Hand" feature in Google Meet_.

## Attendees

1. Wendell Baker (Yahoo)
1. Kapil Vaswani (Microsoft)
1. Konstantin Stepanov (Microsoft)
1. Martin Pal (Google Privacy Sandbox)
1. Phil Lee (Google Privacy Sandbox)
1. Akshay Pundle (Google Privacy Sandbox)
1. Michael Kleber (Google Privacy Sandbox)
1. Arinha Dey (Google Privacy Sandbox)
1. Aditi Page(Google Privacy Sandbox)
1. Agustin Recouso (NextRoll)
1. Andres Bordese (NextRoll)
1. Maybelline Boon (Google Chrome)
1. Daniel Kocoj (Google Privacy Sandbox)
1. Sid Sahoo (Google Chrome)
1. Courtney Johnson (Google Privacy Sandbox)
1. Dave Garred (Google Privacy Sandbox)
1. Mihir Gandhi (Google Privacy Sandbox)
1. Priyanka Chatterjee (Google Privacy Sandbox)
1. Peter Meric (Google Privacy Sandbox)
1. Jaspreet Arora (Google Privacy Sandbox)
1. Salman Malik (Google Privacy Sandbox)
1. Arun Nair (Google PS)
1. Itay Sharfi (Google PS)
1. David Roundy (NextRoll)
1. Viacheslav Levshukov (Microsoft)
1. Vincent Minet (Criteo)
1. Kevin Naughton (Google Privacy Sandbox)

## Agenda

- Stefan Deml - Direct usage of the Root of Trust provided by Hardware Based TEE
  solutions like Intel SGX/TDX or AMD SEV SNP
- Cost targets for trusted servers
    - [https://github.com/WICG/protected-auction-services-discussion/issues/48][5]
    - [https://github.com/privacysandbox/protected-auction-services-docs/blob/main/bidding_auction_cost.md][6]
    - [Bidding and Auction Cost Presentation][8]

- Azure participation in scale testing, concerns with CCF as KMS
  - [Azure participation in beta and scale testing · Issue #31 · WICG/protected-auction-services-discussion (github.com)][7]

Notetaker: Martin Pal

### Notes

Phil: we have 3 items on the agenda. One is carry-over from last time.

We have ~20 ppl on the call. Pls sign in.

Can we use the automated transcription feature in Meet?

Kleber: I've never used it. A bit hesitant to trust it. How does it attribute
comments to people. Can try it – no strong opinions.

Wendell: In w3c, we've avoided literal transcription available to general
public. A reporter followed up on what's been said. The more literal the
transcript. Legal Discovery.

Manual scribing is work, but adds value.

Itay: feels like there are objections. Can we start?

Phil: I'm leaving Google this week. Arinha will take over chairing the meeting.

Arinha: Hi, I'm a TPM on the trusted Servers team on Privacy Sandbox. I'll
co-chair the call with Itay Sharfi.

Itay: pls sign in, if you haven't already.

Phil: first agenda item is from two weeks ago. Is Stefan on the call? No?

**On hardware based TEEs**:

Martin: Have heard requests for running servers on non-public clouds, using
hardware backed TEEs. Doing early explorations. 3 questions:

- How to build these solutions? (On Intel/AMD tech, OSS hypervisor)
- Can these be secure enough? Challenges in terms of physical access. Logical
  access can still be a problem as the hypervisor is powerful.
- One confidential VM is useful but we'll need multiple working together.
  This'll need productionization work in general.

Premkumar: 2 B&A proposals about <todo>. Realtime selection is support for app-install ads (e.g. gaming on pc/desktop) Do we allow app-install ads to perform realtime inspection on the Chrome side?

- Phil: We're adding this to the agenda for after the other topics

Itay: pls file a github issue for a question/topic you'd like to discuss, then add the issue to the meeting agenda.

Phil: cost targets.

Itay: to give context, we'd like to give more info about compute cost of B&A servers. We're aiming to improve on the cost explainer. Pls read the explainer for background.

Akshay Pundle [presenting]: cost is a big topic. Want to share work we've done in the area. Want feedback & participation from the group.

Main goal is to give visibility into our thinking on cost. Benchmarking. Tooling we're building. Looking for feedback around the method, and metrics to measure. Want to work with ecosystem, value feedback.

Background: scope is limited to operational cost of bidding & auction servers on a cloud system. THere are other cost such as ops personnel. Here we focus only on cloud cost.

Earlier we released an explainer on cost components for b&a. Goes into details of how cost may vary with different factors. Section on cost estimation – how to run a cost test, measure cost, extrapolate to your deployment. This lays groundwork for tools we plan to build. Tooling focuses on b&a, but should extend to other servers like KV servers.

To be on the same page. Many contexts for cost. We want to publish a baseline system with some configuration, with scripts. Measure cost against this baseline. Measure changes against the baseline. We're working on a tool to let you measure and estimate cost. In q2, publish the tool. In q3, we want to publish results from the system.

TL;DR: pls look at the explainer. We're building tools.

Kapil: lot of configuration to this system, including adtech specific config. How do you account for all that.

Akshay: you should measure your own deployment. We will publish a reference/baseline system with a particular configuration. You can make changes to it, run the measurement tool on it. Sandbox team can't measure your own setup, you'll have to do that.

Itay: Purpose of the benchmark. It lets us explain what we mean by a benchmark system. We aim to do this publicly. We're happy to take comments on method. Adtechs can make their own modifications to the benchmark, and publish as they see fit. For ourselves, we'll be able to see what to focus on.

Kapil: adtech will able to run the cost tool to measure cost of their own deployment. It won't measure everything, but adtech can use it to measure what's in scope of the tool. Happy to make changes to the tool based on feedback.

Mihir: two goals. FOr ourselves, have an eval tool to see if we're improving. Second, adtech to measure their own cost. Aiming to satisfy both use cases. Tooling will extrapolate, so not 100% accurate.

Itay: it's a benchmark, so it won't be perfect.

Akshay: this will be an easy way to model/benchmark cost.

Kapil: How tied is this tool to a specific cloud? Do you need a version of the tool for each cloud?

Itay: yes, should work on AWS and GCP. We'll want to focus on reference clouds.

Itay. Cost targets. We're trying to get realistic cost targets. We're thinking X dollars sticker price per 1M requests. Goal is to measure e2e cost on b&a side. Want to eval $$ of serving 1M requests.

Fix latency. Say 200ms. Configurable.

Standard billing on a reference cloud provider. May start with AWS. Dollars per request. Includes networking, load balancing.

Question for adtech: benchmark design. First version of generate bid will be simple. No big model to load.

How we measure cost. Sticker price per 1M requests. May need help from adtech on ground cost targets. On average, for a rmkt ad, what is reasonable cost per 1M requests to make a profit.

We release the tool, users can tweak params. Contributions welcome. Number of IGs.

Benchmarking is hard to get right the first time. But we want to start and get feedback.

Akshay Pundle: We're trying to get a baseline system definitions nd tooling published in Q2. Want to publish reference measurements in Q3.

How does "cost per $1M requests" sound as a metric. Want to develop a vocabulary of metrics. Integral to how we talk about costs. Want feedback on tooling.

What is a way to arrive at "acceptable cost per 1M requests"

Itay: So far we haven't got any feedback on magnitude of cost. Only directionally – we want cheap. Not actionable.

Kapil: good metric to start. Depends on different clouds. There may be static cost oven if there's little traffic. Depends on load balancers.

Akshay: the number we want to release is on a well loaded system. Is this single region, multi region. How much do you overprovision. Provision for average qps, max qps. Say 50% utilization. Not 5% utilization.

Itay: What's a good way for us to get a dollar amount to shot for. One way: adtech disclose some cost, we take some percentage. How do we come up with a number scientifically.

Kapil: are you asking about a cost target.

Itay: what if I say $1 per 1M request. Is that a good target? Too high? Too low? Acceptable?

Premkumar: One way is to look at what cost is spent today, pre-3pcd. Cost to serve existing traffic on existing hardware with 3p cookies. Current cost gives an upper bound on what we're shooting for. Are TEEs more performant than non-TEE. Discount factor?

Akshay: Is the current cost an upper bound? Probably lower bound. Current system is result of long evolution. B&A is private, implemented from scratch.

Itay: say 10%. Debate. How

Prem: adtechs dont' want to increase prices and cost of serving.

Itay: how do we know current cost. Rad public statements? Once we release benchmark, ppl will say its expensive

Wendell: I'm afraid the number you want is a business secret. Perhaps you can get Google to release, or find a friendly adtech who is willing to release numbers. We have very stringent cost constraints. I know adtechs who have daily cost standups.

Itay: dollars per 1M requests seems like a good start. Getting an actual target may require releasing private adtech data. Maybe some adtechs will find a number acceptable, others will complain.

Kapil: if you release the tool, and the tool is sound, adtech can measure for themselves. Maybe adtech can measure, compare overhead vs their legacy system.

Akshay: can adtech release estimates on "production light" workload.

Wendell: nobody pays retail. If you have a big cloud footprint, you get a discount. Deal is "free" as other things are happening off stage. Publish your tool, and everyone will make their own conclusions.

Akshay: all the costs we publish will be "sticker price", no volume discounts.

Itay: we plan to open source the tool. Others can make modifications, publish if they want. Does that sound reasonable?

Wendell: github seems fine, with appropriate license. If ppl proud of their numbers, they'll publish a blog post.

Akshay: thank you for the feedback.

**Phil: next item is Kapil: Azure participation**.

Mihir: no new updates on Azure. TImeline-wise, we won't be able to get Azure ready by June. We may be pushing scale testing back. Don't have announcement ready yet. June milestone not feasible.

Martin: On the question of coordinators: CCF design is fine, the question is how to scale to more clouds. I.e. can we have one coordinator that handles multiple clouds, including Azure. E.g. run on one cloud to service multiple clouds. This would be operationally simpler, regardless of different security properties.

Kapil: This seems ambitious. Clouds are all different in terms of ECB publishing, etc. Is this the main concern around CCF on Azure?

Martin: The goal is scalability. Something that's more centralized will be easier to operate and maintain. Might well run into problems in the details. For on-prem TEEs, there'd need to be some sort of coordinator for those, and if we have to do it for them anyway then maybe we should do it for clouds in general.

Kapil: Tons of details here. E.g. don't want a cross-cloud dependence at startup time. Happy to discuss.

Martin: Could do a hybrid and split key generation vs hosting. Exploration happening on workload identity federation.

Kapil: Workload identity is under cloud providers control, so issues here.

Martin: Cloud provider is currently inside the TCB. E.g. AWS Nitro Enclaves. So it might be okay? And then security requirements go up over time.

Kapil: Agree on hardening over time. We need to decide on what the baseline security is. Azure have been thinking of providing more security than Nitro, if possible. I.e. cloud provider outside TCB. There is no HCL, do direct-boot into an OS image. Image is open source, and runs a container that's measured.

Martin: Time to learn about details of measurement/boot. (See pre-read document on CCF)

[1]: https://github.com/WICG/protected-auction-services-discussion/issues/27
[2]: https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings
[3]: https://meet.google.com/htk-obgg-smb
[4]: https://tel.meet/htk-obgg-smb?pin=4553130257370
[5]: https://github.com/WICG/protected-auction-services-discussion/issues/48
[6]: https://github.com/privacysandbox/protected-auction-services-docs/blob/main/bidding_auction_cost.md
[7]: https://github.com/WICG/protected-auction-services-discussion/issues/31
[8]: resources/bidding-auction-cost-presentation-2024-03-13.pdf
