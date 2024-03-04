# Protected Auction Services WICG Calls: Agenda & Notes

Calls take place on some Wednesdays, at noon New York = 9am California.  Please check https://github.com/WICG/protected-auction-services-discussion/issues/27 for details.

That's 6pm Paris time and 5pm UTC (those change sometimes, when some country fiddles with their clocks).

(This notes doc will be editable by everyone, during the meeting)

**Wednesday 28th February, 2024**

Google Meet joining info

Video call link: https://meet.google.com/htk-obgg-smb 

Or dial: ‪(US) +1 509-676-3166‬ PIN: ‪117 463 428‬#

More phone numbers: https://tel.meet/htk-obgg-smb?pin=4553130257370

_To join the speaker queue:_

_Please use the "Raise My Hand" feature in Google Meet._


# Attendees



*   Robert Kubis (Google Privacy Sandbox)
*   Peter Meric (Google Privacy Sandbox)
*   Daniel Kocoj (Google Privacy Sandbox)
*   David Roundy (NextRoll)
*   Andres Bordese (NextRoll)
*   Stefan Deml (decentriq)
*   Pierre Chlet (decentriq)
*   Paul Farrow (Microsoft)
*   Akshay Pundle (Google Privacy Sandbox)
*   Philip Lee (Google Privacy Sandbox)
*   Kapil Vaswani (Microsoft)
*   Pawan Khandavilli (Microsoft)
*   Wendell Baker (Yahoo)
*   Vincent Minet (Criteo)
*   Isaac Foster (MSFT Ads)
*   Itay Sharfi (Google)
*   Laszlo Szoboszlai(Audigent)
*   Ken Gordon (Microsoft Azure)
*   Mihir Gandhi (Google Privacy Sandbox)
*   Michael Mihn-Jong Lee (Google Privacy Sandbox)
*   Matt Davies (Criteo | Bidswitch)
*   Arun Nair (Google PS)
*   Premkumar Srinivasan (Microsoft)
*   Brian Schneider (Google Privacy Sandbox)


# Agenda, 28th February 2024


## Open Issues, or Issues that Need Opening



*   Akshay Pundle - Updates to B&A Monitoring Explainer
    *   https://github.com/privacysandbox/protected-auction-services-docs/blob/main/monitoring\_protected\_audience\_api\_services.md
*   Philip Lee - https://github.com/WICG/protected-auction-services-discussion/issues/41 
    *   Let’s talk about what ‘general availability’ should mean for the B&A and KV Servers
*   Stefan Deml - Direct usage of the Root of Trust provided by Hardware Based TEE solutions like Intel SGX/TDX or AMD SEV SNP
*   Itay Sharfi - binaries compatibility
    *   Code vs. Binaries
    *   Cloud specific code

Notetaker: Itay


## Notes

**Bidding and Auction monitoring/debugging (by Akshay)**



*   We released a new update to our monitoring metrics:
    *   https://github.com/privacysandbox/protected-auction-services-docs/blob/main/monitoring\_protected\_audience\_api\_services.md
*   Looking for feedback
*   We have published explainer for debugging
    *   https://github.com/privacysandbox/protected-auction-services-docs/blob/main/debugging\_protected\_audience\_api\_services.md	
    *   There’s work to support local debugging
    *   You can also provide traffic to your own using consented debugging
        *   Special bit in Chrome
    *   If you find a problem identified via monitoring such as agg metrics, you can go debugging
*   [Isaac] in normal conditions we understand we can’t log without the restriction
    *   Are there application logs on the box like failed to connect and stuff like that?
    *   Our callbacks might have errors. Can we see them on the machine? Ex: B&A cannot connect via SSL. Will we have those chromium space logs? / var/logs 
    *   [Akshay Pundle] This error is not available per event, you see them in aggregate in monitoring (OpenTelemtry)
        *   Errors by destination grouping
        *   All metrics are instrumented into the code, no custom metrics you can define
        *   Should 
        *   2 types of metrics: things that’re generally applicable should be added.
    *   [Itay Sharfi] Please do open Github issues with information if more metrics are needed
    *   [Brian Schneider] There are structured and unstructured output data (e.g. metrics; logs).
        *   And within that there’s those on the user request path and those that aren’t.  (E.g. KV loading data.)
        *   And then there’s trusted vs untrusted code.  (Aka adtech-space or not.)
        *   For structured metrics that’s not on the user request path, that’s unnoised and goes to cloud metrics via OTel.
        *   For the user request path, that’s noised.
        *   Logging on non-user-request path goes out with no changes.  On the user-request path, logs are dropped.
        *   Dropped logs show up for consented-debug requests.

**GA milestone label for Key Value server (by Phil)**



*   When work is done?
*   Looking for feedback regarding productionisation
*   [Isaac Foster] GA is a tool for clients to inform clients
    *   Expectations is that you are going to fix problem in production
    *   Need to demonstrate usage at scale
        *   Ramp-up with AdTechs
    *   Compatibility with different environment
*   [Philip Lee] The release process for KV has a window
    *   Not documented yet, should write soon
*   [Wendell Baker] GA is a legal term
    *   **AI(pjl): Look into the legal side of this**
    *   Business decision towards the receiver 
    *   Not ok to say we are not going to fix that
    *   Wake up at 2 am to fix, large $$$ riding on it
    *   Hard to get work done in Q4
    *   Organizations don’t like to upgrade, so don’t assume people will upgrade soon
        *   **AI(pjl) how old versions will be supported**
*   [Philip Lee] Policy suggested by aggregation server is published externally
    *   Link policy 
        *   https://github.com/privacysandbox/aggregation-service/issues/23  
        *   https://github.com/privacysandbox/aggregation-service/wiki/Aggregation-Service-release-and-deprecation-plan 
    *   6 months patching window might overlap with Q4
        *   Upgrade during holiday season is a no-go for many companies
*   [Kapil Vaswani] Hardware vendor might have their own release cycle
    *   **AI(pjl): Also look into this one**
    *   In TEEs updates might not be able to wait
    *   Some patches might need to apply quickly because hardware vendor can revoke permission
    *   The way firmware updates get deployed is different between cloud and on-prem, as part of attestation you need to look at what’s deployed and that’s cloud specific
    *   [Robert Kubis] we expect API to not break us from the cloud providers and need to take that into consideration in our changes
    *   Cloud providers might have a hard time to promise release cycle to not break if a security patch is needed

**[Stefan Deml] root of trust**



*   Azure comes with capabilities of hardware root of trust
    *   Any cloud provider might be supported, can also be on-prem
*   [Itay] Please open a Github issue and we’ll make sure that the right people see it, and can bring it up in the next of these calls.
*   [Robert] Also working on making hardware-backed root of trust plans public.
*   [Stefan] How does Microsoft plan on integrating with hardware root of trust?
    *   [Ken] Please see PRs
        *   Run inside confidential containers on ?ACI?
        *   A container policy sets what can run.
        *   The key management service releases keys if the policy allows
*   [Stefan] Is this reproducible?  Using ?Kata?
    *   [Ken] It’s using the ?HCI? container stack and builds on top of Microsoft CCF key management system.

**Itay Sharfi - binaries compatibility**



*   KV Server is being tested and we’re wondering what sort of binary/compiled artificats we should be providing.
*   [Kapil] Also had build time challenges and integrating into the CI process.
    *   You’re already looking at pre-built container images?
*   [Itay] How big a priority is build times?
    *   [Kapil] High, it takes a lot of effort to set up Baze caches, etc.
*   [Robert] We do publish pre-built artifacts for Aggregation Service.
    *   They’re a black-box, so we do want people to be able to compile themselves and verify what’s there.
    *   We should make the build system robust.
    *   Pre-built artifacts have additional legal processes: to release we need to make sure that all of the Open Source licenses are compatible.
*   [Wendell] Looking at code is great, being able to build is part of the OSS experience.  It’s beyond [their] experience to build and get the hashes to match.
    *   $100’s of AWS bills to compile
    *   Yahoo! doesn’t necessary have the staffing expertise for the complex Google-specific build process
    *   Have to do both
*   [Stefan] Already have experience with reproducible hashes.
    *   Zero-day problems make this harder
*   [Robert] What’s the zero-day scenario? Aggregation Service is planning on providing a hash for zero-day fixes, which would be allowlisted.  And then adtechs would have a timeframe to update to the new patch version; then the old version is disallowed.
    *   [Stefan] Agree, but as this is OSS anyone can follow what zero-day patches are being made.  Ideally the patches are applied before the changes show up in OSS codebase.
        *   Usually a small group rolls out zero-day patches.
        *   Customers want to fully reproduce things before they accept changes though.
        *   Disclosure policies also come into play.
        *   Transparency in how patches are applied is important.
    *   [Robert] Challenge here is that adtech are operating the servers and they need to take action to address the vulnerabilities.  So we’d need a way to communicate zero-day changes.
    *   [Wendell] Yes to all the suggestions above.  Support contracts are needed.  Adtechs will need to have time to schedule patches and to assess whether the emergency is one that they want to respect or not.
        *   A universal lockout based on hashes will be difficult for everyone.
        *   We’ll both go through the same process: initial proposal/contract

**Log of chat conversation:**

You

12:03

https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8\_EbPnzcptnhV9mxBP5Mo/edit

You

12:04

https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8\_EbPnzcptnhV9mxBP5Mo/edit

Paul Farrow

12:10

As a PM, I beg to differ

oh I see what u mean now. Totally agree.

Matt Davies

12:25

sorry im late can someone send me the link to the sign in doc please?

Paul Farrow

12:25

https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8\_EbPnzcptnhV9mxBP5Mo/edit

You

12:25

https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8\_EbPnzcptnhV9mxBP5Mo/edit

Paul Farrow

12:25

JUST quicker Philip

Matt Davies

12:26

ty

Isaac Foster

12:40

in theory a "custom error" could have a similar privacy output gate as urls do in core fledge...but, can talk on github

Ken Gordon

12:47

https://github.com/microsoft/hcsshim the container system

Stefan Deml

12:47

ah thanks, that relies on hyperv right?

so is not using nested VMs?

Ken Gordon

12:48

https://github.com/microsoft/azure-bidding-and-auction-services-demo

@Stefan It uses nested. Email me and we can chat offline. ken.gordon@microsoft.com

Paul Farrow

12:51

NTD, apologies.

Stefan Deml

12:52

We spend a lot of time on making various large codebases build binary reproducible (including fw, os, large runtimes). Reach out to me if you want to chat about that topic: stefan.deml@decentriq.com

You

12:53

Thanks, Stefan, we'll do that

You

13:01

Sorry, I'm losing my meeting room and have to drop off.  Please do edit the notes to make sure they're accurate!
