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

## Attendees:

1. Roni Gordon (Index Exchange)
1. David Roundy (NextRoll)
1. Fabian Höring (Criteo)
1. Andres Bordese (NextRoll)
1. Ashish Bhardwaj ( Google Privacy Sandbox)
1. Matt Davies (Criteo | Bidswitch)
1. Matt Kendall (Index Exchange)
1. Kevin Lee (Google Privacy Sandbox)
1. Aditi Page (Google Privacy Sandbox)
1. Peter Meric (Google Privacy Sandbox)
1. Jon Foust (Google Privacy Sandbox)
1. Isaac Foster (MSFT Ads)
1. (IDPrivacy)
1. Akshay Pundle (Google Privacy Sandbox)
1. Daniel Kocoj (Google Privacy Sandbox)
1. Arun Nair (Google PS)
1. Mihir Gandhi (Google Privacy Sandbox)

## Agenda

### Suggest agenda items here:

- [Fabian Höring, Criteo] TEE inference inside the key/value server
  - [https://github.com/WICG/protected-auction-services-discussion/issues/55#issuecomment-2097651667][5]

      - [Fabian} implemented on-device K/V service - looking into how we can
        migrate existing code base to TEE K/V implementationI. Closely following
        PAS explainer - scoring logic implemented - take the campaigns with best
        scores and send them back - scoring logic is implemented with custom ML
        models -would like to do ML inference models inside K/V service
  - [Akshay] BYOS server inside K/V - executing real time models
  - [Fabian] Took into account all constraints with Google PSB to create custom
    implementation - custom UDF executed in the lookup state. Looking to do this
    in an efficient way. Putting two servers - B&A and K/V may not be perfect
    solution - it'll be easier to directly inside the server would be more
    efficient
  - [Akshay} ML inference is executed in real time
  - [Issac] right now we have one server that in effect can have logic and data
    and another server that gets stuff from it - why not have all the signals
    you need from one place to make the process more efficient - PAS is sort of
    solving this
  - [Fabian] start with easiest possible solution - TEE constraint makes it
    difficult to communicate between servers - start with one server where it
    works, is simple - achievable within a realistic timeline. Main motivation
    to migrate existing K/V server - what we already have available key thats a
    good start
  - [Issac] micro service and arbitrary network calls in the TEE - if you have
    the contextual IG signals in the same place - able to run something similar
    to current process in the TEE
  - [Arun] server topology problem - need more flexible topology - B&A can be
    that place with data service backing it - merges sharding in one place. More
    interesting point can we have all the signals, IGs in one place - KV server
    and if KV is running in TEE no difference between running in B&A and K/V. KV
    BYOS makes it not possible to get all the data in KV service - B&A is
    currently running in TEE
  - [priyanka] what is buyside end to end latency target for criteo - 50ms, we
    have benchmarking on latency numbers
  - [Fabian] default implementation should reply in 3ms - thousands of 10k
    QPS/ms. Every note in the pipeline will add latency - K/V will add latency
    why not do http server directly. 50ms is server side, network depends on
    where server and client is located
  - [Issac] Inside bidder response time takes more than 30ms its concerning
    - [Priyanka] in your rtb stack - you may have a distributed cache, does criteo
    follow micro service server or one server that does everything. What is the
    encryption and proxy overhead - lets not conclud that it is high - we can
    share the benchmark data. Servers need to scale - if its loading, caching
    and responding to queries - different from Ml and inference that's current
    way RTB is done
  - [Fabian] Internal K/V server not currently generating bid. The difference
    doesnt deploy in TEE no encryption cost involved - doing computations
    directly with pre object. How will we migrate all this stuff? Today
    inference is in K/V server - we need to migrate first to B&A - we cant
    migrate one part and then migrate second part - how do we migrate our
    current system - on device would be too slow. Part of the bidding i=on
    device, pre scoring server side
    - [Issac] think it's fair for DSPs to say if there are unnecessary hops in the
    system, unoptimized data hops in the server topology - if we can't get
    signals into KV it hinders a lot of optimization - design towards contextual
    signals in KV would help a lot of processing time - pretty good thing to
    explore
  - [Shabsi] interesting to see where the bottlenecks are in the existing work
    that Fabian has done to see where we see the most pain.
    Serialisation/Deserialisation causing problems? Hops causing a lot of cost
  - [Fabian] Can check for the pain points and bottlenecks - arguing against
    could split K/V in two - one part does bidding that can scale independently -
    K/v UDF and inference and one part looking up key values
  - [Priyanka Chatterjee] - The network overhead for hops within TEE KV and TEE
    B&A is over private VPC
  - [Arun Nair] - that is exactly the B&A + KV architecture :) We would like to
    understand requirements - to do gap analysis of the ask and what we are
    missing - what are the requirements, what kind of code and load of models
    you want to run
    - [Priyanka Chatterjee] +100 to Arun. I think what Fabian is explaining is TEE
    KV + TEE B&A
  - [Issac] best would be if inference is implemented on my own - pre-compiled
    model our own JS
  - [Akshay] what kind of models you run? Size? Implementation etc
  - [Fabian]
    - [Roni] greenfield whatever model we want from an adtech POV – it's important
    to make sure that the architecture doesn't preclude that kind of evolution
  - [Akshay] early evolution of inference on Keys - main point to understand
    what does the field look like here - trying to understand the use case.
    Questionnaire to fill out -
    [https://github.com/WICG/protected-auction-services-discussion/blob/main/resources/inference-questionnaire.pdf][6]
    what are the inputs to your model right now?
  - [Fabian] will fill out the pdf and share internally with you - post it in
    github - we can connect through partnerships
    - [Issac] Use cases not becoming specs - break these out into phases - and try
    to see if we can get gains in each phase. Hypothetically first state - if KV
    server was getting contextual signals and had inference service - [Fabian]
    that woud be a good starting point
  - [Matt D] If the KV service got both the contextual and user data - is there
    then a need for the original ORTB request?
  - [Itay] difficulty with TEE - we can try to work through requirements and
    prioritization. Bid that will stay on device instead of running in B&A -
    what is the issue here?
  -

### Notes

### Chat log

Arinha Dey

9:06 AM

[https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8_EbPnzcptnhV9mxBP5Mo/edit][7]

keepPinned

Arthur Coleman

9:10 AM

can we find the iossue number for reference in the notes please

ah nevermind - it is in the title here

actually- not

Arthur Coleman

9:11 AM

the KV server porting docuemtnation looks like a different issue

Priyanka Chatterjee

9:31 AM

The network overhead for hops within TEE KV and TEE B&A is over private VPC

Arun Nair

9:33 AM

Priyanka Chatterjee

9:34 AM

+100 to Arun. I think what Fabian is explaining is TEE KV + TEE B&A

Shabsi Walfish

9:36 AM

(was hoping to get actual latency breakdown numbers if at all possible, since
every impl will have different bottlenecks and always something to learn from
that)

Roni Gordon

9:37 AM

IMO the latency is somewhat beside the point -- this is about the logical
separation of concerns

Shabsi Walfish

9:39 AM

Roni: I understand, but hypothetically if latencies were all zero and CPU was
infinitely fast it wouldn't matter right?

Isaac Foster

9:40 AM

they both matter, independent i thiiiinkk

Isaac Foster

9:42 AM

appreciate that, thanks

You

9:42 AM

[https://github.com/WICG/protected-auction-services-discussion/blob/main/resources/inference-questionnaire.pdf][6]

keep

Pin message

Matt Davies

9:45 AM

If the KV service got both the contextual and user data - is there then a need
for the original ORTB request?

Isaac Foster

9:45 AM

Isaac Foster

9:47 AM

sorry hand ahead of me

Roni Gordon

9:47 AM

indeed, depends what "contextual" scope means in this context

Isaac Foster

9:47 AM

well, i actually meant with rendering and reporting

wasn't even thinking about the bidding strictly

but yes you could see getting in that direction

Roni Gordon

9:48 AM

I'm thinking from the seller's perspective -- so not so much rendering per se

Isaac Foster

9:48 AM

i think, if, we can get to contextual + user data in a TEE, and, if, we can
solve rendering and reporting...i mean, yeah, we're solid

Arthur Coleman

9:52 AM

are we still taking notes?

Roni Gordon

9:52 AM

^^^^

Arthur Coleman

9:52 AM

I can pick up if need be

Isaac Foster

9:52 AM

the rendering/reportng point...hmm...i think that matters sell side too...like
basically, even if you have full auction in KV, even all of your partitioned
IDs, etc, you're still constrained by reporting and some of the current
rendering rules...like, at some point that may be an acceptable tradeoff
(especially as we mitigate those issues)

[1]: https://github.com/WICG/protected-auction-services-discussion/issues/27
[2]: https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings
[3]: https://meet.google.com/htk-obgg-smb
[4]: https://tel.meet/htk-obgg-smb?pin=4553130257370
[5]: https://github.com/WICG/protected-auction-services-discussion/issues/55#issuecomment-2097651667
[6]: https://github.com/WICG/protected-auction-services-discussion/blob/main/resources/inference-questionnaire.pdf
[7]: https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8_EbPnzcptnhV9mxBP5Mo/edit

