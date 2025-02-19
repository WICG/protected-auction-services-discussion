# Protected Auction Services WICG Calls: Agenda & Notes

Calls take place on some Wednesdays, at noon New York \= 9am California.  Please check [https://github.com/WICG/protected-auction-services-discussion/issues/27](https://github.com/WICG/protected-auction-services-discussion/issues/27) for details.

That's 6pm Paris time and 4pm UTC (until the end of summer, when countries fiddle with their clocks).

Notes repository: [https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings](https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings)

(This notes doc will be editable by everyone, during the meeting)

**Next meeting: Feb 12, 2025**

Google Meet joining info  
Video call link: [https://meet.google.com/htk-obgg-smb](https://meet.google.com/htk-obgg-smb)   
Or dial: ‪(US) \+1 509-676-3166‬ PIN: ‪117 463 428‬\#  
More phone numbers: [https://tel.meet/htk-obgg-smb?pin=4553130257370](https://tel.meet/htk-obgg-smb?pin=4553130257370)

*To join the speaker queue:*  
*Please use the "Raise My Hand" feature in Google Meet.*

# Attendees:

1. [Alexander Tretyakov](mailto:tretyakov@google.com)(Google Privacy Sandbox)  
2. [Daniel Kocoj](mailto:dankocoj@google.com) (Google Privacy Sandbox)  
3. Brian May (unaffiliated)  
4. [Samantha Jung](mailto:samanthajung@google.com) (Google Privacy Sandbox)  
5. Trenton Starkey (Google Privacy Sandbox)  
6. [Leiming Zhang](mailto:leimingzhang@google.com) (Google Privacy Sandbox)  
7. [Ashish Bhardwaj](mailto:ashishbh@google.com) (Google Privacy Sandbox)  
8. [Kevin Lee](mailto:kevinkiklee@google.com) (Google Privacy Sandbox)  
9. Victor Pena (Google Privacy Sandbox)  
10. Fabian Höring (Criteo)  
11. [Abishai Gray](mailto:abishai@google.com) (Google Privacy Sandbox)  
12. [Robert Kubis](mailto:rkubis@google.com)(Google Privacy Sandbox)  
13. [Mihir Gandhi](mailto:mihirg@google.com) (Google Privacy Sandbox)  
14. Phil Acker (Amazon)  
15. [David Roundy](mailto:david.roundy@nextroll.com) (NextRoll)  
16. [Rashmi Rao](mailto:rjrao@google.com) (Google Privacy Sandbox)  
17. [Andres Bordese](mailto:andres.bordese@nextroll.com) (NextRoll)  
18. [Akshay Pundle](mailto:apundle@google.com) (Google Privacy Sandbox)  
19. [Brian Schneider](mailto:bschneider@google.com)(Google Privacy Sandbox)  
20. [Xavier Plantaz](mailto:xpf@google.com) (Google Privacy Sandbox)  
21. Bill Cox (Google Privacy Sandbox)  
22. [Andrew Chasin](mailto:andrewchasin@google.com)(Google Privacy Sandbox)  
23. [Dipika Suresh](mailto:dipikasuresh@google.com) (Google Privacy Sandbox)  
24. Arun Nair (Google Privacy Sandbox)

# Agenda

For Feb 12 2025

* Fabian Höring  
  * Discuss feedback given here [https://github.com/privacysandbox/protected-auction-key-value-service/issues/72\#issuecomment-2485843775](https://github.com/privacysandbox/protected-auction-key-value-service/issues/72#issuecomment-2485843775)  
  * Feature parity with on device PAAPI (priv agg API, real time monitoring, [https://github.com/WICG/turtledove/issues/1366](https://github.com/WICG/turtledove/issues/1366))  
  * Handle multiple bidding scripts & trusted bidding signals keys ([https://github.com/privacysandbox/bidding-auction-servers/issues/29](https://github.com/privacysandbox/bidding-auction-servers/issues/29))  
* Announcement (Akshay Pundle, Trenton Starkey)  
  * The cost estimation tool explainer has been published ([https://github.com/privacysandbox/protected-auction-services-docs/blob/main/bidding\_auction\_cost\_estimation\_tool.md](https://github.com/privacysandbox/protected-auction-services-docs/blob/main/bidding_auction_cost_estimation_tool.md)).   
  * Please check it out and give us feedback. 

**Note taker:** 

## Notes

* Trenton: Published a new B\&A cost estimation tool, please provide feedback   
* Key Value [https://github.com/privacysandbox/protected-auction-key-value-service/issues/72\#issuecomment-2485843775](https://github.com/privacysandbox/protected-auction-key-value-service/issues/72#issuecomment-2485843775)  
  * Alex: Regarding questions asked by Fabian in github post  
    * Some were addressed last week and still need to cover a few  
      * What are the use cases for B\&A and injecting more signals to KV  
        * When wanting to process signals in conjunction with data, you can do the processing where the data resides instead of having to transmit the data.  
        * Fabian: doesn’t seem to make sense.  Why not pass buyer signals from client.  Don’t want a single state server (kv today).  Want a context state server and a user state server.  Don’t want more server side storage.  If everything needs to be in the KV server, everything should be done there and no need for separate Bidding server.  
        * Arun: KV doesn’t store use data, it stores campaign data  
          * Place for advertisers to store real time signals  
        * Fabian: It must be user data, since I can’t pass it from the IG  
        * Arun: Not used for user data today  
          * Team has proposed change to add contextual signals  
        * Fabian: For B\&A there must be a user data store somewhere.  Today it is the KV server.  
        * Arun: Userlist to campaign mapping?  
        * Fabian: ex. Number of visits a user does on a given website.  First party.  
          * KV is saving user data with certain properties  
            * If buyer signals can’t be passed from client to B\&A then we should introduce contextual storage  
            * If we can pass everything in anycase…why all these containers?  What is the difference between BFE, Bidding Server, KV?  
            * Currently focused on BA  
              * Limited to number of bytes client can pass all the way to the bidder  
        * Arun: Reading back understanding of claims made by Fabian  
        * Fabian: B\&A contextual signal has plenty of signals, why add more to KV.  
        * DavidR: actual contextual data does not help, the only place where it is helpful is the place where we get the contextual data   
        * Fabian: Think that existing RTB payload is big & duplicated   
        * DavidD: Most of what’s in RTB   
        * BrianS: Original comment in the Github, KV is trying to be generic, in the event that I need to join, pass the small data vs large amount of data to KV, would be beneficial to passing it to KV  
          * Alex: Optional  
          * Arun: mirrors what RTB is doing today at the retrieval stage like geotargeting, and adds value who want to filter ads upfront   
        * Alex: ok to move onto the other issues?  
        * Fabian: it is ok for some to use this.  Maybe it will add value, but not as is.  Concerns about additional overhead of additional containers needed to do this.  
        * Alex:  compute can involve data lookups and set queries.    
        * Fabian: still thinks interesting to have a context storage layer.  Possible to use key value server for this.  Maybe it is the same to do that, will give it some thought.  Maybe just need right keys in kv.  
        * Arun: Maybe per buyer signals can be generated in kv and that is the value  
        * Fabian: wants one container to do everything.  Dont’ need bidding service and front end.  Will see with testing  
        * Arun: We would like to know what the capabilities are required to do something like generate per buyer signals in a trusted server.  This is happening in untrusted servers today.  Would be a good topic for a future session.  Call out to David for requirements  
        * DavidR: Would like the code that does this should be isolated from first party user data, should have some way of logging the buyer signals generated (acknowledges security/privacy challenge).  With this we could put bid id \-\> later wins. And allow for ML training to figure out where auctions runs and where wins can happen.  
        * Arun: Historically the contextual towers have big big with a cardinality explosion.  Contextual models have been relatively larger than others.    
        * David: Our contextual are not that big. Logging also provides reach estimation.  New campaigns can associate publisher sites with keywords, how often do we get auctions per keyword so advertisers can make an informed choice on campaign creation.  
        * Arun: thanks to David and Fabian  
        * Alex: Question about adding inference to KV  
          * We think ad retrieval service should eventually support it, but no timeline.  
          * Any further questions  
        * Fabian: What is the plan on the feature \- per buyer signals in kv  
        * Alex: Currently available in B\&A with explainer published  
          * On device which would be more useful for you is a WIP  
          * Should be the next thing we do as far as i know  
  * Private aggregation API  
    * Fabian: what will be fixed in the next release and what else will happen  
    * Ashish: Issue raised will be fixed in 4.7  
      * Other features will be published in release notes  
      * Singal seller private aggregation in previous release  
      * Real time metrics will publish an explainer on RT monitoring  
        * Can have further discussion after publication  
      * Request to queue up questions   
    * Fabian  
      * Want to register metrics in UDF  
        * On device and B\&A  
    * Rashmi: will be an explainer   
    * FAbian  
      * I wnat to A/B test on-device and BA  
      * Need to see what works better \- 2025 goal  
    * Rashmi  
      * Win and loss  
    * Fabian: Performance and latency.  Normally by design should improve participation metrics. Maybe cost    
      * Want private agg api and rt monitoring api  
    * David: Participation rate. In B\&A, component or top level seller controls how much data for each buyer is sent from device.  Do we have visibility in how much we are excluded  
    * Fabian: This is an important metric  
      * Number of times we are excluded per rationale (ex. Ig too big)  
    * David: Participation rate is had IG on device, could run bidding script.  But you could participate but not with full list of IGs and you only get a small percentage..hopefully prioritized by bidder.  Need visibility in this.  
    * Fabian: Not sure this is available today, but yes, we need this.  IIUC each buyer can be max of 2KB.  I want to be able to prioritize and A/B.  Should be target for 2025 to be able to measure this and conclude upside of B\&A and make decision on what to use.  
    * Akshay: Question around perf metrics.  How do you measure them today on device.  Via private agg?  (latency, etc).   
    * Fabian: Need to check what they can measure and share.  Want to measure latency and no easy way to measure.  Would be nice if chrome could implement something.   
    * Akshay: want ability to measure like on device.  How do you do it on device  
    * Fabian: latency is tricky because only top level seller has the insight.  What we measure today is e2e all the way to display.  Clear increase for on device auctions.  
      * E2e is from time to bid to display  
      * Big topic  
    * Rashmi: do ou want to slice some fo the performanc emetrics  
    * Fabian: Yes.  Quesiton is what can be exposed by chrome.  Extent is limited by what Chrome is willing to exose  
    * Brian M.: Most narrowly scoped context which can be provided.  
    * Akshay: On server side \- many metrics that are collected. [https://github.com/privacysandbox/protected-auction-services-docs/blob/main/monitoring\_protected\_audience\_api\_services.md](https://github.com/privacysandbox/protected-auction-services-docs/blob/main/monitoring_protected_audience_api_services.md)	  
      * UDF execution latency  
      * In server latencies.  
      * 50-60 metrics discussed in explainer  
      * Not apples to apples with Chrome, limited to just server side.  
    * Fabian: wil look. Would like to compare with what we have today wit RTB vs. On device  
      * Reiterate: need to A/B test \- closest to apples to apples as possible  
* Multiple bidding scripts and signals keys  
  * Dan: want to specify generate bid per ig  
  * Fabian: want to a/b test bidding script on half IG for example  
    * Coudl do one bidding script with condition inside?  
  * Dan: in top level auction config, pass in new generateBid version 2 (example)  
    * Roll this out to certain number of servers  
  * DavidD: how do you know if the top level seller   
  * Jaspreet: it will be component level auction config   
  * Fabian: Should be buyer controlled   
  * BrianS: clarification on the requirements:   
    * AB testing   
    * How we do AB test option would be,  
      *  I want this set of IG to execute all server  
      * I want half of generateBid function to the other half   
  * Fabian: Want both for contextual split, user split  
    * I cannot do both today   
  * Arun: are you looking for complete separate generateBid?   
    * Fabian: I cannot bc no control on the IG, embedded with server   
    * Arun: User level (IG) & contextual level control (per buyer signal)   
      * Multiple generateBid?  
        * Fabian : want to use a separate bidding script, Separate generateBid scripts  
        * Brian: Choosing AB testing based off on TEE   
  * Dan: What we have today is per request will run the same script, but can specify which script per request   
    * Fabian: but if it is seller controlled, not useful, needs to be buyer controlled, user level split   
      * Dan: makes sense, but the downside is that you will need to wait \~1 hour to update the script   
    * Fabian: but want to measure business level script even if it is testing broken level split, could be used for shardding as well   
    * Brian: are you saying you want to shard with different kv deployments?   
      * Fabian: Yes, and it’s possible on device today 

      

      

Chat:   
Fabian: https://github.com/WICG/turtledove/issues/909