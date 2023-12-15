# Protected Auction Services WICG Calls: Agenda & Notes

Calls take place on some Wednesdays, at noon New York = 9am California.  Please check https://github.com/WICG/protected-auction-services-discussion/issues/27 for details.

That's 6pm Paris time and 5pm UTC (those change sometimes, when some country fiddles with their clocks).

(This notes doc will be editable by everyone, during the meeting)

**Wednesday December 13 2023**

Attendees: please sign yourself in!



1. Itay Sharfi (Google)
2. Roni Gordon (Index Exchange)
3. Brian May (dstillery)
4. Wendell Baker (Yahoo)
5. Phil Lee (Google Privacy Sandbox)
6. Paul Jensen (Google Privacy Sandbox)
7. Kevin Lee (Google Privacy Sandbox)
8. Daniel Kocoj (Google Privacy Sandbox)
9. David Dabbs (Epsilon)
10. Rémy Saissy (Teads)
11. Fabian Höring (Criteo)
12. Brian Schmidt (OpenX)
13. Sid Sahoo (Google Chrome)
14. David Roundy (NextRoll)
15. Agustin Recouso (NextRoll)
16. Andres Bordese (NextRoll)
17. Garrett McGrath (Magnite)
18. Kapil Vaswwani (Microsoft)
19. Pawel Ruchaj (Audigent)
20. Laszlo Szoboszlai (Audigent)
21. Harshad Mane (PubMatic)
22. Matt Davies (Bidswitch)
23. Xavier Capaldi (Optable)
24. Isaac Foster (MSFT Ads)
25. Konstantin Stepanov (Microsoft Ads)
26. Paul Farrow (Microsoft)
27. Jacob Goldman (Google Ad Manager)
28. Laurentiu Badea (OpenX)
29. Vincent Minet (Criteo)
30. Miguel Morales (TechLab)
31. Guy Edwards (Arcspire)
32. Shankar Venkataraman (Jivox)
33. Boris Shmerlin (Start.io)
34. Motti Shpirer (Start.io)
35. Alexander Tretyakov (Google – Privacy Sandbox)
36. Arun Nair (Google Priv. Sandbox)
37. Kenneth Kharma (OpenX)
38. Ken Gordon (Azure Confidential Computing)
39. Takuro Sato (Microsoft)
40. JR Ereyi (Google Privacy Sandbox)
41. David Tam (Relay42)
42. Akshay Pundle (Google Privacy Sandbox)
43. Viacheslav Levshukovr (MSFT Ads)
44. Mahati Chamarthy (Microsoft)
45. Zach Edwards (Victory Medium)
46. Kevin Naughton (Google – Privacy Sandbox)
47. Mihir Gandhi (Google - Privacy Sandbox)
48. Robert Kubis (Google Privacy Sandbox)
49. Priyanka Chatterjee (Google Privacy Sandbox)
50. Leiming Zhang (Google Privacy Sandbox)
51. Martin Pal (Google Privacy Sandbox)
52. Federico Soave (OneTag)
53. Premkumar Srinivasan (Microsoft)

Note taker: Phil Lee / Itay Sharfi



*   Scope: 
    *   Bidding and Auction and Key Value server
    *   Not focused on changes in Chrome and Android
    *   Open issues with the Protected Auctions proposal

**<span style="text-decoration:underline;">Next Steps: </span>**



*   Schedule a follow up meeting with B&A and Azure on progress made and what's needed next for participation in Beta and Scaled Testing
*   MSFT Azure to share the whole design and flow with this group
*   For agenda topics please create issue in Github and add to agenda in advance for clarity and participation - https://github.com/WICG/protected-auction-services-discussion/issues

Google Meet joining info

Video call link: https://meet.google.com/htk-obgg-smb 

Or dial: ‪(US) +1 509-676-3166‬ PIN: ‪117 463 428‬#

More phone numbers: https://tel.meet/htk-obgg-smb?pin=4553130257370

_To join the speaker queue:_

_Please use the "Raise My Hand" feature in Google Meet._


# Agenda, 13 December 2023


## Introductions and logistics

Itay will be going over these.


## Open Issues, or Issues that Need Opening



*   Phil Lee - benchmarking of JS/WASM code that runs inside BA or KV:
    *   https://github.com/WICG/protected-auction-services-discussion/issues/29 
*   Kapil Vaswani - support for Azure as a platform for deploying B&A services
    *   Clarify contribution guidelines [[B&A] Clarify contribution guidelines · Issue #30 · WICG/protected-auction-services-discussion (github.com)](https://github.com/WICG/protected-auction-services-discussion/issues/30)
    *   Participating in beta and scale testing [[B&A] Azure participation in beta and scale testing · Issue #31 · WICG/protected-auction-services-discussion (github.com)](https://github.com/WICG/protected-auction-services-discussion/issues/31)
    *   Clarifications regarding KMS APIs [[B&A] Requirement for EncryptionKey fields · Issue #32 · WICG/protected-auction-services-discussion (github.com)](https://github.com/WICG/protected-auction-services-discussion/issues/32)
    *   HPKE Key signing [Signing of HPKE public keys · Issue #33 · WICG/protected-auction-services-discussion (github.com)](https://github.com/WICG/protected-auction-services-discussion/issues/33)
*   Roni Gordon - TEEs in Non Public DCs
    *   https://github.com/WICG/protected-auction-services-discussion/issues/14 \

*   <Please add issues here.  It’s preferable to open a new Github issue in the repo, [here](https://github.com/WICG/protected-auction-services-discussion), and then put a link to it in this doc along with your name.  That way people can comment on the subject even if they can’t attend the meeting.>


## Notes

IS (Itay): Welcome to our first meeting!  This forum is separate from the existing Protected Audiences WICG call so that we can focus on the trusted servers.  The audience here is also for Android and Chrome use cases of servers.

DD: What’s the expectation about when more people will be brought in for testing?

IS: Please add this to the agenda.

IF: For this meeting and group, what’s the scope?  Is it dealing with issues for the current Fledge proposal’s TEEs?  (Roma, etc, etc).  Is the scope broader into how can we implement advertising on TEEs?

Addenda: Isaac is sorry he jumped the gun

PL: Initial scope is B&A and KV servers, not looking to go broader.  If changes are needed in Chrome or Android, then not necessarily for this call; better for other WICG call.  Github repo is the same scope as call.

IF: Is group the same scope as call?

IS: The group also discusses trusted servers for Android, and use cases that are not only Protected Audience.

BM: For people who’re jumping around between meetings, let’s make sure there’s a link to the [Chrome WICGProtected Audience (FLEDGE) call](https://docs.google.com/document/d/1Kr0hpfQ_Q1LX1aN00D5k_09yV_a7WE9RSn69nS3nZho/edit#heading=h.l1zcw3fpe8jc) and [repo](https://github.com/WICG/turtledove/) and other related resources, like the Chrome PA repo and meeting.  **AI: Add this.**

MD: Bid Switch is an independent middle layer that can be used for various things, e.g. traffic shaping.  Is that in scope for this meeting?

IS: Anyone’s welcome to open issues and bring them to this meeting, the same as how the Protected Audiences call works.  Traffic shaping questions are welcome.  Some topics cut across the Chrome API and Trusted Servers; for those we’ll do our best to pass them to the [Chrome WICGProtected Audience (FLEDGE) call](https://docs.google.com/document/d/1Kr0hpfQ_Q1LX1aN00D5k_09yV_a7WE9RSn69nS3nZho/edit#heading=h.l1zcw3fpe8jc) and share closely with them.

BM: Have we considered adding a Github label to allow people to flag which side of the client/server line an issue will land on?

PJ: There’re 2 repos now.  Filing repos that’re specific to each topic is fine and we can move issues between repos.  We can also link between issues in the two repos.

KL: An issue can be migrated easily within the same org.

IS: We’re leaving the topic of the KMS (key management service) out of scope for this group as it’s covered by the Measurement WICG group.  Topics that don’t have the right people will be moved offline.

KV, BM: **AI: Add a ‘Resources’ section that links to the Measurement WICG as well as the repos that make up B&A.**

IS: KMS-specific conversations are not in the group.  It’s a different engineering team and it’s the same KMS system that’s used by PA as well as Measurement.

IF: This is PA/Fledge/TEE related questions?  KMS is an overlap.  Microsoft has some KMS questions so we should work out where those questions should be discussed.

PF: Are we sure that the Measurement group won’t send it back to this group?

AN: Let’s do this on a case-by-case basis.  With some heads-up we’ll make sure to invite the right people to this group and we can have the discussion here.

PF: What’s a good heads-up time? \
AN: A week.

IF: Fledge is a level above KMS, so we can start here and maybe pull in infra people as needed.

BM: Let’s flag in the agenda whether an issue will be discussed or whether it’ll be deferred so that we can pull in the right people.

Logistics:

IS: There’s no meeting in 2 weeks, next meeting is the first week of January.  We’re aiming for every 2 weeks.

BM: **AI: Let’s have a Google Groups entry for calendaring for this meeting - copy the Protected Audiences WICG setup.**

IS: There’s a number of people working on different areas, to make sure we can get them to this meeting please put issues on the agenda in advance (see above).

Azure support

KV: Looking to support adtechs deploying BA on Azure.  The TEE and KMS is different to what’s currently supported but the aim is to follow the same principles.  Various questions about this: contribution guidelines to add Azure support to BA.

MG: Two parts to this question: Azure support during load testing and beta phases and then contribution guidelines.  On the first one, we didn’t see as much interest in Azure when we initially chose the Clouds to support.  Given the timeline for beta and load/scale it’s unlikely/impossible that we can add Azure support in that timeline.  However we still want to continue collaborating on this.

KV: Can we understand what it takes to participate in beta/scale testing?  Microsoft may have some infra in place or ability to help out.

PF: To confirm: Azure won’t be supported in beta testing?

MG: There’s a lot of work leading up to beta and it’s extremely unlikely that we can add this support in the next two months.

PF: This request has been existing for a while.

KV: Can we understand what requirements there are?

IF: There’s interest from MSAN (Microsoft Ad Network) and Xandr, although they run in their own datacenters.  Is this saying that the early BA testers have said (1) we won’t use Azure (2) would use it if there (3) will use Azure.  Can we understand the demand?

AN: Please could KV share what the steps look like in migrating to Azure?

AN: There’s been a lot of effort to get to the current state.  It’s not impossible to make progress but it’s difficult to get everything together, including KMS discussions.  Adding a cloud provider is a lot of work.  To IF’s question: have we heard nuances on what the demand is.  It’s a very open ended question and we’ve mostly heard AWS and GCP.  We’d like to hear from Microsoft about how to get BA working on Azure.  And also if IF could share which adtechs are looking for Azure support and their timelines - that can help our prioritization.

IS: Two parts here: building Azure support for BA and &lt;I missed this bit>

LB: Perhaps we can document the requirements for a cloud provider to be able to participate.

IF: One adtech is the company that IF works for (Microsoft).  There are different levels of process that we might be looking for here and the Microsoft team may be able to do some of the work.  Echoing LB’s question on general cloud provider support.  How can we get a widely used public cloud to be supported?  There’s room for us to get together and work on Azure as well as general infrastructure providers.

KV: Quite far along on port of BA and KMS.  This means that it’s definitely not starting from scratch.  Perhaps sync with AN on the porting work.

AN: Yes, let’s do that.  Public communication is fine or sharing it directly if that’s easier.  There is no current process to take pull requests, which we need to be changing.  Could you help us understand the pull requests that are needed for Azure support.  It’s hard to promise anything at this point in the year.

IS: A deep dive into how Azure BA support would work is a good next step.

KV: Have tried to do this but it’s hard to schedule meetings; either in this forum or separate.

IS: Either’s fine.

KG: Have been working on Azure and BA integration and expect to do the engineering work.  I.e. porting your app to our cloud.  The request is to be able to stream data effectively and also that requests and test data are communicated effectively.  I.e. integration conversations.

MG: Sounds good, let’s connect and see how we can move forward.

PF: Offline might not be the right approach, perhaps doing everything in public would be better?  General questions about what has to be done (by any cloud) to fit in.  Starting from adtech requirements is the wrong starting place because it may mean people start with GCP or AWS.  Public conversation, and clear requirements are the right north star.

MG: Agree on public conversation.  Private discussion is just for current progress on KV’s implementation work.

PC: Beta 2 is slated for February.  Does Microsoft have a design that can be shared for what you’re planning for the beta?  It’s easier to understand a design rather than individual pull requests.  Have you gone into the BA dependencies (e.g. key fetching, KMS, etc) too?  It’s not just about BA being cloud agnostic, it’s also about the rest of the trust model will stay the same with Azure support.  Perhaps share the design in this forum?  We can do scoping after we look at the design.

KV: Can share the design.  Yes, looking at KMS, etc, for the design.  Can share both design and implementation in this forum.

IS: How much time do you need to share this?

KV: Next week.

PL: Next meeting is January.

IF: Ad-hoc meeting next week?  There are twice as many people in this meeting as in the Fledge one.

IS: How many meetings to present?

KV: Can do an overview in an hour.  Ready to do it in the next week.

IS: Please do open a Github issue in advance.

KV: Only found out about this forum recently.  On the KMS there have been previous conversations, but all the material can be reshared.

**AI: Let’s schedule an ad-hoc meeting to do this meeting next week out-of-band.  Same time.  IS to confirm whether we can get all of the necessary people.**

IS: Please open a new Github issue for this and we’ll get the right people and do the scheduling.

BM: Doing this in public is also good for anyone depending on cloud providers and wanting insight into how it is implemented and supported.

DD: The adhoc meeting is a ‘builders’ meeting rather than a ‘users’ meeting?  I.e. the people building Azure support for BA?

IS: In general, correct.  We try to have Github issues so that people can decide whether to attend.

RG: Had a similar topic: understanding what the blockers are?  How is the TEE trusted?  What KMS setup is needed?  And then there’s work on the server-side, which anyone can contribute to.  Let’s separate how-would-this-ever-work from implementation.

KV: Agree, and will share the whole design.

MP: There’s interest in supporting other clouds.  Doing early explorations on confidential VMs (Intel, AMD) but there are formidable challenges to the trust model.  There are lots of attacks with physical access to the host.  This is also a good conversation to have - what setup do people have on other clouds?

BM: Two separate BA meetings?  One for people supporting it on their infra and one for using it?

PF: What if you’re doing both?  Go to both meetings?

IS: We’re trying to give the agenda in advance for this meeting so that people can join as they see fit.  We do want to support clouds where the trust model allows.  There’s work happening on evaluating trust models and engineering options.

KV: If the meeting series is dominated by cloud provider questions then we should change something.

IS: Having the adhoc meeting is one way to offload, as are Github issues.  We’ll try to keep space in the agenda for everyone.

DD: On process: for the adhoc meeting, will it be recorded?

PJ: The WICG Protected Audiences call tends to use the notes doc - with links - rather than recording.

PF: Is there a general WICG thing against record?

IS: Depends on consent.

WB: Had this request early in the Fledge calls so that discussion can be freewheeling.  People do read these notes and it can lead to questions.  Explicit rule is to ask and then if anyone says ‘no’ then drop it.  Parakeet calls used automatic transcription but no video.

IS: Please do open issues for the next meeting in advance.

PL: Please do correct these notes! \


GM: What are the requirements for hosting environments that are not cloud? not every ad tech uses a commercial cloud provider. many of us are on-prem DCs via places like equinix etc

VM: The discussion in this group shouldn’t be framed around cloud vs on-prem. Just which requirements are required to clear the bar to host trusted servers.

Need to understand what it takes for Azure to be a part of the Beta and scaled load testing - what dev and documentation requirements are needed from Google for Azure Beta participation. Beta timeline is February. Timelines on github - 

B&A Beta timelines- https://github.com/privacysandbox/protected-auction-services-docs/blob/main/bidding\_auction\_services\_api.md#beta-testing

B&A Onboarding guide: https://github.com/privacysandbox/protected-auction-services-docs/blob/main/bidding\_auction\_services\_onboarding\_self\_serve\_guide.md
