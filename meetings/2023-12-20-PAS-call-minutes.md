# Protected Auction Services WICG Calls: Agenda & Notes

Calls take place on some Wednesdays, at noon New York = 9am California.  Please check https://github.com/WICG/protected-auction-services-discussion/issues/27 for details.

That's 6pm Paris time and 5pm UTC (those change sometimes, when some country fiddles with their clocks).

(This notes doc will be editable by everyone, during the meeting)

**Wednesday December 20 2023**

Attendees: please sign yourself in!



1. Kapil Vaswani (Microsoft)
2. Brian May (dstillery)
3.  (Google Privacy Sandbox)
4. Kevin Naughton (Google Privacy Sandbox)
5. Vincent Minet (Criteo)
6. Mahati Chamarthy (Microsoft)
7. Yanush Piskevich(Microsoft)
8. Renan Feldman (Google Privacy Sandbox)
9. Chau Huynh (Google PS)
10. Mihir Gandhi (Google Privacy Sandbox)
11. Martin Pal (Google Privacy Sandbox)
12. Daniel Kocoj (Google Privacy Sandbox)
13. Owen Ridolfi (Mediaocean)
14. JR Ereyi (Google Privacy Sandbox)
15. Harshad Mane (PubMatic)
16. Amaury Chamayou (Microsoft)
17. Alexander Tretyakov (Google Privacy Sandbox)
18. Ken Gordon (Microsoft)
19. Arun Nair (Google PS)
20. Neil Vohra (Google Privacy Sandbox)
21. (Google Privacy Sandbox)
22. (Google Privacy Sandbox)
23. Suvigya Nijhawan (InMobi)
24. Akshay Pundle (Google Privacy Sandbox) 
25. Samantha Jung (Google Privacy Sandbox)  
26. David Tam (Relay42)
27. Matt Davies (Criteo | Bidswitch) 
28.  (Google Privacy Sandbox)
29. Sid Sahoo (Google Chrome)
30.  (Google Privacy Sandbox)
31. Ruchi Lohani (Google PS)
32. Salman Malik (Google Privacy Sandbox)
33.  (Google Privacy Sandbox)
34. Pawan Khandavilli ( Azure Confidential Computing/Microsoft)
35.  (Google Privacy Sandbox)

Note taker: Martin Pal

**<span style="text-decoration:underline;">Next Steps: </span>**

Google Meet joining info

Video call link: https://meet.google.com/htk-obgg-smb 

Or dial: ‪(US) +1 509-676-3166‬ PIN: ‪117 463 428‬#

More phone numbers: https://tel.meet/htk-obgg-smb?pin=4553130257370

_To join the speaker queue:_

_Please use the "Raise My Hand" feature in Google Meet._


# Agenda, 20 December 2023


## Open Issues, or Issues that Need Opening



*   Kapil Vaswani - support for Azure as a platform for deploying B&A services
    *   Participating in beta and scale testing [[B&A] Azure participation in beta and scale testing · Issue #31 · WICG/protected-auction-services-discussion (github.com)](https://github.com/WICG/protected-auction-services-discussion/issues/31)
    *   Pre-read document [Bidding and Auction Services on Azure](https://1drv.ms/w/s!AmI-86sms1pYqJ5Uqgo5Qv2Ynmrcmw?e=Bnk2Zo)
*   [Itay from Google] Questions from pre-read from Google
*   <Please add issues here.  It’s preferable to open a new Github issue in the repo, [here](https://github.com/WICG/protected-auction-services-discussion), and then put a link to it in this doc along with your name.  That way people can comment on the subject even if they can’t attend the meeting.>


## Notes

Itay Sharfi: We’ve looked at your doc, and have a lot of questions about the preread. 

Kapil Vaswani: Lot of technical detail. How about 15 mins overview, then Q&A

Kapil (main presentation). Focus today is on design & implementation of protected services on Azure. Please read the pre-read doc. Some missing pieces, tried to cover the main pieces. Wanted to build on top of existing elements. Doc is about hosting the services on Azure, using existing Azure container hosting functionality. 

We choose to implement the KMS differently, to provide similar guarantees, but be easier to operate on Azure. Want feedback. We want to be involved in beta/scale testing.

We have components working. Starting integration testing with Chrome and Edge.

Shift to the doc now. [Sharing doc on screen]  [Bidding and Auction Services on Azure](https://1drv.ms/w/s!AmI-86sms1pYqJ5Uqgo5Qv2Ynmrcmw?e=Bnk2Zo). 

Goal: support B&A on Azure. Core pieces of business logic reused from Privacy sandbox implementation. 

Deploying using COnfidential Comtainers on Azure. Allows deploying a group of containers on SEV-SNP VM. 

Full integrity and testability of the workload. Attest kernel image, container runtime, set of containers (just one). 

Use “container scale sets” to deploy at scale and monitor. Deploy multiple VMs, autoscale, monitor.

Different KMS. BUlt on top of Azure offering “hosted CCF”. Cloup provider should not compromise the KMS. Fundamental assurances similar, but easier to manage. 

Mihir Gandhi: Diff between confidential VM and confidential containers.

Kapil: Conf containers: deploy a collection of containers protected by a SEV-SNP VM.

Azure provides VM image. Customer provides the containers. Goal is to attest the set of containers and their security attributes (configs, command lines). 

Martin: documentation on container runtime, guest kernel

Ken: kernel open source, can provide config. Lot of process to build it. Intention is to be fully open sources, reproducible. Hasn’t fully happened yet.https://github.com/microsoft/hcsshim

Kapil: how do conf containers work.

As a tenant, provide description of containers you want to load. Think pod spec. Azure has hosting stack that runs containerd, hcsshim. 

VM boot image: linux kernel, container runtime, containers

Host tells the VM to do stuff: bring up images, run commands etc. Host is untrusted though. Solution: Container policy.

Policy defines set of containers that are allowed to be executed, and their parameters. 

Bidding container: a bunch of flags, plus container image. Container image represented as set of hashes, one per layer.

If host asks VM to do something, runtime checks request against policy. Policy hash baked into VM image, hence remotely attestable. 

Azure offers Tooling to derive policy from a descriptions of containers

Design is generic, can run any set of containers, with any policy.

For B&A, container policy very simple: One container with B&A code.

Details on what is in the policy, what is enforced.

B&A on ACI: changes to support Azure KMS. Already extensibility in B&A codebase to support more KMS. We’ll create a new build flavor for Azure. Core B&A logic remains identical to Google impl.

Arun Nair: Runtime is an open source component. What is a policy?

Kapil: given a container, you can generate policy. REGO(?) policy. Policy captures how the host can interact with the VM. 

Container runtime is invoked on all commands from the host into the VM, and enforces checks.

Itay: When I look at the doc, most of it describes generic Azure platform. As we go into the specifics, two questions:



*   How far you got with integrations of B&A and Chrome/Edge
*   What are the current points where you’re blocked and we (Google) can help

Ken: we can start B&A and send them test messages. We can release keys. Just beginning integration with KMS. 

Problematic: specification of key format, how to publish keys to Chrome. Don’t want to make assumptions by reverse engineering. Cleaning up code; after x-mas may be able to send a PR. 

Kapil: able to bring up sell side and buy side platform, each with a load balancer. Can retrieve bidding script from storage. Can talk to each other. Testing w. Edge/Chrome pending integration questions.

Itay: looks like you need information.

Kapil: when we talk about KMS, how will public key verification work. We have a proposal, but need to collaborate to flesh out requirements. Not blocking at the moment.

Renan: happy to follow up on KHS questions and specs.

Itay: ideally, open an issue on github

Kapil: we may have an existing issue; will ping the link

Akshay Pundle: Can you talk about the division of responsibility between assertions and who enforces what. External attestation vs internal policy.

Kapil: good segway into policy.

Container policy enforced locally vy the VM. The policy is represented in the attestation report. The attestation verifier (KMS) needs to decide if it likes the policy represented in the attestation report. 

In the diagram, ignore multiple CCF nodes. There’s a “key release policy”. The policy defines what CVM images are allowed to get keys. A service operator can propose a change to the policy. Coordinators need to approve a new key release policy. 

A B&A TEE calls the KMS with an attestation report. The KMS checks if the VM image matches a good VM image list, and the policy is a good policy. 

Let’s dive into the architecture of the KMS. It’s based on “managed CCF” which is an Azure service. Key release policy, key rotation policy. Coordinators. Service operator is Azure, but is untrusted. 

Operator can’t observe internal state, and has no voting rights. Operator responsible for availability. Can bring up new nodes. Can propose changes to key release policy; changes must be approved by coordinators. 

Coordinators accept by signing request by their identity. 

Ledger carries information about CCF nodes, and the constitution of the CCF network..

Akshay: multiple parties work together. How many parties are needed to get the key?

Kapil: KMS service has the HPKE keys. Key is not directly shared. Always hosted in CCF nodes (TEEs) or in the ledger, encrypted by ledger encryption keys. 

Worker VMs can talk to a CCF server to get attested, and get the full key.

Coordinators hold shares of the key used to encrypt the ledger. The ledger contains the (encrypted) HPKE key.

Brian Schneider: is is possible to run stuff on the untrusted host, e.g. for metrics collection.

Kapil: OTEL collector is untrusted. You can run it as a separate service, doesn’t matter where it runs.

Brian: On AWS&lt; ,we run one on the host. On GCP, separate service.

Kapil: On Azure, also separate service.

Renan Feldman: What prevents the operator from remotely accessing the container?

Kapil: this is expressed in the policy. Policy san casy “you can’t ssh into the container group”. 

Ken (?): I think exec group is empty. If you allow /bin/bash command, then ppl can use it. These are regular commands one can send to a container group. We should disable all those.

Kapil: the seccomp policy of the container is attested as well.

Back to the KMS. Key release policy governs which TEEs can run. Policy is straightforward. Policy looks at claims from SNP report, and looks at values. Set allowed values for each claim.

Any change (new VM, firmware update) requires new proposal.

Coordinators need involved whenever platform update. Dealing with zero-day.

Verify hpke keys

Ken Gordon: prove the cpu runs in azure. You get that from the . CPU id passed to the KMS. Running on a host that knows these secrets. In the future, certs from AMD will be tied to DC. 

KMS maintqains a list of identity providers to trust. Allowlist adtechs as they join. 

Kapil: KMS is open source. Can host outside Azure, with SGX. managed service on Azure. ACI environment 

Ken: non-azure: the piece that provides confidentiality is portable. Orchestration is aAzure, not easily portable. Could use pieces with SNP hardware. Orchestration part would be new. Not 

Kapil: launch measurement = os+ runtime

Host data = container policy

Priyanka: Couple of questions. Are the keys per region?

Kapil: KMS is a global service. Keys not region specific right now, but regions can be added. If there are requirements that we’re not aware of, can add.

Priyanka: Disaster recovery. Keys are in memory. How do you recover? Need keys from Coordinators.

What is the availability guarantee? 

Amaury: Can add more nodes to improve resilience. Each node has a copy of the key. Need a quorum. Adding to a quorum is only when recovering 

Priyanka: How do you validate identity of the adtech

Kapil: we can elaborate. Set of token issuers is part of CCF state. 

Priyanka: I see multiple splits of public keys. How is the key provisioned to the browser. Private HPKE key is not split, protected by TEE. Split is the ledger encryption key. Browser doesn’t see that. Browser only needs to know the public HPKE key. Ledger key only needed for disaster recovery.

Mihir: Status of the implementation. You say you’ve been testing. What is missing.

Kapil: we have been testing. We can bring up sell side and buy side with load balancers. Not terraform, but similar. Able to talk to KMS, and fetch private keys. Use tooling to send requests, look at responses. 

As part of container scale feature, adtech can configure VM sizes, regions, availability zones, rolling upgrades. In the process of end-to-end testing w. Chrome and Edge. Hope to do open source release in January.

First party adtechs want their own KV service. Happy to work on KV, question of priorities. 

Arun: if you can share pull requests, we’d love to look. What open sourcing means

Kapil: we’ll send a PR. Then, fully open source the KMS application. Open source scripts for deployment. Eventually want to get to parity with your terraform, so an adtech can deploy on Azure. 

Arun: looking forward to next steps. Would be nice to try this with KV.

Kapil: our 1p adtech didn’t ask for KV yet; happy to look

Itay: What do you hope as a next step; how can we support.

Kapil: get more clarity on beta and scale testing. We want to make sure Azure is a viable alternative, so we want to participate in testing. Technical conversations.

Itay: We’ll regroup in january.

Arun: We’d love to understand your high level timeline, who on msft side wants to test, when. Would msft do a public test if this is available?

Arun,. Will Xandr use this on Azure? Are you ready for public testing in Q1?

Isaac Foster: Xandr: yes to Q1. Circle again on details. Will focus on this next month. 

Robert: 

Chat log:

Arinha Dey

6:02 PM

https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8\_EbPnzcptnhV9mxBP5Mo/edit#heading=h.5xmqy05su18g

Itay Sharfi

6:03 PM

https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8\_EbPnzcptnhV9mxBP5Mo/edit#heading=h.5xmqy05su18g

Itay Sharfi

6:04 PM

https://github.com/WICG/protected-auction-services-discussion/issues/31

Kapil Vaswani

6:08 PM

https://1drv.ms/w/s!AmI-86sms1pYqJ5Uqgo5Qv2Ynmrcmw?e=Bnk2Zo

Mahati

6:15 PM

this is the public documentation:[ https://learn.microsoft.com/en-us/azure/container-instances/container-instances-confidential-overview](https://learn.microsoft.com/en-us/azure/container-instances/container-instances-confidential-overview)

Ken Gordon

6:16 PM

https://github.com/microsoft/hcsshim

Priyanka Chatterjee

6:21 PM

We need attendees to check in here[ https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8\_EbPnzcptnhV9mxBP5Mo](https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8_EbPnzcptnhV9mxBP5Mo). Thanks

Ken Gordon

6:33 PM

We use this scheme but without the serviceability provided by reference info.[ https://github.com/microsoft/confidential-aci-examples/blob/main/docs/Confidential\_ACI\_SCHEME.md](https://github.com/microsoft/confidential-aci-examples/blob/main/docs/Confidential_ACI_SCHEME.md)

Priyanka Chatterjee

6:46 PM

Go ahead Martin

Akshay Pundle

6:52 PM

Similar question on policy updates

Ken Gordon

7:02 PM

I have to drop.

Priyanka Chatterjee

7:03 PM

Thank you

Akshay Pundle

7:03 PM

Thanks Kapil!
