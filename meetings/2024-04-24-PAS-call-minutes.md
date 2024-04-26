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

**Next meeting: 24th April 2024**

Google Meet joining info

Video call link: [https://meet.google.com/htk-obgg-smb][3]

Or dial: ‪(US) +1 509-676-3166‬ PIN: ‪117 463 428‬#

More phone numbers: [https://tel.meet/htk-obgg-smb?pin=4553130257370][4]

_To join the speaker queue_:

_Please use the "Raise My Hand" feature in Google Meet_.

## Attendees

1. Mihir Gandhi (Google Privacy Sandbox)
1. David Roundy (NextRoll)
1. Andres Bordese (NextRoll)
1. Brian May (Dstillery)
1. Alex Cone (Google Privacy Sandbox)
1. Martin Pal (Google Privacy Sandbox)
1. Peiwen Hu (Google Privacy Sandbox)
1. Brian Schneider (Google Privacy Sandbox)
1. Michael Mihn-Jong Lee (Google Privacy Sandbox)
1. Nikunj Agrawal (Google Privacy Sandbox)
1. Arthur Coleman (IDPrivacy/ThinkMedium)
1. Christoph Armster (Remerge)
1. Felipe Gutierrez (Microsoft Ads)
1. Konstantin Stepanov (Microsoft Ads)
1. Premkumar Srinivasan (MSFT Ads)
1. Matt davies (Criteo | Bidswitch)
1. Renan Feldman (Google Privacy Sandbox)
1. Bartosz Łoś (RTB House)
1. Akshay Pundle (Google Privacy Sandbox)
1. Vincent Minet (Criteo)
1. Maxime Vono (Criteo)
1. Trenton Starkey (Google Privacy Sandbox)
1. Itay Sharfi (Google Privacy Sandbox)
1. Peter Meric (Google Privacy Sandbox)
1. Arun Nair (Google PS)
1. Priyanka Chatterjee (Google PS)
1. Arinha Dey (Google PS)
1. Wendell Baker (Yahoo)
1. Roopal Nahar (Google PS)
1. Leon Yin (MSFT)
1. Manoj Thakur (MSFT)
1. Ashish Bhardwaj (Google Privacy Sandbox)
1. Steve Gan (Google Privacy Sandbox)
1. Hari Krishna Bikmal (Google Ads)
1. Kapil Vaswani (Microsoft)

## Agenda

Discussed:

- Kapil Vaswani (Microsoft)
  - Azure participation in scale testing
- Renan Feldman (Google Privacy Sandbox)
  - Public cloud TEEs requirements;
    [https://github.com/renanfel/protected-auction-services-docs/blob/main/public_cloud_tees.md][5]

    - Itay Sharfi (Google Privacy Sandbox)
  - Documentation feedback:
    [https://github.com/WICG/protected-auction-services-discussion/issues/58][6]

- Peiwen (Google Privacy Sandbox)
  - KV roadmap
- Mihir Gandhi (Google Privacy Sandbox)
  - [FYI] Update to B&A [timelines][7]
- Akshay Pundle (Google Privacy Sandbox)
  - B&A Inference overview
    - [Presentation][19]
    - Pre-read: [Inference Explainer][8]
    - Discussion and feedback:
      [https://github.com/WICG/protected-auction-services-discussion/issues/59][9]
    - [Inference feedback questionnaire][20]

Backlog:

Notetaker: Martin Pal

### Notes

Itay: we have 2 large topics, and a few shorter ones. Let's do the short ones
first.

Arinha: Renan also has a short topic.

Renan: Hi, I'm Renan from Privacy Sandbox. Earlier this week we published an
explainer on public clouds. Linked in the agenda above. Pls have a look.

Vincent: At Criteo, we've read it. We would like to see an explainer for
non-public clouds. Does this explainer apply to non-public clouds as well?

Renan: we're early on non-public clouds. Some of the items may carry through

Vincent: How would a company target a public or non-public specification. If a
CSP also has a cloud business they'd be using the public cloud specification.
Can an adtech open a small CSP subsidiary?

Renan: requirements we've put in. Public cloud has to be trusted, have
customers. Try to ensure the cloud is trustworthy.

Kapil: Do the existing clouds meet the criteria?

Renan: GH issues on this will be posted soon.

Kapil on Azure scale testing. On the Azure side, we're making progress in our
B&A implementation. Eventually we'd like to give a demo to this audience. Can
Google speak about timelines.

Renan: Can you please file an issue in response to the explainer so we can start
the Azure process.

Kapil: we have in the past shared details about Azure. Happy to refine our
documentation and how we meet these standards.

Renan: at the bottom of the explainer we have a template for filing this issue.

Itay: the issue is to collect information we need about Azure. Supporting B&A is
extra step.

Itay: we're trying to improve our documentation. For K/V and B&A we'd like
feedback on which areas are in need of documentation improvements. Please file
issues to let us know what to focus on. Please ask for information, not new
features.

Peiwen Hu: Hi, I'm from the KV team. Request about CHrome to send full publisher
URL to the KV server. BYOS API will not change. For the TEE KV server, we'll
support an opt-in model. If adtech uses TEE KV, they'll get access to the full
publisher URL in the KV server.

Itay: expect a roadmap document coming soon.

Next: Mihir. Hi everyone. As FYI, we updated the B&A timeline document; link in
notes. Scale testing milestone is moving from June this year to January '25. New
timeline for PA and PAS published.

Itay: link in the doc.

The rest of the time will be dedicated to Akshay talking about inference
capability in B&A. This allows running large models.

Question for Michael: 3pcd timeline. Will Chrome be on 1% 3pcd treatment until
January 2025

Michael Kleber: there was an [announcement][10] yesterday about the change in
expected [timeline][11] on when Chrome will wrap up deprecation of 3p cookies.
3pcd is now scheduled for early 2025.

Itay: please join the Turtledove WICG weekly call

Akshay on inference in B&A:

Problem we're solving: models must be embedded in js/wasm. We want to support
first class ML inference capability, to allow serving ‘large' models. Allow
worklets to connect to a system that runs inference. You should be able to run a
pre-trained model inside the TEE. Training of the model is out of scope; we
assume you already have a trained model you'd like to access in the worklet and
serve from the tee.

This is being built for the B&A set of servers initially for PAS. Aiming for
Q2(?). PA will be a follow-up. Same infrastructure will be used for both. This
will be implemented on the bidding server. Worklets will be able to call
inference. Can be expanded to other worklets/servers/usecases in the future.
Limited to model serving. Work in progress. We'd like feedback. We'll share link
to a questionnaire.

We recently made pieces of this implementation public. Not production ready yet,
but you can try it out. In active development.

Inference capability includes loading models from a cloud bucket. B&A instances
linked to that. Load model inside TEE> Your code running on this server will be
able to call inference. Backends support standard ML frameworks: Tensorflow and
PyTorch. Can support more frameworks. All this runs inside TEE.

We also support factorized models. Use multiple smaller models, combine
predictions into a final prediction. You may consider this strategy if some
features are sensitive, but others are available in your contextual/untrusted
serving stack. You can break up your model, run part of prediction outside tee,
part inside. There will be a way to coordinate model versions, pass data around
so that the final prediction is available in the worklet.

Your service is connected to a cloud bucket. You put your model in the cloud
bucket. Inference runs inside TEE.

Question Brian May: how do I know which model is being used? Model versioning?

Akshay: runInference call takes a model path, which can encode model version.

Model version choice can be done outside the TEE. I'll talk about how to
coordinate model versions. Your code will choose a version based on externally
available info.

For the factorized flow, there are 3 main points that affect inference.
Contextual request outside the TEE can generate embeddings, which you can pass
in via buyerSignals. Can also pass pre-generated embeddings from retrieval (KV)
server.

See diagram. On the contextual path you can generate contextual embeddings, and
pass them in via buyerSIgnals. Can also pass in a version for each model in
buyerSignals. You can pass your own structure describing model versions for this
particular request.

In bidding service, PAS. prepareDataforAdRetrieval(). Retrieval service can use
the ad tower.

We don't control version, you're in control of version info.

In generateBid, predictions combined with user tower to compute final
prediction. If you want, everything can run inside TEE, but you pay the cost.

Questions?

Premkumar: will this be similar for PA?

Akshay: we haven't evaluated the full requirements for PA. But we imagine the
infrastructure will remain the same. There are material diffs between the use
cases, so we're focusing on PAS first.

Bartosz: at RTB House, we like the idea of picking model versions flexibly.
Currently we use a multi-tower models architecture and this proposal would
improve support for A/B testing and upgrading new model versions gracefully.
But, today for performance reasons we rather run our auto-generated code for
models evaluation than using PyTorch for model inference. What I worry about is
adding latency, especially since in the proposed design we separate running
bidding logic in the worklet from the model inference process. What's the main
motivation for doing that?

Akshay: support large models, and efficient execution. We're using C++
implementation for inference, and mature frameworks. In the future, perhaps
accelerators. In contrast, bidding worklets are in javascript. We're building a
bridge to let your javascript call out to a more performant system to offload ML
inference.

Bartosz: this model looks more efficient than javascript, but today, we're
compiling C++ down to wasm. This is at least 10x better than javascript. It
would be good to benchmark wasm vs call out to a ML inference service.

Akshay: definitely go benchmark. If your models are simple, sure, wasm may be
better for you.

Kapil: question from the other side. In this inference setup, what are the
constraints on the model, and sandboxing the model?

Akshay: we sandbox the model the same way we sandbox UDFs. For PyTorch, we
periodically reset the model, as we want it to be stateless. For privacy, we'll
reset the model with some probability to ensure statelessness.

Kapil: in general, PyTorch and TF allow custom code. Is sandbox2 enough of a
mitigation against arbitrary malicious code?

Also, about updates. If TF/PT ship security patches, will you patch as well?

Akshay: yes, we'll want to release with patches. Regarding privacy, we don't
allow custom operators in TF. Tricky to disallow in PyTorch. If you're
malicious, our defense is to reset state with some probability. Working with our
internal privacy folks to hash out details.

It would be nice to guarantee the model is stateless. Maybe we can work with the
platforms themselves to get statelessness.

Kapil: we have thoughts, happy to share separately.

Brian May: composability and richness of model looks promising. How do we
understand what is going on? Debuggability, monitoring.

Akshay. Good question. We've started to look into metrics. Observability, what
can you see operationally. We'll collect metrics about the sidecar, with DP
noise. Some metrics at model level, some at request level, CPU consumption,
#requests per model

For debugging, we'll piggyback on B&A debugging work. Main way is to run stuff
on a local untrusted server. To get a production request, use "consented
debugging" – client indicates the request is consented, and this bit will cause
the TEE stack to produce plaintext debug info, and raw request. If you own a
device, you can set consent bit on it.

Brian: this addresses the two extreme points: specific request, and aggregate
data. Between those two, there are runtime errors that are hard to detect. Have
you thought about how to debug.

Akshay: have thought of this in the context of B&A. We have a notion of
"aggregate errors". You can collect histograms of errors, where each bucket
represents a line of code. This histogram will get DP noised and released. In
aggregate, you can monitor this. Perhaps we can extend this to inference. Happy
to get feedback, collect concerns.

Akshay: 6 mins left. Will breeze through some slides.

Model execution.

Itay: any other big thoughts people would like to share about this feature, its
utility, cost, compatibility etc. You can do things that can't be done on
device.

Brian May: you can run multiple instance of inference engine, compare
performance.

Akshay: haven't thought about model comparison. It would be nice to understand
what you expect to learn from this exercise.

Brian: not sure about exact goal. I put inputs to the model, compare outputs,
compare with something known. Given the insulated nature of the service, want to
compare unknown thing with known thing.

Itay: is this for experiment, or what purpose? Catch problems?

Brian: when dealing with a black box, I want ground truth.

Itay: sound useful, we'll think about that.

Akshay: love to hear your ideas. Pls share, file GH issues.

Brian: in the past, constant fraction of traffic going through a known channel,
compare with unknown channel.

Akshay: need to sort out what runs where. Let's chat more.

Akshay: my feedback slide. Pls give us feedback on these topics.

### Chat log

Peiwen Hu

9:14 AM

[https://github.com/WICG/turtledove/issues/1105][12]

You

9:14 AM

Kapil your hand is still up - legacy hand?

keep

Pin message

Premkumar Srinivasan

9:17 AM

will chrome be on 1% 3PCD treatment flight till end of dec 2024?

Arthur Coleman

9:18 AM

that was my question earlier

Mihir Gandhi

9:18 AM

Context of the question:
[https://privacysandbox.com/intl/en_us/news/update-on-the-plan-for-phase-out-of-third-party-cookies-on-chrome/][10]

Arinha Dey

9:18 AM

[https://privacysandbox.com/open-web/#the-privacy-sandbox-timeline][11]

Arthur Coleman

9:18 AM

so 1% all the way to end fo 2024?

Alex Cone

9:19 AM

@Arthur - Removing third-party cookies for more than 1% of Chrome users will
only be done in consultation with the CMA and with notice to the ecosystem

Arthur Coleman

9:20 AM

I'll take it offline with you - need to chat anyway

David Roundy

9:44 AM

Thank you Bartosz, I had the same questions.

Arinha Dey

9:48 AM

Brian has his hand up as well

Michael Mihn-Jong Lee

9:52 AM

Bartosz, please feel free to share your ideas regarding user privacy and
malicious code in TensorFlow/PyTorch. We also want to hear more about A/B
testing & model upgrade features. Both of them are important features.

Mihir Gandhi

9:52 AM

Largely B&A Debugging and monitoring guidelines will still work with Inference.
Would love to get more feedback on these areas with inference though.

Debugging:
[https://github.com/privacysandbox/protected-auction-services-docs/blob/main/debugging_protected_audience_api_services.md][13]

Monitoring:
[https://github.com/privacysandbox/protected-auction-services-docs/blob/main/monitoring_protected_audience_api_services.md][14]

Trenton Starkey

9:53 AM

Time Check

Michael Mihn-Jong Lee

9:53 AM

(acutally, Kapil has some ideas for user privacy. Again, I'd love to discuss
more offline)

Felipe Gutierrez

9:55 AM

Is the inference API documented? I mean signature,, possible exceptions thrown,
etc. I saw a signature for runInference in inference_overview.md, but the
explainer says those specifications are tentative. Also, the inference explainer
in B&A repo shows a different signature for runInference, where can we read
about the signatures that were actually implemented?

Michael Mihn-Jong Lee

9:55 AM

We have a doc how to build the inference sidecar and some example usage at
[https://github.com/privacysandbox/bidding-auction-servers/blob/main/services/inference_sidecar/README.md][15]

Michael Mihn-Jong Lee

9:57 AM

We use JSON for runInference API, but we have a comparable protobuf definition
available at
[https://github.com/privacysandbox/bidding-auction-servers/blob/main/services/inference_sidecar/common/proto/inference_payload.proto][16]

Felipe Gutierrez

9:57 AM

yes I had seen that, do you have the pointer to the source of runInference?

Itay Sharfi

9:59 AM

GitHub would be great

Michael Mihn-Jong Lee

9:59 AM

runInference() will trigger the C++ callback in the bidding server. PTAL
[https://github.com/privacysandbox/bidding-auction-servers/blob/64cf212087572e4f0c1eac56083e49489d85e06a/services/bidding_service/inference/inference_utils.cc#L131][17]

Mihir Gandhi

9:59 AM

time check - 1 minute left

Felipe Gutierrez

9:59 AM

got it, thanks, Michael

Michael Mihn-Jong Lee

10:00 AM

(assuming you're using TensorFlow, it will send a gRPC request to the Tensorflow
sidecar which is
[https://github.com/privacysandbox/bidding-auction-servers/blob/64cf212087572e4f0c1eac56083e49489d85e06a/services/inference_sidecar/modules/tensorflow_v2_14_0/tensorflow.cc#L122][18]

manoj thakur

10:01 AM

I had a similar comment as Brian, l we usually roll the model out to smaller %
of traffic, would be great to see support for model ramping in this proposal

Felipe Gutierrez

10:01 AM

thank you!

[1]: https://github.com/WICG/protected-auction-services-discussion/issues/27
[2]: https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings
[3]: https://meet.google.com/htk-obgg-smb
[4]: https://tel.meet/htk-obgg-smb?pin=4553130257370
[5]: https://github.com/renanfel/protected-auction-services-docs/blob/main/public_cloud_tees.md
[6]: https://github.com/WICG/protected-auction-services-discussion/issues/58
[7]: https://github.com/privacysandbox/protected-auction-services-docs/blob/main/bidding_auction_services_api.md#timelines
[8]: https://github.com/privacysandbox/protected-auction-services-docs/blob/main/inference_overview.md
[9]: https://github.com/WICG/protected-auction-services-discussion/issues/59
[10]: https://privacysandbox.com/intl/en_us/news/update-on-the-plan-for-phase-out-of-third-party-cookies-on-chrome/
[11]: https://privacysandbox.com/open-web/#the-privacy-sandbox-timeline
[12]: https://github.com/WICG/turtledove/issues/1105
[13]: https://github.com/privacysandbox/protected-auction-services-docs/blob/main/debugging_protected_audience_api_services.md
[14]: https://github.com/privacysandbox/protected-auction-services-docs/blob/main/monitoring_protected_audience_api_services.md
[15]: https://github.com/privacysandbox/bidding-auction-servers/blob/main/services/inference_sidecar/README.md
[16]: https://github.com/privacysandbox/bidding-auction-servers/blob/main/services/inference_sidecar/common/proto/inference_payload.proto
[17]: https://github.com/privacysandbox/bidding-auction-servers/blob/64cf212087572e4f0c1eac56083e49489d85e06a/services/bidding_service/inference/inference_utils.cc#L131
[18]: https://github.com/privacysandbox/bidding-auction-servers/blob/64cf212087572e4f0c1eac56083e49489d85e06a/services/inference_sidecar/modules/tensorflow_v2_14_0/tensorflow.cc#L122
[19]: https://github.com/WICG/protected-auction-services-discussion/blob/main/resources/bidding-auction-cost-presentation-2024-03-13.pdf
[20]: https://github.com/WICG/protected-auction-services-discussion/blob/main/resources/inference-questionnaire.pdf
