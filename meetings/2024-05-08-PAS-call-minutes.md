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

**Next meeting: 5th June 2024**

Google Meet joining info

Video call link: [https://meet.google.com/htk-obgg-smb][3]

Or dial: ‪(US) +1 509-676-3166‬ PIN: ‪117 463 428‬#

More phone numbers: [https://tel.meet/htk-obgg-smb?pin=4553130257370][4]

_To join the speaker queue_:

_Please use the "Raise My Hand" feature in Google Meet_.

## Attendees

1. Arthur Coleman (IDPrivacy/ThinkMedium)
1. Brian May (Dstillery)
1. Kapil Vaswani (Microsoft)
1. Matthew Atkinson (Samsung)
1. Mihir Gandhi (Google Privacy Sandbox)
1. Martin Pal (Google Privacy Sandbox)
1. Peiwen Hu (Privacy Sandbox)
1. Laura Morinigo (Samsung)
1. Agustin Recouso (Nextroll)
1. David Roundy (NextRoll)
1. Dan Rhody (Google Privacy Sandbox)
1. Abishai Gray (Google Privacy Sandbox)
1. Akshay Pundle (Google Privacy Sandbox)
1. Yanush Piskevich (Microsoft)
1. Itay Sharfi (Google Privacy Sandbox)
1. Ashish Bhardwaj ( Google Privacy Sandbox)
1. Matt Davies (Bidswitch | Criteo)
1. Robert Kubis (Google Privacy Sandbox)
1. Renan Feldman (google Privacy Sandbox)
1. Anant Bhatia (InMobi)
1. Imran Nadeem (InMobi)
1. Daniel Kocoj (Google Privacy Sandbox)
1. Felipe Gutierrez (Microsoft)
1. Aditi Page (Google Privacy Sandbox)
1. Arun Nair (Google PS)
1. Shabsi Walfish (Google PS)
1. Isaac Foster (MSFT Ads)
1. Wendell Baker (Yahoo)

## Agenda

### Suggest agenda items here:

- [Fabian Höring, Criteo] TEE inference inside the key/value server
  - [https://github.com/WICG/protected-auction-services-discussion/issues/55#issuecomment-2097651667][5]

Discussed:

- [Anant Bhatia, InMobi] Request for Supporting Azure as a Public Cloud TEE ·
  Issue [#67][6]
- [Isaac Foster, Microsoft] (Isaac: really?) Service composability:
  [https://github.com/WICG/turtledove/issues/1140][7]
- [Robert Kubis, Google Privacy Sandbox] Feedback on consolidating coordinator
  services: Issue [#69][8]
- [Peiwen Hu, Google Privacy Sandbox] Release schedule and support window for
  TEE KV server [#66][9]
- [Martin Pal, Google Privacy Sandbox] Questions about "on-prem/private cloud"
  environments [#68][10]

Notetaker: Arinha Dey

[Anant Bhatia] PM from InMobi - representing for DSP and SSP - primarily based
on Azure - looking for support on TEE for Azure public cloud. Working with Kelly
and Omar on testing and brainstorming on how PSA should be setup and work. This
is for android for PA and PAS.

[Renan] Published requirements for public clouds - we are going to evaluate
requests from MSFT and InMobi go through review process mentioned in explainer.
Step 1 - if cloud is approved and step 2 - when we expect support to be
available - we'll get back as soon as possible. What cloud to support is based
on adtech needs - InMobi is ask important to make sure we are prioritizing cloud
support appropriately

[Renan] Is aggregation service also going to be used on Azure? Or are you going
to leverage GCP and AWS? This ARA which uses Aggregation service which is a TEE
for aggregate data. Can you provide a sense of urgency? WHen and why you need
this?

[Anant Bhatia] Ags is also included in the azure request. Why? We are working
with google to test the system E2E but due to complete dependency on Azure they
are unable to support this - they have an alternative support but they can't
scale. How and when we want to take thing to production - they are testing on
GCP temporarily as soon as they go to production, they will need to be setup on
Azure - need this a few months before to ensure migration.

[Kapil] This is the official response from Azure for TEE requirements,
[https://github.com/WICG/protected-auction-services-discussion/issues/31#issuecomment-2096962679][11]

[Kapil] Specific concern - in typical adtech setting you usually have different
teams that contribute different parts of the logic (signals and bidding and
auction) how to architect B&A in a way that different teams can take different
ownership without compromising privacy and security of B&A. K/V has distributed
K/V service different teams have different attributes - but when you serve the
ad, all attributes comes together. No leakage of traffic analysis is absolutely
required more flexible patterns without violating the code. It will be good to
get design discussions started soon even if implementation comes later. We can
iterate on the more specific design patterns - distributed K/V that feels more
trackable one - addressing specific patterns would be more useful.

[Itay] We looked into composability - one team will look into brand safety, some
team look at something different - maybe different binaries. Details need to be
figured out - info come in different sizes (chaffing maybe needed), sharding
etc. we know its important and aim to prioritize. Think about if you have a use
that you would like to share, brand safety etc - help us to understand
constraints and comms. Chain them with this github.

[Peiwen] Plan to tentatively look into composability in H2 2024 - may not be as
flexible as today's untrusted servers. Some constraints we could have request
size, endpoints etc will be fixed.

[Arun] design requirement? Is this generic? Bidding server needs to orchestrate
between multiple KV servers this we could design and discuss. WHat is the scope
of design you are looking for?

[Brian May] One thing that would be useful to do - supply set of foundational
rules for constraints between multiple servers - might help ppl to think about
the problem

[Martin] You could load multiple data sets into a single physical server, or
each team is writing different logic - is it the same logix today or different
logix in the KV code.

[Arun] Brian - there is some write up on why we need to do chaffing here:
https://github.com/privacysandbox/protected-auction-services-docs/blob/main/bidding_auction_services_system_design.md#fake-requests--chaffs-to-dsp
. But, ack, we can share some more design principles as we think through this
more.

[Robert] COnsolidating coordinators - we are taking feedback for potentially
adding cross cloud capabilities - key hosting on one cloud and serve workloads
on multiple clouds fo getting the keys.

[Kapil] Taking external services even within the same cloud there is hesitancy
to accept so cross cloud seems like it would be difficult to accept. Single
consolidate coordinator has to understand cloud specific TEEs and their policies
with what constitutes known good TEEs - lots of operational challenges to do
this cross cloud

[Robert] these are all challenges we are still thinking through - we envision
doing this in phases not everything would consolidated in one cloud in one go -
need to understand subcoordinator model in each cloud a bit better to avoid the
bifurcation issue

[Dan] We will want to have clear boundaries on SLAs and federate out those
permissions.

[Kapil} federated option maybe a good one

[Renan] More context on value (1) right now dev wise supporting clouds is a lot
of duplicative work across new clouds - greater burden across all teams (2) How
we will be able to support non cloud solutions - this could provide value.

[Shabsi] Would it be more palatable centralized global coordinator chained to
each local cloud? Your complexity is only to validate other coordinators rather
than every single TEE feature.

[Kapil] Advantages to the model you already have - cloud providers can run and
maintain compatible systems is valuable - operation value and resistant to
attacks - one single point of failure is challenging from security perspective -
adtechs may have some specific clouds approved if they have dependencies on
other clouds, they may have to get additional cloud approvals - even external
services falls within compliance approvals

[Robert] They wouldn't maintain any resources within the coordinator cloud, this
would be an external service.

[Renan] how do adtechs think of compliance of external services and how do you
handle?Main parts of processing - stays within the same cloud - fetching keys
from different cloud to encrypt that data

[Issac] Adtechs use external services but not in their hot paths, have
integrated with external endpoints that we don't own and control and there are
paths for that

[Peiwen] on Release schedule proposal for TEE KV	- release code will be for a
stable version of the server for production traffic - main branch will be for
the version that hasn't gone through all the tests so may not be very stable.
Support window will be around 180 days - support vulnerability patches for those
and for oncall and onboarding. Latest release v0.16 - starting from v0.17 having
this support window in place.

[Martin] Get feedback on machine would be managed or co-managed by adtech. Today
wanted to get feedback on if I want to supply a binary adtechs can run, what do I
need to know? Lets say we built software i want to support it for adtechs to run
on On-prem? Lets not worry about security yet, what do I need to do to run a
server on-Prem?

[Kapil] It will be good, for transparency - to start documenting all the
infrastructure pieces that have to come together to run and operate a service
like this - right hardware, hypervisor, environment within the TEE that can
support full attested - caching collateral, way to attest - need infra and
operational (processing for rolling out upgrade etc). On the stack itself it can
be done - don't see that as a barrier - barrier is operationalize infra and
keeping it running long term can be expensive

[Martin] prototype stack that we can ship in GitHUb - maybe first we run a pure
VM - can we actually enable service MVP? It will be an iterative process - would
be helpful from our end to get to a place where we can ship code ppl can start
playing with

### Notes

### Chat log

[1]: https://github.com/WICG/protected-auction-services-discussion/issues/27
[2]: https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings
[3]: https://meet.google.com/htk-obgg-smb
[4]: https://tel.meet/htk-obgg-smb?pin=4553130257370
[5]: https://github.com/WICG/protected-auction-services-discussion/issues/55#issuecomment-2097651667
[6]: https://github.com/WICG/protected-auction-services-discussion/issues/67
[7]: https://github.com/WICG/turtledove/issues/1140
[8]: https://github.com/WICG/protected-auction-services-discussion/issues/69
[9]: https://github.com/WICG/protected-auction-services-discussion/issues/66
[10]: https://github.com/WICG/protected-auction-services-discussion/issues/68
[11]: https://github.com/WICG/protected-auction-services-discussion/issues/31#issuecomment-2096962679

