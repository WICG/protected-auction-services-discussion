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

**Next meeting: 31st July 2024**

Google Meet joining info

Video call link: [https://meet.google.com/htk-obgg-smb][3]

Or dial: ‪(US) +1 509-676-3166‬ PIN: ‪117 463 428‬#

More phone numbers: [https://tel.meet/htk-obgg-smb?pin=4553130257370][4]

_To join the speaker queue_:

_Please use the "Raise My Hand" feature in Google Meet_.

## Attendees:

1. Someone from google
1. Isaac Foster (MSFT Ads | Avengers) (also who put Avengers next to me last
  time? I liked it I just don't know who it got there)
1. Konstantin Stepanov (MicroSOFT Ads)
1. Felipe Gutierrez (MSFT Ads)
1. Alex Cone (Google Privacy Sandbox)
1. Andres Bordese (NextRoll)
1. Agustin Recouso (NextRoll)
1. Martin Pal (Google Privacy Sandbox)
1. Daniel Kocoj (Google Privacy Sandbox)
1. Ashish Bhardwaj(Google Privacy Sandbox)
1. Brian Schneider (Google Privacy Sandbox)
1. (Google Privacy Sandbox)
1. Yashaswini Kumar (Google Privacy Sandbox)
1. Arthur Coleman (IDPrivacy)
1. Yanush Piskevich(Microsoft Ads)
1. Mihir Gandhi (Google Privacy Sandbox)
1. Abishai Gray (Google Privacy Sandbox)
1. Viacheslav Levshukov (Microsoft)
1. Kapil Vaswani (Microsoft)
1. Robert Kubis (Google Privacy Sandbox)
1. Laura Morinigo
1. Yarong Mu (Google Privacy Sandbox)
1. Peter Meric (Google Privacy Sandbox)
1. Akshay Pundle (Google Privacy Sandbox)
1. (Epsilon)
1. Aditi Page (Google Privacy Sandbox)
1. David Roundy (NextRoll)

## Agenda

### Suggest agenda items here:

- Isaac:
  - Roma gVisor Sandboxing Structure
    [https://github.com/WICG/protected-auction-services-discussion/issues/79][5]

**Note taker**:

### Notes

Isaac Foster: Roma gVisor ([GH Issue][6]

How will ROMA gVisor fit into the sandboxing structure? WIll the gVisor
container replace v8, or sandbox2, or SAPI. Is there a change to hooks allowed
in the UDF to run query. Communication between loaded data and UDF.

Brian Schneider: Plan is to integrate this with B&A and KV. The V8 option will
remain an option for UDF. Inference remains as is.

How this works: google security policy and Sandbox policy for privacy. Security
policy is two layers of protection. For v8, it is SAPI and v8. For gVizor,
Sentry and limited system calls.

For privacy, v8 isolates make things side effect free.

For gVizor, clone/PivotRoot/exec to provide side effect free-ness

Arthur Coleman (via chat): What does SAPI stand for?

Brian Schneider/Isaac Foster: SAPI = [sandboxed API][7]. Extension/wrapper of
sandbox2

David Dabbs: Did you say per request execution?

Brian: your executable will get file descriptors to read request from, and write
response to. Another file descriptor for lookups on the KV database.

Pool of workers ready to hande requests.

Isaac: Let me repeat this back. Consider KV server. Trusted code receives
request. Adtech has indicated it's using BYOS binary. THe trusted code will
spawn a new process for every request. Binary will execute, read input, write
output. It will have GetValues hook.

GetValues will be a gRPC interface.

Executing in gVizor, so capabilities limited. What happens if binary makes a
call that's not supported.

Brian: this sounds accurate.

Peter Meric: yes, each worker is spun up fresh per request.

Shruti Agarwal: If syscall not supported returns operation not permitted. For
more details, see

[https://gvisor.dev/docs/user_guide/compatibility/linux/arm64/][8]

David Dabbs: WIll this apply to bidding?

Brian Schneider: Eventually, yes.

Brian Schneider describing diagram:

Runner firing up pool of workers

David: question about GetValues. Everything loaded needs to be cached in memory.

Brian: yes, the KV DB needs to be in-memory [for privacy]

If your KVDB is shareded, your UDF implementation can be oblivious to that

Isaac: What does this solve? Ability to use own binary is quite substantial.
WASM is not ideal.

Crossing the boundaries with hook calls is still significant. That cost will be
independent of the binary. Is the boundary required by Sandbox privacy stance?

Under what conditions would it be OK to remove this boundary.

Brian: side-effect free per request. We need to be able to guarantee you're not
keeping state across requests.

David Dabbs: same with B&A -- can't keep context across requests.

Brian: for adoption, BYOB is easier than wasm. Wasm doesn't have threads; here
in theory you can. Second, performance is improved. WIth v8, we use "inline
wasm". To pass data, everything needs to be copied to jst, then to wasm. Here we
elide one copy. Native code vs wasm code. For certain use cases, native code is
faster.

Clone/PivotRoot/Exec is overhead. For very small UDFs, v8/javascript is probably
faster.

Isaac: Excited about the improvement. Want to understand if this solves any
other issues besides programming model. I also want to talk about sandboxing
consequences.

Side-effect free, what does it mean? Don't want to mix signals across contexts.

One worker per origin

Brian: what if we're not strictly side effect free? Sandbox implications.

First question. We have no control over the network. You have a process that
gets a user request, you cache the request & response. On next (attacker)
request, echo data from first request, and leak data.

David Dabbs: What is the crossover between v8 being better vs BYOB better. Are
you going to support both?

Brian: we're supporting both. You get to choose which one you want to use. You
configure js/wasm or executable. The KV server loads data via delta files,
including executables/UDFs.

Peter: you have 3 UDF flavors. Executable, javascript, or wasm. Depending on
your application, optimizing compilers etc, you may find one being better than
the other. We can show toy examples of logic where either is the best.
What language is your code in? Etc.

Isaac: There's some feature loss in wasm -- threads, assembly etc.

Brian: there's cost to the first invocation of a system call by a given process.
At each point you invoke a system call you're going to pay a cost.

Isaac: When I said sandboxing consequences, I meant what are the implications
for security boundary. My understanding is that the gVizor vs v8
security/sandboxing is different.

Brian: gVizor is Google security team's policy.

Per-request invocation is Sandbox privacy policy.

Kapil Vaswani: On the v8 side, there's a clear security boundary. For gVizor,
the question is servicing the security boundary. Does it mean every time there's
a vulnerability in the kernel or sentry, there will be a security patch &
release.

Brian: any security vulnerability in the trusted code is our responsibility to
patch, and release. What level of threat requires what action. We could have
written trusted code in a way that leaks.
Configuration of gVizor is part of the trusted code.

Kapil: combination of gVizor and linux kernel is what guarantees security.

Brian: yes, the linux kernel is part of TCB, and if there's a vulnerability,
it;'s up to us to patch.

Kapil: with v8, we have a solid security layer. Most kernel vulns won't threaten
v8.

Brian: According to Google security team, gVizor counts as two isolation layers.
[https://gvisor.dev/security/][9], [https://gvisor.dev/docs/][10]

Kapil: What TEE model do we have in different clouds. In Azure, there's some
decoupling between kernel and the container.

Shruti: gVizor intercepts syscalls, applies a policy. Has overrides for certain
syscalls.

Isaac: trying to understand whether the security/utility tradeoff is worth it.
With wasm, it seems the UDF is more limited, and less able to exploit kernel
vulnerabilities.

Peter: with gVizor you won't get direct access to the kernel.

Isaac: is it explicitly agreed that Chrome will be OK with sending data into a
UDF running in gVizor?

David Dabbs:

Isaac: the sooner you can officially state whether BYOB is officially supported
for processing user traffic in B&A, the better. When that happens, I expect a
lot of WASM work to stop.

Brian: you have access to the public repo, you'll see our progress.

David: you said timeline. Public timeline says Q1'2025 for B&A. Ready for scale
operation? Is gVizor part of that B&A milestone?

Priyanka Chatterjee: Please giev us time. We're working on a timeline. First
step is publishing a timeline. No commitments from B&A, but we'll keep everyone
posted.

Priyanka: understood that you'd want to drop WASM in favor of BYOB. We're
working on it.

Brian: gVizor needs testing with AWS, GCP. We're not 100% sure this can run
everywhere (e.g. SEV-SNP CVMs)

Peter: we're reasonably confident, but until we've demonstrated it works in each
environment (with security, privacy and performance) we're cautious.

Isaac: Microsoft also has a cloud, called Azure. I'll send pointers.

Kapil: We want to make sure all of this also work on Azure.

Brian: gvizor doesn't require /dev/kvm, so it should be able to work in more
constrained environments.

### Chat log

You

6:04 PM

Please sign in:
[https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8_EbPnzcptnhV9mxBP5Mo/edit?usp=sharing][11]

keepPinned

keep_off

Unpin message

Isaac Foster

6:05 PM

i can do it!

Arthur Coleman

6:10 PM

what is does SAPI stand for? Services API?

Isaac Foster

6:12 PM

Sandbox API

Arthur Coleman

6:12 PM

AH got it - I have seen this - first time it has been brought to a high enough
level to remind me/force me to study it. Thanks guys

David Dabbs

6:12 PM

The API dude abides

Isaac Foster

6:12 PM

[https://developers.google.com/code-sandboxing/sandboxed-api][7]

Isaac Foster

6:19 PM

putting my hand up to get in queue for hwne this part is done, not interrupting

David Dabbs

6:23 PM

Good think they;re not plastic!

Peter Meric

6:44 PM

[https://gvisor.dev/docs/][10] has some nice images/info regarding kernels, VMMs
and layers

David Dabbs

6:53 PM

Yes, looking forward to the Explainer. 👍

Arthur Coleman

6:54 PM

Me too

Peter Meric

6:57 PM

what's Bing?

Isaac Foster

6:57 PM

i hear about it in presentations here sometimes

[https://azure.microsoft.com/en-us][12]

Arthur Coleman

6:58 PM

Isaac - time to go into sales

[1]: https://github.com/WICG/protected-auction-services-discussion/issues/27
[2]: https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings
[3]: https://meet.google.com/htk-obgg-smb
[4]: https://tel.meet/htk-obgg-smb?pin=4553130257370
[5]: https://github.com/WICG/protected-auction-services-discussion/issues/79
[6]: https://github.com/WICG/protected-auction-services-discussion/issues/79)
[7]: https://developers.google.com/code-sandboxing/sandboxed-api
[8]: https://gvisor.dev/docs/user_guide/compatibility/linux/arm64/
[9]: https://gvisor.dev/security/
[10]: https://gvisor.dev/docs/
[11]: https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8_EbPnzcptnhV9mxBP5Mo/edit?usp=sharing
[12]: https://azure.microsoft.com/en-us

