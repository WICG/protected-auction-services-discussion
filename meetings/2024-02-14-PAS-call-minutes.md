
# Protected Auction Services WICG Calls: Agenda & Notes

Calls take place on some Wednesdays, at noon New York = 9am California.  Please check https://github.com/WICG/protected-auction-services-discussion/issues/27 for details.

That's 6pm Paris time and 5pm UTC (those change sometimes, when some country fiddles with their clocks).

(This notes doc will be editable by everyone, during the meeting)

**Wednesday 14th February, 2024**

Google Meet joining info

Video call link: https://meet.google.com/htk-obgg-smb 

Or dial: ‪(US) +1 509-676-3166‬ PIN: ‪117 463 428‬#

More phone numbers: https://tel.meet/htk-obgg-smb?pin=4553130257370

_To join the speaker queue:_

_Please use the "Raise My Hand" feature in Google Meet._


# Attendees



1. Itay Shafi (Google Privacy Sandbox)
2. Peter Meric (Google Privacy Sandbox)
3. Kapil Vaswani (Microsoft)
4. Ken Gordon (Microsoft Azure)
5. Matt Davies (Criteo | Bidswitch)
6. Daniel Kocoj (Google Privacy Sandbox)
7. Leiming Zhang (Google Privacy Sandbox)
8. Pawel Ruchaj (Audigent)
9. Emma Fu(Google Privacy Sandbox)
10. Andres Bordese (NextRoll)
11. Agustin Recouso (NextRoll)
12. Phil Lee (Google Privacy Sandbox)
13. Vincent Minet (Criteo)
14. Alexander Tretyakov (Google Privacy Sandbox)
15. Mihir Gandhi (Google Privacy Sandbox)
16. Paul Farrow (Microsoft)
17. Leon Yin (Microsoft)
18. Sasha Gavrilov (Microsoft)
19. Robert Kubis (Google Privacy Sandbox)
20. Shruti Agarwal (Google Privacy Sandbox)
21. Akshay Pundle (Google Privacy Sandbox)
22. Kevin Naughton (Google Privacy Sandbox)


# Agenda, 14th February 2024


## Open Issues, or Issues that Need Opening



*   Kapil Vaswani
    *   PRs for Azure support
    *   Azure participation in beta and scale testing https://github.com/WICG/protected-auction-services-discussion/issues/31	

Notetaker: Itay Sharfi / Phil Lee


## Notes

Azure support for B&A



*   Google is still unsure about the status of B&A support for Azure
    *   No current resources
    *   Would need reprioritization of other projects
    *   Re-prioritization with leadership may be needed
*   MSFT would like to know the roadmap for having resources to work on it
    *   More specifics on time frame would be good
*   Some technical questions regarding the coordinator design
    *   Should CCF be a dependency
*   Significant lead time for other cloud that were supported
*   DSPs are asking for Azure, could benefit adoption
*   May need a deeper discussion on CCF
    *   In particular: whether to use CCF or the existing KMS on Azure
    *   How much of a challenge is it to use the existing KMS on Azure?
        *   Microsoft think that CCF will be easier to support
        *   The governance cost depends on how much Privacy Sandbox is involved
        *   The third parties involved for KMS already would need to be involved here too
        *   It is feasible to not use CCF but Microsoft would need to scope that effort.
        *   Microsoft have a strong preference for CCF because of maintenance commitments from the Azure team who run it.
        *   There are privacy property differences between CCF and existing KMS, that’s the main question.
*   Microsoft PRs should be of minimal impact and keep things compatible.  The Eng cost to Privacy Sandbox should be minimal.
*   Is the implementation of KMS same between GCP and AWS?
    *   The design is the same but implementations are slightly different.
    *   Cloud-specific infrastructure is different
*   Is Microsoft open to using Terraform instead of bicep (sp?)?
    *   Yes, open to starting with one first and then the other

Traffic shaping, follow-up from the discussion [last time](https://github.com/WICG/protected-auction-services-discussion/blob/main/meetings/2024-01-31-PAS-call-minutes.md)



*   Last time 4 different ways of minimizing DSP load were presented
*   5th way is more limited, and has worse privacy properties
*   No other follow-ups, we should be good.  Adding to the [Github issue](https://github.com/WICG/turtledove/issues/951#issuecomment-1883996605) is always welcome

**<span style="text-decoration:underline;">Next Steps: </span>**



*   **AI: Google and Microsoft should put leadership in touch**
*   **AI: Deep dive into the privacy properties of CCF**

Chat thread, from the meeting:

You

12:01

https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8\_EbPnzcptnhV9mxBP5Mo/edit#heading=h.5xmqy05su18g

You

12:03

https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8\_EbPnzcptnhV9mxBP5Mo/edit

Matt Davies

12:04

Did we finish the discussion on traffic shaping?

Vincent Minet

12:10

+1 to what Paul is saying, we at Criteo would like to see Azure as a Cloud provider. We see diversity of options to host TEEs as very important for the ecosystem, be it on the Cloud or hopefully on-premise.

You

12:10

@Matt - we haven't talked about it yet today, sorry, was that a follow-up from last time?

Matt Davies

12:11

Yeah i was wondering if i missed a meeting as last time it looked as if we got partially through the conversation / presentation but maybe we did

You

12:11

One sec, let me find the notes - I also missed the last meeting

You

12:13

Notes here, looks like you're right and we should continue that discussion: https://github.com/WICG/protected-auction-services-discussion/blob/main/meetings/2024-01-31-PAS-call-minutes.md

Mihir Gandhi

12:15

FWIW, I would not read too much into external job postings wordings - they are generically worded for larger org level; so it may read as on-device but not always necessarily true.

Paul Farrow

12:15

Fair point

I was making a more general point about resources in the space at Chrome. Probably made it poorly though

Premkumar Srinivasan

12:22

Is the implementation of KMS same between GCP and AWS (given AWS started 1.5 years back), and any changes done on higher or lower layers of KMS on AWS, be monitored by Google PS team?
