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

**Next meeting: 17th July 2024**

Google Meet joining info

Video call link: [https://meet.google.com/htk-obgg-smb][3]

Or dial: ‪(US) +1 509-676-3166‬ PIN: ‪117 463 428‬#

More phone numbers: [https://tel.meet/htk-obgg-smb?pin=4553130257370][4]

_To join the speaker queue_:

_Please use the "Raise My Hand" feature in Google Meet_.

## Attendees:

1. David Roundy (NextRoll)
1. Andres Bordese (NextRoll)
1. Brian May (Dstillery)
1. Jaspreet Arora (Privacy Sandbox)
1. Aditi Page (Google Privacy Sandbox)
1. Hari Krishna BIkmal (Google)
1. Peter Meric (Google Privacy Sandbox)
1. Isaac Foster (MSFT Ads)
1. Michael Kleber (Chrome Privacy Sandbox)
1. Arthur Coleman (IDPrivacy)
1. Fabian Höring (Criteo)
1. Ashish Bhardwaj (Google Privacy Sandbox)
1. Viachesla (Slava) Levshukov (Microsoft)
1. Suresh Chahal (Microsoft)
1. Maybelline Boon (Google Privacy Sandbox)
1. Felipe Gutierrez (MSFT Ads)
1. Brian Schneider (Google Privacy Sandbox)
1. Abishai Gray (Google Privacy Sandbox)

## Agenda

### Suggest agenda items here:

- [Isaac] gVisor
- [Isaac] Curious to understand what the planned support is for B&A 64bit WASM
  support
  - [Meric] wasm64 -- does v8 support this yet?
    [https://v8.dev/blog/4gb-wasm-memory][5]
- [Slava] I have a few questions regarding the Roma Service. I noticed that
  there has been a new approach proposed for implementing sandboxing for UDFs,
  as outlined in the Roma documentation: Roma gVisor
  ([https://github.com/privacysandbox/data-plane-shared-libraries/blob/main/docs/roma/roma_gvisor.md][6].

    - [Slava] Could you please provide an estimated timeline for when this feature
    will be available in B&A? Additionally, I noticed in the [code][7] , that
    the current implementation relies on the Linux kernel feature. Wouldn't this
    require Cloud providers to carefully manage and update their Linux kernel
    versions to ensure compatibility?

**Note taker**:

Arthur Coleman

### Notes

NOTE: We weren't supposed to be having an agenda, so we missed a whole first
part of this conversation before @Arinha asked for a notetaker……

……… (discussion continues)........

[Arinha Dey] Don't know if the right folks are on the call today.

[Itay Sharfi] We need either Alex, Brian, or someone from the connectivity team
here.

[Isaac Foster] Great topic for next time. I can try to write more than this
gVisor but trying to understand what the target is for that and what the state
is because it does seem like there is some open source stuff but not sure what
the opinion of security and privacy experts is on that versus WASM inside ROMA
where the instruction set is more limited and there is a lot of details there.
Would be really great to hear what the long-term thinking is.

[Arinha] Isaac - can I ask you to create a github issue for discussion next
time?

[Isaac] Of course.

[Viacheslav Levshukov] I have a question about whether this approach will also
be allowed with the B&A.

[Arinha] - Is that something we need to await Alex or someone for?

[Jimmy] Assuming that gVisor becomes part of the mix of possibilities, then it
would apply equally to KV and B&A. But there is nothing to announce or discuss
at this point. Yes there is code in the open-source repo. What's in the repo we
all see, but we are not quite ready to have a discussion around that yet. But
Isaac I think what you said seems plausible.

[Viacheslav] Does this mean that if you publish this approach that it is part of
our options to implement, versus if you don't and then we are limited? How
should we think of this?

[Jimmy] I don't think we have a commitment (to fully deploy) yet. The code is
not a currently supported modality, and could remove that code without notice.

[Arinha] We can follow up next time with more details when the rest of the team
is here.

[Fabian] - For the gVisor code, it doesn't currently seem to work. For example,
if the context needs to be reset after each request, it is already quite clear
this will never work because of the constraints the server works under. Looks
like that is true for even gVisor approach that has been published

[Arinha] The right people are not here. Isaac add an issue in the Github please

[Itay] I talked with him to provide exact details to your question. Sorry it is a
bit late. We had a bit of a conflict and some people dropped, and others
couldn't join.

[Isaac] When someone said nothing was on the agenda, I don't expect a response.
But if he is going to join - I could ask another question.

What is the extent to which B&A will provide support for a 64-bit WASM vs a
32-bit? I've been trying to WASM-ize some of our SSP code. There is a bunch of
stuff we can live without that we do with straight assembly, but with 64-bit
stuff we do there is something weird in a few spots. Brian joined?

[Itay] Question for Brian: When a person looking into the KV code would be
looking into extensions further than having WASM - how is this going to work and
some questions regarding the limits with the current EDF execution model. Fabian
asked a question about this. Might be easier to get this more from you than from
second-hand understanding

Also a 	question about how this similar or not similar to bidding in an auction

[Brian] What extensions are you looking for?

[Isaac] To some extent this is unfair with no agenda items. I wrote down gVisor
as it is something I have been looking at more in the past. One way to discuss
it today: it's interesting to see other sandboxing possibilities other than WASM
under ROMA. I am passingly familiar with gVisor but not clear how it is seen
within the privacy sandbox community as to how it holds up versus something like
WASM in ROMA. From a performance perspective, all excited to use it. What is the
thinking around that? Without guarantees, what are the targets you are seeing
there? Looks like a really promising thing to use something more like native
binaries. But I can understand why that is challenging.

[Brian] If you go to the KV repo, go to workspaces, you will see a dependency on
data plane shared libraries. That's where ROMA lives. If you go to the ROMA
directory there, you will see there is a directory called gVisor. Got some
examples and benchmarks. That is functionality we are looking at but no
documentation and not implemented in any trusted server. There is no final
decision yet. That code does exist in the common repo open sourced under the
ROMA umbrella. I think there are some example benchmarks in there for different
use cases as to how something could potentially work in the future

[Isaac] Peter, maybe you can elaborate on the comment you just made that as a
sandbox technology gVisor is considered stronger than Sandbox 2. Stronger in the
privacy perspective?

[Jimmy] - Sandbox 2 is effectively a filter on system calls. Whereas gVisor does
not filter every system call - it reimplements every system call. It says to the
underlying platform "this is how we are going to implement write or open". In
that sense it is stronger because the full implementation with sys calls is done
in gVisor itself. It also - there are some technical details - they basically
rewrite every call site, for example - it has some sort of magic where it
intercepts that and it does a bit of rewriting of that call site so that
subsequent calls are faster. The mechanics of it are such that - to Fabian's
point, as well - there are lots of details here to be worked out. Exploratory at
this point. Early days. No announcements even to this group. But it is in the
repo so you can see what we are working on in the way of ideas. But until proven
useful in one or more contexts, it may not be much to announce.

[Isaac] Best thing for me is to write up an issue and then have a detailed
discussion. Not trying to get a commitment . More trying to understand how it
fits into the realm of sandbox technologies. How does it do the system calls
differently from Sandbox 2? Where my knowledge falls short: are there
interesting workarounds or exploits people are concerned about? For example with
WASM you are running in this runtime and the instruction set is limited and the
way the memory is set up you get trapped if you try to go outside the memory
boundaries. I don't know enough to know if there are interesting attacks with
gVisor that the privacy community is concerned about.

[Jimmy] In general, the general parameters haven't changed in terms of privacy
and security guarantees.

[Itay] Couple of topics:

1. In general , there are some attacks that might be new that are loading in a
  certain way - would be some differences. We are working through them and some
  people on the call already highlighted them.
1. Regarding the alignment with B&A, we are trying to have a similar execution
  shared or capabilities that are not WASM between key values between WASM and
  B&A. Trying to have that kind of consistency.
1. The third thing that might be interesting is that not all the forms of more
  advanced types of execution that are available as part of the service are
  going to be fully compatible with what is on the device. Certainly for various
  properties. Not necessarily the language, but also what you can do. So, in one
  way, we are compatible. The UVF is not supposed to run on the device, there is
  a known device KV. There are a lot of small branches in the conversation. If
  you can highlight areas of concern to you - e.g. privacy, KVA and B&A
  compatibility -we can address those for you.

We can spend at least an hour just on this topic. I think it is a very good
topic and others have highlighted that.

[Brian] Some commitment has been made to gVisor and arbitrary binaries - we need
a deeper discussion on how it is going to work and have better documentation
when ready.

[Itay] - I think it would be good to do some deep dive into the execution model
with KV and B&A.

[Brian] - Applicable to both. That was one of the questions. I know you opened a
bug on WASM 64, although I haven't personally looked into it. Sounds like Itay
may have. Is there another question

[Isaac] Same question on WASM 64 issue. If gVisor is going to become a thing,
then WASM 64 is not that important. WASM 64 seems like it is not that well
supported right now (IZF update: I must apologize for my slander about wasmtime
and node not doing 64 bit well in the runtime…at least as of now it seems
somewhat supported, the flags are just not well documented).

[Brian][ I don't think that V8 supports it and, irrespective of whether it
supports the 64 spec, it certainly doesn't give you more than 4GB of addressable
memory in WASM in V8 today. That's my understanding. I looked quickly at
WASMtime and it looks like they do support WASM 64 but we don't support WASMtime
at runtime for WASM. Looks like it from a Github issue that has been closed.

[Isaac] Just a bit on various levels of 64 bit support and what you would get
out of it. In the absence of gVisor, it could be interesting to have more than
4GB. Today we have mostly been thinking about this as the Chromium space code
will handle everything and then pass everything off to WASM processes. I think
what Criteo pointed out, as of now, is that some of that boundary crossing is
expensive. And it somewhat limits your ability to map your stack into this
environment. You could see if there is 64-bit support that also expands beyond a
few little tricks - then you could do more in the WASM that allows you to do
less boundary crossing. There would still be benefits from the 64-bit support
just even from a compatibility perspective. If we look at this as if we are
trying to map stacks into this and we are trying to make it more seamless….

[Fabian] In general, the question is on WASM 64 bit. Do you see a use case for
WASM ? Because we saw the same speed as JScript. I don't think it is really
useful for better performance. So the only use case I see is to reuse code
already created or in a shared code base. But this is only useful for people who
currently run RUST code. But I don't think many people in the ad tech industry
use Rust?

[Isaac] Are you saying WASM fully running on the server would have the same
performance as JScript running the same process?

[Fabian] Yes. I didn't make any benchmarks, but when we tried to run on our side
our current bidding script we didn't find any improvement in performance. We
tried with on-device bidding logic.

[Isaac] How much of this is about boundary crossing?

[Fabian] There wasn't any boundary crossing. It was all on-device code. But
apparently this is mainly about people who use RUST today.

[Isaac] We are using C++ for our SSP and DSP, which is why we are looking at
WASM. But I take your point that WASM shouldn't be the end of the discussion for
this.

[Arinha] Isaac please make a discussion post and we will follow up next time.

[Itay] - One question: has anyone tried cost benchmarking for B&A?

[Isaac] We have not yet.

[Itay] It's something we published as open source, so I am kind of interested.
Any other topics on the agenda?

### Chat log

[1]: https://github.com/WICG/protected-auction-services-discussion/issues/27
[2]: https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings
[3]: https://meet.google.com/htk-obgg-smb
[4]: https://tel.meet/htk-obgg-smb?pin=4553130257370
[5]: https://v8.dev/blog/4gb-wasm-memory
[6]: https://github.com/privacysandbox/data-plane-shared-libraries/blob/main/docs/roma/roma_gvisor.md
[7]: https://github.com/privacysandbox/data-plane-shared-libraries/blob/04cb31e8f3efab9b2fedaeed8f5304ed8ad03916/src/roma/gvisor/container/sandbox/pool_manager.cc#L153
