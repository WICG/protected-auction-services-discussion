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

**Wednesday 27th March, 2024**

Google Meet joining info

Video call link: [https://meet.google.com/htk-obgg-smb][3]

Or dial: ‪(US) +1 509-676-3166‬ PIN: ‪117 463 428‬#

More phone numbers: [https://tel.meet/htk-obgg-smb?pin=4553130257370][4]

_To join the speaker queue_:

_Please use the "Raise My Hand" feature in Google Meet_.

## Attendees {:#attendees}

1. Wendell Baker (Yahoo)
1. Kapil Vaswani (Microsoft)
1. David Roundy (NextRoll)
1. Andres Bordese (NextRoll)
1. Agustin Recouso (NextRoll)
1. Arthur Coleman (OnlineMatters/ThinkMedia)
1. Akshay Pundle (Google Privacy Sandbox)
1. Dave Garred (Google Privacy Sandbox)
1. Sven May (Google Privacy Sandbox)
1. Aditi Page (Google Privacy Sandbox)
1. David Eilertsen (Remerge)
1. Martin Pál (Google Privacy Sandbox)
1. Arun Nair (Google PS)
1. Vincent Minet (Criteo)
1. Ashish Bhardwaj (Google Privacy Sandbox)
1. Daniel Kocoj (Google Privacy Sandbox)
1. Kevin Naughton (Google Privacy Sandbox)
1. (Google Privacy Sandbox)

## Agenda {:#agenda}

-

Notetaker: Akshay Pundle

### Notes {:#notes}

Premkumar srinivasan: when can we get info about inference capabilities?

Akshay: we're prepping a presentation for this forum. Don't promise a timeline,
but within a few weeks.

Prem: is Google thinking about training as well? I saw some fields being added.
WIll training happen inside TEE, or outside TEE?

Akshay: for now, assumption is that training is outside TEE

Arun Nair: we don't have the right folks here. Can you add this to agenda for
next time, so we can get the right folks on the call.

Follow up question:

Arun Nair: What kind of use cases are you looking at? Click through rate,
conversion rate?

Premkumar: Yes

Arun: Any specif things you want to understand

Premkumar: These models are pretty complicated, cannot wrap it inside JS. The
API part, the RAM, how big the models could be. Implementation code. Privacy
features / Non private features, how do you train non-private features? Do these
come out of TEE, or do these get trained inside

Kapil: How are you thinking about sandboxing, when you do inference.

Arun: Raise a github issue, and we can follow up offline as well.

Yanush: Saw the article about PAS and retrieval service. Works only on android
./ app ads, do you have plans for other type of ads?

Arun: Works only on android, don't have plans for chrome protected audience.
Key-Value server can be used for ads retrieval. Selected ads should match one of
the selected ads kept on the device. Full fledged retrieval server not available
on chrome side.

Arun: How will opening it up help?

Yanush: How will ad tech upload creative in the key-value service?

Arun: Ad retrieval service based off of k/v service. Combination of key-value
lookup and user defined functions. Protected audiences you retrieve and keep ads
on device as a part of daily update. You would keep creative and urls in this
retrieval service. 2 scenarios : render urls kept in retrieval (kanon can be
kept as a part of this) If urls are dynamic, then k-anon needs to be done real
time. Path will be dependent on whether dynamic urls are supported or not.

Arun: K-anon is not expected to be on the critical path for now. When we have
dynamic creative urls, then we need to figure out the design.

Yanush: Will it work only for android? Or also chrome?

Arun: Chrome, is easier for now, because dynamic urls are not supported

Premkumar: App install ads on PCs and Dekstop - gaming is booming a lot, if we
allow app install ads to participate in chrome PA auctions will also be useful

Arun: This may overlap with chrome PA design, can bring it to the previous WICG
group ince this one is server focussed.

Vincent: Exploring other TEEs, any news on that. Can ad tech help for this
exploration.

Martin: We are doing research on running trusted workloads on less than trusted
environment. We are investigating trusted VMs. Can this solution be secure
enough and meet the chrome security bar. Working on publishing something.

Dan: Group of folks doing active research in this area, will share more when we
have more information.

Retrieval explainer:
[https://github.com/privacysandbox/protected-auction-key-value-service/blob/main/docs/protected_app_signals/ad_retrieval_overview.md][5]

Inference explainer:
[https://github.com/privacysandbox/protected-auction-services-docs/blob/main/inference_overview.md][6]

### Chat log {:#chat-log}

[1]: https://github.com/WICG/protected-auction-services-discussion/issues/27
[2]: https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings
[3]: https://meet.google.com/htk-obgg-smb
[4]: https://tel.meet/htk-obgg-smb?pin=4553130257370
[5]: https://github.com/privacysandbox/protected-auction-key-value-service/blob/main/docs/protected_app_signals/ad_retrieval_overview.md
[6]: https://github.com/privacysandbox/protected-auction-services-docs/blob/main/inference_overview.md

