# Protected Auction Services WICG Calls: Agenda & Notes

Calls take place on some Wednesdays, at noon New York = 9am California.  Please check https://github.com/WICG/protected-auction-services-discussion/issues/27 for details.

That's 6pm Paris time and 5pm UTC (those change sometimes, when some country fiddles with their clocks).

(This notes doc will be editable by everyone, during the meeting)

**Wednesday Jan 17, 2024**


Note taker: Martin Pal

**<span style="text-decoration:underline;">Next Steps: </span>**

Google Meet joining info

Video call link: https://meet.google.com/htk-obgg-smb 

Or dial: ‪(US) +1 509-676-3166‬ PIN: ‪117 463 428‬#

More phone numbers: https://tel.meet/htk-obgg-smb?pin=4553130257370

_To join the speaker queue:_

_Please use the "Raise My Hand" feature in Google Meet._


# Attendees



1. Martin Pal (Google Privacy Sandbox)
2. Wendell Baker (Yahoo)
3. Mihir Gandhi (Google Privacy Sandbox)
4. Daniel Kocoj (Google Privacy Sandbox)
5. Kevin Lee (Google Privacy Sandbox)
6. Paul Farrow (Microsoft)
7. Sid Sahoo (Google Chrome)
8. Renan Feldman (Google Privacy Sandbox) 
9. Pawel Ruchaj (Audigent) 
10. Phil Lee (Google Privacy Sandbox)
11. Agustin Recouso (Nextroll)
12. Andres Bordese (NextRoll)
13. Kapil Vaswani (Microsoft)
14. Priyanka Chatterjee (Google Privacy Sandbox)
15. Yashaswini Kumar (Google Privacy Sandbox)
16. Cfir Cohen (Google. First 30min)
17. Arinha Dey (Google Privacy Sandbox)
18. Viacheslav Levshukov (Microsoft)
19. Akshay Pundle (Google Privacy Sandbox)
20. Vincent Minet (Criteo)
21. Arun Nair (Google PS)
22. Robert Kubis (Google Privacy Sandbox)


# Agenda, 17th January 2024


## Open Issues, or Issues that Need Opening



*   Isaac Foster - discussion of “TEEs in your own DCs”
    *   [Carried over from last time]
*   Kapil Vaswani - Update on Azure implementation of B&A services and participation in beta and scale testing
    *   [Azure participation in beta and scale testing · Issue #31 · WICG/protected-auction-services-discussion (github.com)](https://github.com/WICG/protected-auction-services-discussion/issues/31)
    *   Understanding criteria for participation in beta/scale testing
*   Phil Lee - Clarifying contribution guidelines (in particular support, design reviews, etc)
    *   https://github.com/WICG/protected-auction-services-discussion/issues/30 
*   Itay Sharfi - Traffic Shaping using contextual signals in KeyValue
    *   https://github.com/WICG/turtledove/issues/951#issuecomment-1883996605
*   <Please add issues here.  It’s preferable to open a new Github issue in the repo, [here](https://github.com/WICG/protected-auction-services-discussion), and then put a link to it in this doc along with your name.  That way people can comment on the subject even if they can’t attend the meeting.>

Notetaker: Martin Pal


## Notes

Phil: Itay, over to you

Itay: we have a couple of interesting topics. There’s an issue about traffic shaping

Phil: follow up question from last time. Is Isaac on the call. Question is about TEE in your own datacenter.

Renan: Let’s go with other topic while Isaac gets here.

Kapil: Main question we want to discuss. Want to give update on our PR process. What does it mean to participate in beta and scale testing. We are raising PRs in the B&A repo with Azure specific changes. Have first small PR. Over the course of the next 2-3 weeks we plan to have all PRs out. 

We want to understand what does it mean to participate in beta. What bar do we need to meet as both Azure CSP and as an adtech.

Mihir, let me respond. Thanks Kapil. Criteria for beta: agnostic to Azure being ready. No Google criteria. Anybody is welcome to participate in beta. Let us know if you’re testing so we can ask you for feedback. 

Itay: First, participation in beta means working with the partner team. No specific criteria. Regarding which cloud and when: requires engineering and prioritization on our side. 

Renan: nothing to add

Kapil: Want to understand what Itay said. As Azure we can’t participate, but I also hear there’s effort on Google side to let Azure participate. 

Itay: two separate questions: (a) supporting Azure, and (b) participation in actual beta on AWS or GCP. We need to internally align on headcount for support of clouds beside AWS/GCP.

Kapil: you mean outside GCP/AWS

Mihir: Kapil is perhaps asking whether we’re committed to supporting Azure. 

Kapil: what work is required to support Azure. 

Mihir: we haven’t looked at your code yet. Understand the security model. We won’t have a solid answer for the next ~2 weeks. Attempting to ballpark work on Google side and headcount. 

Kapil: to rephrase. Google needs ppl to code review msft contributions. G needs to bring up stack in Azure environment. Set up CI. Is there more work than eyeballing PRs.

Mihir: on the KHS side, we’re trying to understand CCF. Also trying to evaluate Bicep vs Terraform and whether we want to take that work on. Testing work. Don’t have a ton of Azure expertise. Want Azure environment for testing and CI. All of this requires reprioritization internally.  Can’t commit until we’ve done the scoping exercise w. leads. 

Itay: we do want to support more clouds. Team has a lot on the plate. Hopefully we can get back to you when we see the PRs. 

Kapil: we can still participate in beta, right?

Mihir: yes, you can participate on GCP or AWS if you like. Question is whether Azure stack will be ready for beta. We cannot commit on that yet.

Itay: pls talk to our partnership team to prioritize.

Paul Farrow: can you detail the partner team. 

Itay: Usually, we work with the partnership team. We get a list of requests from adtechs to participate. We prioritize and set up engagements. 

Paul: as Azure, or GCP/AWS?

Itay: we don’t know if we’ll have Azure ready. 

If you want to participate in official beta (aws/gcp), work with partnership team. If you want to participate Azure, work with the eng team. 

Paul: the two paths are not as separate on the msft side as they are on Google side. 

Itay: don’t want to commit until we understand the amount of work.

Itay: how do you see the long term support of msft contributions?

Phil: yes, I want to ask about long term support, but don’t want to jump queue. 

Isaac: let’s talk mainenennace first. 

Phil: how do you think about design review, coding style

Isaac Foster: can we use tabs instead of spaces

Phil: is microsoft committed to long term maintenance?

Kapil: we are happy to write and maintain azure specific code. There is a lot of surrounding code that will be maintained by Google. The KMS is something Microsoft expects to maintain. 

Phil: awesome. 

Renan: As you develop the Azure code, how do we imagine supporting adtechs who want to run on Azure. Msft adtech can be supported internally?

Kapil: we at msft haven’t focused on supporting 3p adtechs. We need to address it, haven’t figured it out. 

Isaac: how does support work with Amazon today. 

Renan: google is the first line of defense.

Isaac: what is the long term plan>

Renan: I don’t know if we’ve clarified this yet. 

Isaac: if there isn’t clarity for AWS, it;s not reasonable to expect to have answers for Azure. 

Kapil: Depends on the amount of interest from adtechs, and Microsoft resources for support. Don’t have answers yet.

Renan: Google does have channels set up with adtechs. Partnership teams help onboard. 

Kapil: we would take responsibility to onboard in the short term. 

Paul: We don’t have clarity internally at Microsoft, but we don’t expect to drop this responsibility on Google. 

All said, it seems we are generally aligned. Having Azure be part of this is good for the overall confidential computing story. We (msft) are excited to participate.

Phil Lee: to reiterate, lack of clarity is about the long term.

Kapil: how do we do releases. Whole bunch of questions to address. Happy to work together. 

Phil: lots of productionization decisions to make. Aggregation service has already gone through the growing pains of setting up a release process. 

Phil: second half of my issue is about design reviews. If we propose a new feature, we have internal security and privacy reviews. What I don’t know is how to run this process ina public forum. 

Kapil: great question. I don;’t think there are a lot of precedents. What would help is if you can share Google’s process. Microsoft also follows a bunch of processes. We can try to replicate.

Phil: I want to find out how OSS projects like Chrome and Android are making decisions. 

Kapil: microsoft would be happy to contribute to this. 

Phil: that’s end of my topic. 

Isaac Foster: next topic. Not sure I have anything new since we talked 4-5 months ago. Opening up to more clouds is a good thing. There is a larger issue. One of the goals of privacy sandbox is to not be anti-competitive, not produce a walled garden. Xandr wants to run on own infrastructure as a competitive advantage. The B&A code has pretty bad performance even in toy settings. In the foreseeable future we’ll have server fleets for contextual traffic. Traffic across datacenters will be a pain and latency hit. For those reasons I’d like to push for criteria that don’t involve a public cloud. Standard on where stuff is deployed based on physical and software security rather than public cloud. Maybe public cloud is perceived as more safe. I know Xandr, Criteo, RTBHouse would be interested. 

Renan: Thanks Isaac for raising this. To outline the difficulties: all the hardware based TEEs have security attack vectors that isn’t well defended. If environment is hostile / can’t be trusted, that adds difficulty to the trust model. I hear the sentiment of SLA, performance. How do we still keep a security bar we still find acceptable. 

Our research so far – we haven’t yet found standards that would easily applied to this scenario. If you know of some, we’d love to hear.

Vincent Minet: msft, google, amazon also have an ad operation and a cloud. So these companies are going to run on your own platform. How can ad companies do the same. 

Isaac: If one requirement is public cloud, and not your own cloud, maybe then we can say Chrome uses another cloud, Edge uses another cloud. But I don’t see this as requirement. 

Kapil: there are concerns around TEEs even from research perspective. Yes, there are not standards. We can take this as an opportunity, and take this to CCC. We know there are standards on physical security,v etting employees. Let’s make a list of minimum criteria. 

Renan: this is also how we’re thinking about it. We are considering. Public clouds are bound by standards: Iso ???, CLoud Security Alliance. Adtechs currently may not keep up.

Isaac: if international standards are included in a proposed bar, you should write that up. “Public cloud” is not a precise 27001 is the right one, vs another norm. If you want to publish this in a github issue, that would be a good place to start. Not saying this is easy. We should work together on this.

Renan: I hear you about publishing an initial set fo standards. 

Isaac: maybe you can say which standards GCP publicly says it complies with are important for the spec. Happy to help drive. 

Renan: I think this topic showed up at PATCG in June. We can think about how to structure this. 

Isaac: this is not trivial, but let’s work together. 

Martin: we’ve been looking at an easier problem: 2 separate legal entities (Cloud, adtech).  If they don’t collude then is it easier?

Can figure out responsibilities of adtech vs cloud.  Want to assume that neither is fully malicious but would also like some hardware attestation.  For some adtech we might not have clarity on their setup and capabilities (e.g. running on bare-metal hardware unless you’re on two level virtualisation).

In that case we need to discuss who manages the hardware, the host software, and boundaries for responsibility.

Kapil: There’s a whole set of issues here where we can’t use existing standards.  E.g. applying updates to a fleet of hardware needs a relationship with the hardware vendor.  There aren’t standards for how often you have to do those updates - it’s best efforts.  That would need formalizing.

Martin: Yes

Isaac: you said cloud provider, I assume infrastructure provider. There’s a company with an infra arm and another arm for advertising. Maybe different domain, different certificate. 

Martin: My interpretation of Kapil’s point is that in order to patch the software you need a certain amount of experience that is often found in cloud providers but not so much in adtech companies.  The adtech may not have the expertise necessary to operate the stack.  There’s also a separate legal separation.

Isaac [also Vincent]: Adtech do have this experience.  AppNexus had their own DCs and now run Xandr datacenters.  We’re not talking about a small adtech, who might use the cloud.  This isn’t a server rack in a kitchen: these are pros.

Martin: Legal separation: the intent is to say that no-one is going to plug random hardware into the machines.  Also, that you’re not going to run malicious software for things like side channel attacks or single-stepping the VM.  For that it’s not clear if adtech should administer the host - Cloud hosts are administered by the Cloud.  Some level of confidence that the cloud isn’t going to mess with the hypervisor.  Adtech have less to lose if they break the rules.

Isaac: Sure

Vincent: This is something that you’re willing to work on and formalize?  We would like to work on formalizing this with you [Privacy Sandbox] and having clear requirements backed by technical requirements and not just ‘public cloud’.

Martin: One question to discuss: would you be okay if Criteo is willing to run on hardware owned by another entity which doesn’t allow physical access?  This is an example of a question to discuss.

Isaac: This would have to involve our techops team.  Trying to find the best path forward.  Colocation really matters: knowing the hardware that’s running and the other applications is important.  If, hypothetically, we had to pay $X per month to another company to keep the hardware access controls then that would probably be fine.  We don’t expect to end up doing exactly what we have been doing, hopefully we can find something in the middle.

Renan: Isaac, your key requirements are latency and SLA?  And you get this from your own hardware.  But the hardware maintenance is less of a concern?

Isaac: Yes, there’s room for negotiation.  Colocation with a datacenter might be important.  A separate rack might be okay.  Want to avoid bad/unpredictable SLAs.  E.g. a pigeon eating through a pipeline and causing a failover.  Top line: SLA, quality, variance, deployment.  We can gradient curve to the right place.

Vincent: Cost is also a factor.

Isaac: Can you explain the hardware attestation where someone is managing the physical hardware, doesn’t the attestation ability give us the attestation that we need?  Then it’s just a matter of physical security?

Martin: SEV-SEP provides VM integrity guarantees.  CPU says this is the exact contents of the VM and that’s good.  But some physical attacks are outside of the attack model that the CPU vendors consider, e.g. power glitching.  Side channels can also be out of scope, e.g. page accesses of the VM can tell you a lot, injecting page faults from a bad hypervisor.  There are ways to set the VM up to help obscure what’s happening but in practice this is hard.

Anything we can do to ensure that the hypervisor isn’t malicious is good.

Isaac: Are all the attacks ones that need physical access?

Martin: Some can happen based on logic access.  E.g. zero days and side channel attacks if you have root access.

**If you’re interested in following up on this topic, please put your interest here so that Isaac can reach out to you:**



*   **Vincent Minet (Criteo)**
*   **Robert Kubis (Google PS)**
*   **Martin Pal (Google Privacy Sandbox)**
*   **Renan Feldman (Google Privacy Sandbox)**
