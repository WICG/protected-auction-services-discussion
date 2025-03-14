# Protected Auction Services WICG Calls: Agenda & Notes

Calls take place on some Wednesdays, at noon New York \= 9am California.  Please check [https://github.com/WICG/protected-auction-services-discussion/issues/27](https://github.com/WICG/protected-auction-services-discussion/issues/27) for details.

That's 6pm Paris time and 4pm UTC (until the end of summer, when countries fiddle with their clocks).

Notes repository: [https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings](https://github.com/WICG/protected-auction-services-discussion/tree/main/meetings)

(This notes doc will be editable by everyone, during the meeting)

**Next meeting: March 12, 2025**

Google Meet joining info  
Video call link: [https://meet.google.com/htk-obgg-smb](https://meet.google.com/htk-obgg-smb)   
Or dial: ‪(US) \+1 509-676-3166‬ PIN: ‪117 463 428‬\#  
More phone numbers: [https://tel.meet/htk-obgg-smb?pin=4553130257370](https://tel.meet/htk-obgg-smb?pin=4553130257370)

*To join the speaker queue:*  
*Please use the "Raise My Hand" feature in Google Meet.*

# Attendees:

* Samantha Jung (Google Privacy Sandbox)  
* Arun Nair (Google Privacy Sandbox)   
* Ashish Bhardwaj (Google Privacy Sandbox)  
* Victor Pena (Google Privacy Sandbox)  
* Matt Kendall (Index Exchange)  
* Priyanka Chatterjee (Google Privacy Sandbox)  
* Brian Schneider (Google Privacy Sandbox)  
* David Roundy (NextRoll)  
* Andres Bordese (NextRoll)  
* Trenton Starkey (Google Privacy Sandbox)  
* Mihir Gandhi (Google Privacy Sandbox)  
* Fabian Höring (Criteo)  
* Shruti Agarwal  (Google Privacy Sandbox)  
* Peter Meric (Google Privacy Sandbox)))  
* Baris Metin (Google Privacy Sandbox|  
* Xing Gao  (Google Privacy Sandbox)  
* Michael Kleber (Google Privacy Sandbox)  
* Abishai Gray (Google Privacy Sandbox)  
* Viacheslav (Slava) Levshukov (Microsoft)  
* Bharat Rathi (Google Privacy Sandbox)  
* Daniel Rojas (Google Privacy Sandbox)  
* David Dabbs (Epsilon)  
* Alexander Tretyakov (Google Privacy Sandbox)  
* Michael Mihn-Jong Lee (Google Privacy Sandbox)  
* Akshay Pundle (Google Privacy Sandbox)

# Agenda

* Fabian Höring Any news on [https://github.com/privacysandbox/protected-auction-key-value-service/issues/66](https://github.com/privacysandbox/protected-auction-key-value-service/issues/66) ?  
* Viacheslav (Slava) Levshukov: BYOB with inference side car

**Note taker:** Samantha Jung (Google) 

## Notes

* \[Fabian \- Criteo\] Context around: [https://github.com/privacysandbox/protected-auction-key-value-service/issues/66](https://github.com/privacysandbox/protected-auction-key-value-service/issues/66)  
* 2 modes   
  * Bidding script and run java script  
  * Bring your own binary mode   
    * Not efficiently supported due to runtime,  
    * Take into account of the data already known running long post  
  * 1 proposal is to isolate all the workers, only process the IG \- looks like its in the works, so want to know the status   
    * \[Bill-Google\] how to run this securely, question is does this run randomly? For example, different order?   
      * \[DavidR- NextRoll\] timestamps, currently we do this with 30 sec, but nice to have directly in TEE, randomize bid    
        * \[Fabian\] But everything goes into generateBid    
        * \[Bill\] cannot override   
    * \[Brian-Google\] Today there are 2 UDFs \- Inference and generateBid in Roma  
      * There is no constraints on determine based on input today   
      * Event is to avoid side effects like caching, and potentially leak privacy   
      * Why is it okay Inference sidecar to have long running instances?  
        * Inference sidecar is more constrained than BYOB, therefore stateless   
        * To deal with this in BYOB, every request is processed with instantiated   
          * No explicit language   
      * Trying to reimplement private computing world, not there yet but we are trying to get there to support long running process   
        * Determine, randomize and sample   
      * Around C\# and Java   
        * Today: Java example on the ahead of time (AOT) compilation   
          * Does this work for you now for C\# and Java people?   
            * \[Fabian\] how does this work?  
        * \[Peter\] no experience with C\#, in linux, there are 2 options   
          * Publish single file \- tried it, can work in BYOB  
          * Publish AOT \- higher performance level  
            * [https://learn.microsoft.com/en-us/dotnet/core/deploying/native-aot/](https://learn.microsoft.com/en-us/dotnet/core/deploying/native-aot/)  
          * Native binary \- UDF, no JDM   
          * Internally depends on what AOT does   
          * Also depends on the performance as a UDF developer   
            * \[Fabian\] Matters Execution time, cannot work   
        * \[Brian-Google\] Our repo today has java with AOT execution, near native example, limitations as to what languages are supported in the compilation environment, but for Java AOT works well and AOT option available for C\#   
          * [https://github.com/privacysandbox/data-plane-shared-libraries/blob/e3e9e3419ebba9b700c5391425e8557a7148c2de/src/roma/byob/sample\_udf/SampleUdf.java\#L1](https://github.com/privacysandbox/data-plane-shared-libraries/blob/e3e9e3419ebba9b700c5391425e8557a7148c2de/src/roma/byob/sample_udf/SampleUdf.java#L1) \- Java Example  
            [https://github.com/privacysandbox/data-plane-shared-libraries/blob/e3e9e3419ebba9b700c5391425e8557a7148c2de/src/roma/byob/sample\_udf/BUILD.bazel\#L387](https://github.com/privacysandbox/data-plane-shared-libraries/blob/e3e9e3419ebba9b700c5391425e8557a7148c2de/src/roma/byob/sample_udf/BUILD.bazel#L387)  
          * \[Fabian\] will take a look, but nice to have an expert who can explain how this works on the benchmark and experience   
          * \[Priyanka-Google\] Question to Fabian:   
            * Quick research shows AOT would be faster than JIT  
          * \[Arun-Google\] Question to Fabian   
            * Is there an option where we have runtime work? Fast resets?   
              * \[Fabian\] Don’t know but would be nice  
            * Look into other directions like where we keeps memory but execution is not possible   
              * \[Fabian\] how long will all this take? Fetching the runtime seems like it will take a long time  
                * \[Arun-Google\] Research more on the AOT in parallel look into runtime support and provide input to us   
            * \[Peter\] we could start with minimal C\# program that handles BYOB protobuf, but it will be minimal and would be helpful if fabian evaluates   
              * If there is a confidence, we will support   
              * \[Peter\] Starting point: example, execution overhead is 10 ms, what number would that be?   
                * \[Fabian\] 5ms, will have a look, not sure at the moment, does not think that runtime, garbage collector works so would like the explanation  
                * Challenge is the real workload, and will test it out but believe that the outcome will not work    
* \[Bill\] Requirements, but there are ms of burn CPU time, and latency   
  * \[Fabian\] 20 ms e2e latency. Latency on B\&A looks good today but its not the same workload (lightweight on device workload)   
    * Most important are:   
      * Cost per CPU  
      * **QPS per CPU**  
    * \[Priyanka\] BYOB execution?   
      * \[Fabian\] Only cares about E2e right now, depends on how it is executed   
        * 20 ms   
          * \[Priyanka-Google\]  20 ms may be lower than your with RTB latencies.  
            * Ask to Fabian: Share some latency and throughput requirements for bidding server   
    * \[Peter\] clarification on the E2e  
      * \[Fabian\] Everything input, buyer front end   
      * \[Alex-Google\] Is it with p50?  
        * \[Fabian-Criteo\]  Yes, median value but will take a look but not official, server side not network   
        * \[Priyanka\] Entire buyer side median latency  
    * \[DavidR\] 5ms was also the number I was going to invent off the top of my head, no C\#   
* Viacheslav (Slava) Levshukov: BYOB with inference side car  
  * Option on how we can call it, in the future?   
    * \[Brian-Google \] Yes,   
      * \[Trenton-Google\] no timeline that we can share today, we will bring it back here once we have the updates   
        * Focus is on generateBid right now, no commitment on anything   
* BYOB service   
  * Feature extractor using the data, BYOB will be able to read in memory, save some time on the binary   
    * \[Peter\] Yes, on the roadmap   
      * \[Brian\] Large inline dataset \- it’s possible today, fast access to large, immutable set of data, local storage   
    * \[Peter\] What kind of size would work ?   
      * \[Slava \] Up to 1 GB    
  * \[Mihir\] primarily looking for this in generateBid   
    * \[Slava\] Yes, first execute feature, and send the results to the Inference service 

You

12:01 PM

[https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8\_EbPnzcptnhV9mxBP5Mo/edit?usp=drivesdk](https://docs.google.com/document/d/1Hk6uW-i4KPUb-u20E-EWbu8_EbPnzcptnhV9mxBP5Mo/edit?usp=drivesdk)

keepPinned

keep\_off

Unpin message

You

12:04 PM

Please update the attendees if you are just joining

keep

Pin message

David Roundy

12:04 PM

For some reason I can't edit the document today, so I just suggested my name.

David Dabbs

12:09 PM

Is everyone signed into the doc? Nice to associate entities to names.

Mihir Gandhi

12:10 PM

Thanks David, Samantha has fixed the permissions.

Brian Schneider

12:26 PM

aot is a "today", so worth a shot.

David Roundy

12:29 PM

5ms was also the number I was going to invent off the top of my head.

Alexander Tretyakov

12:38 PM

is that with network? p50?

