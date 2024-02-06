# Protected Auction Services WICG Calls: Agenda & Notes

Calls take place on some Wednesdays, at noon New York = 9am California.  Please check https://github.com/WICG/protected-auction-services-discussion/issues/27 for details.

That's 6pm Paris time and 5pm UTC (those change sometimes, when some country fiddles with their clocks).

(This notes doc will be editable by everyone, during the meeting)

**Wednesday 31st Jan, 2024**


## Open Issues, or Issues that Need Opening



*   Kapil Vaswani - Update on Azure implementation of B&A services and participation in beta and scale testing
    *   [Azure participation in beta and scale testing · Issue #31 · WICG/protected-auction-services-discussion (github.com)](https://github.com/WICG/protected-auction-services-discussion/issues/31)
    *   Discussion on PRs and next steps
*   Itay Sharfi - Traffic Shaping using contextual signals in KeyValue
    *   https://github.com/WICG/turtledove/issues/951#issuecomment-1883996605
*   List of explainers for review
*   Inference - https://github.com/privacysandbox/protected-auction-services-docs/blob/main/inference\_overview.md
*   PAS B&A - https://github.com/privacysandbox/protected-auction-services-docs/blob/main/bidding\_auction\_services\_protected\_app\_signals.md
*   Ad retrieval - https://github.com/privacysandbox/fledge-key-value-service/blob/main/docs/ad\_retrieval\_overview.md
*   B&A cost explainer - https://github.com/privacysandbox/protected-auction-services-docs/blob/main/bidding\_auction\_cost.md
*   B&A self serve and onboarding explainer - https://github.com/privacysandbox/protected-auction-services-docs/blob/main/bidding\_auction\_services\_onboarding\_self\_serve\_guide.md
*   

Attendees: please sign yourself in!



1. Itay Sharfi (Google)
2. Robert Kubis (Google Privacy Sandbox)
3. Ken Gordon (Microsoft)
4. Chau Huynh (Google PS)
5. Sven May (Google Privacy Sandbox)
6. Jaspreet Arora (Google Privacy Sandbox)
7. Daniel Kocoj (Google Privacy Sandbox)
8. Akshay Pundle (Google Privacy Sandbox)
9. Peter Meric (Google Privacy Sandbox)
10. Mihir Gandhi (Google Privacy Sandbox)
11. Lukasz Wlodarczyk (RTB House)
12. Matt davies (Criteo | Bidswitch) 
13. Renan Feldman (Google PS)
14. Vincent Minet (Criteo)
15. Arun Nair (Google PS)
16. Alexander Tretyakov (Google PS)
17. Pawel Ruchaj (Audigent)
18. Arinha Dey (Google PS)
19. Premkumar Srinivasan (Microsoft)
20. Isaac Foster (MSFT Ads)
21. Paul Farrow (MSFT Ads, British)
22. Kapil Vaswani (MSFT Azure)
23. Michael Lee (Google Privacy Sandbox)
24. Shruti Agarwal (Google Privacy Sandbox)
25. Samantha Jung (Google PS) 
26. Priyanka Chatterjee (Google Privacy Sandbox)

Note taker: 

Notes: 

<span style="text-decoration:underline;">Azure: </span>

[Kapil] - get some sense for where sandbox is around reviewing PRs and also understand the right approach to integrating with B&A

[Ken Gordon] How we are seeking participation is it blocking PR reviews? [Renan] Yes currently PR reviews are blocked 

[Ken Gordon] Parallel outreach to understand timelines and resourcing {Kapil] will help knowing early which direction to push 

[Lucasz - RTBH] rep for DSP participating in sandbox - interested to test microsoft azure in testing B&A - value flexibility and option to choose among various cloud providers - from ecosystem perspective could help elevate entry threshold to testing participation - not blocked on testing but would like the flexibility

[Issac] Xandr is in the same spot as RTBH. Not being blocked is not the same thing as being blocked in workflows - business cannot plan without timelines 

[Renan] useful info from RTBH on azure prioritization 

[Paul Farrow] Level of DSP here is a factor in prioritization 

<span style="text-decoration:underline;">Traffic Shaping: </span>

[Matt Davies] Bidswitch - traffic shaping works really well with AI and ML. Is there a way to be able to get some privacy compliant signals before the auction? Simple things what DSP happen to have an IG on that particular request - are you sending this to every DSP? Seller and buyer front ends - looking at way in traffic shaping what IG are likely to be viable or not

[Kapil] What augmented info would go into contextual signals? Limited first party submission just send identifiers and TEE KV and fetch when you need it - not fetch everything in advance - this needs to be in TEE for privacy reasons 

[Matt Davies] reducing signals where people unlikely to bid - traffic shaping useful with feedback loop on impressions etc, not just who could be potential available but need to link it back to outcomes and results etc 

[Issac Foster] Curious what are the things that Sandbox is including in traffic shaping? Traffic shaping - SSP and DSP component - SSP may short circuit an imp early on, auction unlikely to generate revenue not worth, biddable phase (an auction worth holding) shaping of how we send things to a DSP based on stateful info about predictive value and also this bidder timing out a lot so we are not going to hit them. What is the scope of traffic shaping here? [Itay] reducing QPS on the DSP - less QPS but increasing utility per request

[Matt Davies] Current proposal reduces QPS by half, setup pre targeting campaigns that filter out pre-traffic shaping and reduce QPS substantially - many IG per DSP etc, this may become requirement eventually 

[Itay] Need a cost benefit if SandBox are missing some features and impact on utility 

**<span style="text-decoration:underline;">Next Steps: </span>**

AI: Renan will provide an update on Azure work once we have more insight 

AI: Please add github issues if there is any questions or feature asks for traffic shaping, original issue is here - https://github.com/WICG/turtledove/issues/951#issuecomment-1883996605

AI: Please review the list of [explainers](#bookmark=id.aee6xs1lh07v) and add feedback or questions
