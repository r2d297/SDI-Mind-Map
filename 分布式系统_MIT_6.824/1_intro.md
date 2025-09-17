You probably noticed,
I put up the here on the, on the my shared screen, the part of the web page,
most of the class is driven from the schedule,
I'll talk a little bit later about it,
but, you know hopefully you find the url and you found the schedule.
And I'll return to that a little bit later in more detail.
Okay, so what's the plan for today.
I'm gonna talk a little bit about, what is it the distributed system.
So what is it,
and maybe get a little bit of info historical context,
you know how distributed systems have developed over the the last couple of decades,
then hit a little bit on the course structure, what you should expect,
then talk what are the main topics or the main recurring topics that we'll see throughout the term.
And then we'll see actually the first illustration of those main topics
by the case study that was assigned for today, the paper mapreduce,
which is also the topic of the first lab
and you watch the Piazza,
you know we just posted that a lab on piazza, the url,
so you can go and due next next Friday.
Alright, so let's start with the basics,
talk a little bit about what is distributed system.
And sort of you know maybe easier to start with a little picture,
the Internet cloud,
you know we have [] connected to, with clients, and maybe servers,
maybe you have servers that actually are complete data centers,
clients,
and the data centers themselves, you know maybe internally distributed systems,
that are connected by internal networks,
the data centers themselves might be internal connections,
you know outside of the Internet,
that servers, a large collection of computers connected by networks,
and you know sort of informally you know the way I think about it,
what a distributed system is
as a multiple you know more than one computer networked,
you know, so they can interact only through sending or receiving packets,
as opposed to say a multi-processor,
where you can interact from share memory,
and they're cooperating to deliver some service.
Those are the four key words,
that define for me distributed systems.
Often, you know you might not be aware the interactivity of the distributed system,
you know you might be using some clients,
for example the Zoom client,
but at the back end of the Zoom client,
you know there are huge data centers or multiple data centers
supporting actually this particular distributed application.
And in some ways,
you know we wouldn't be having these Zoom lectures,
if there were more in the,
you know there weren't distributed systems
and, so they often perform the backbone of the infrastructure that supports applications.
Okay?
So why are distributed systems interesting
or you know what, what are the main sort of use cases for distributed systems.
And those are broadly speaking,
there are basically four main reasons.
One is to use connect physically separated machines,
you know you might have,
we're involved all of us or any of us,
as we saw in the introduction,
or in different locations
and we get you know we're connecting with our laptop or our phone or our iPad,
you know to some server,
that actually sits in a completely different part of the world.
That's probably the [] basic reason why you care about distributed systems,
because you know just want to have two machines that physically separated in space
and you want to connect to them,
and once you can connect them,
that has an additional benefit,
that it actually may allow sharing between users.
So if you and I can actually connect to the same computer,
then actually we can start sharing data,
and you know that enables all kinds of you know collaborative possibilities
and you know what it is, like file sharing,
you know whether it is sharing of screens,
you know whether it's sharing of computing infrastructure
and it's all enabled,
because we can connect you know to physically separate machines.
There are probably a very important reason,
but a couple other really important reasons.
One is, to another one is to increase capacity, you know through parallelism,
and you know the paper that we assigned for today,
what is the topic of the first lab,
the mapreduce paper,
there was a good example of that,
but the other example is
for example there are many many Zoom sessions going on at the same time,
you know zoom.com has some support at all,
and it requires a lot of computers to basically increase the capacities
and to support all those in parallel Zoom sessions.
Another important reason is to tolerate faults,
so, for example, you know because computers might be physically separated,
you know one part can go down,
and hopefully won't affect another part, of the another part of the service,
so that the service can always be delivered,
so you can get high availability,
we'll see that as a major theme for this class.
And then the final one is going to be,
you know also sort of takes advantage of a physical separation,
which is going to achieve security,
for example if you have, you have a very sensitive service,
the service to manage passwords for your customers,
you know for logging to your service,
you would like to really guard that one machine,
then not shared with anybody else,
or not share any other application, run any applications on it,
so you have very narrow interface to that machine
and it allows you hopefully you get better security,
because you just have to protect one small interface,
and so by putting things on separate computers, isolate them,
you know you might actually be able to,
it's a good stepping stone to get security.
These are major reasons, main four reasons,
I think why one wants to, why distributed systems are popular.
I'm gonna talk a little bit about,
giving a little bit of historical context you know for distributed systems,
and where the [] came from,
and what happened over the, over the decades actually.
And you know sort of basically sort of the distributed systems,
as we sort of now look at them or the way we recognize,
they probably started around the same time that local area networks happened,
from year you know I think early 80s.
And so for example you would have a campus network at MIT,
and connecting for example the workstations, like Athena clusters,
to the Athena servers, like AFS,
and so that was sort of a typical distributed system at that point,
AFS also dates from that period of time,
of course, you know Internet was there too,
but there was really not sort of large-scale Internet applications,
the way we you know are using them now,
and so the main sort of Internet scale type distributed systems was DNS, the domain name system,
we still use
and basically email.
And so when I early in the early days, when I learn distributed systems,
and those are basically the main examples,
that we had to discuss.
Now things have changed quite dramatically,
since the 1980s,
and the importance of distributed systems has tremendously increased,
and one you know significant point,
it was data centers,
you know the rise of data centers, right, that went along with basically the big websites.
And here we're talking sort of the roughly speaking in the 1990s or early 1990s.
And so what happened basically is that,
you know somewhere in the late 80s,
you know 80s, the government or congress allowed commercial traffic on the Internet,
and basically resulted in boom,
where you know start getting big websites,
that were supporting large large number of users.
And you know the applications from those times,
like for example you know web search,
you know being able to search all the different web pages,
that actually were on the on the world wide web,
you know shopping and.
And so these applications you know gave rise to two sort of things,
one huge datasets,
you know sort of indexing to support web search,
have the index all the web pages on the Internet,
so that mean like gather crawl all web pages,
then compute reverse index,
and then you could use that for your search engine
and that was sort a tremendous amount of data,
that didn't fit on one computer,
and the amount of computation to actually do the first indexing,
you know there's also too much for the same computer,
as a result, you know data centers came about,
you know companies started,
putting lots and lots of computers in data centers,
so that it can support those kinds of applications,
so that's one lot of data.
And the second one is just a lot of users,
not uncommon for, you know big upside websites have hundreds of millions of users,
and this requires a lot of machines to actually support all those users.
And so we see tremendous amount of innovation in the period of time,
we're still continuing,
and some of the papers that we read, like the mapreduce paper
actually sort of started from that period of time.
That whole thing sort of sort of accelerated development accelerated
with emergence of cloud computing,
and that early whatever mid late 2000s,
and so here where we see a move were users or customers,
basically move their computation and data to data centers,
you know and by other people,
like Amazon Google Microsoft you know you name it,
and so a lot of the computation daily computation of people
just used run on their desktop or on the laptop,
just moves inside of the cloud computing,
and application change,
all instead of like running an application on your local computer,
you run actually the application inside of the cloud.
And that means you know that these data centers can have to grow further
and support new set of applications,
not only that, you know the customers that were outsourcing their computing to cloud computing,
also started to run large websites themselves,
and do gigantic computations on themselves,
you know machine learning a large datasets or any other kind of type of computation,
and so you see is that,
you know the users themselves wanted to build large-scale distributed systems,
and that means the cloud providers,
they're starting building a lot of infrastructure,
to allow other people to scale up you know their distributed systems to a large number of machines,
and achieve high parallelism, high performance
and store lots of data.
And so as a result, you know the current state is basically that's,
you know it's a very active area of research,
as well as in development.
In fact, you know so hard, so active,
that is difficult you know to sort of keep, keep up to date,
there's a lot of developments,
and you know even in this class,
we're going to spend a full semester in distributed systems,
we're going to only be able to sort of look at
you know a number of small fraction of all the stuff,
all the kind of distributed systems actually that people are building in practice now.
One thing that is cool for us,
you know as you know the teachers or students who for the distributed systems is that,
the people that build these data center early on,
even though they were building distributed system for their own internal infrastructure,
they publish papers about it,
and we can read those papers,
and so in fact during the semester,
we'll read a number of those papers,
that were built by people, that really have large-scale distributed system challenges,
and we can see how they were solved and learn from them.
This accelerated even more with cloud computing,
where you know in the early days of data centers,
many of these services were internal,
for you know the you know Microsoft Google or Amazon or Yahoo for themselves,
with the rise of cloud computing,
these services became public services that were used by other people,
and so suddenly there's even more sort of system infrastructure,
that is well documented and usable,
and so we can even we will study some of those cases too.
So if you look over these four decades,
you know tremendous rise,
you know of the importance of distributed computing,
as I said very earlier,
I did my doctoral thesis in distributed systems actually somewhere in the 1980s,
and it was like, it was an important field,
but not, it didn't blow me away in terms of significance
and and practicality you know sort of limited to more of these [local area clusters].
Now you know just like completely booming research field and development field.
Any questions a little bit about the historical context for distributed systems?
Okay, let me talk a little bit about the challenges,
and many of them you're gonna face head on in the labs.
So, so why is it hard,
and worth you know basically spending a semester learning about you know distributed systems.
There's sort of two things that drive you know the complexity and why distributed systems are hard,
one is there are many concurrent part.
These data warehouses,
you know today the computer is gonna run you know ten thousand, hundred thousand computers in parallel,
sometimes know all on the same job,
we've seen that mapreduce paper today,
which is like from the early 90s,
you know 2000 machines trying to work on one single problem,
so there's a lot of concurrent,
you know a lot of concurrent software,
a lot of things happening concurrently,
it's very hard to reason that through,
like what and and understand why you know things are correct.
And this is compounded by the fact,
that distributed systems must deal with partial failure,
so, you know one of these machines actually might go down,
but that doesn't mean that the whole [competition] stops,
in fact you know the rest of the machines probably, hopefully can continue running,
and maybe you know take over some of the responsibility of the machine that failed.
But this drives you know these two things together, basically drive complexity,
it becomes harder and harder to reason about why you know the system actually is working,
and particularly partial failure makes things very complicated,
because one system, one part of the system might think that another part of the system is down,
but it's not really the case,
you know the only thing that might actually happen is that,
there's a network partition,
and so both sides of the distributed system you know basically keep on computing,
and maybe interact with you know clients,
maybe even interact with the same set of clients,
because the clients can talk to both parts,
but you know the two in a half cannot talk to each other,
and so this, this is a problem known as the split-brain syndrome,
and that makes you know designing distributed systems and protocols distributed systems are complicated,
as we'll see.
So it's really sort of deep intellectual problems here,
then I find sort of really aspect in terms of challenges,
it's actually tricky to realize the performance benefits,
that in principle are possible with distributed systems.
So far,
we've been talking like you want to increase the capacity
or you want to run things in parallel,
you buy more machines
or you know buy another data center,
and you know of course only when the task is complete [] in parallel,
does that work,
and often in practice, this is not the case,
and so actually achieving that sort of high throughput,
and throughput scaling with the number of machines,
turns out to be not straightforward at all.
Sort of brings me to here next topic,
why you takes 6.824
You know, so I think for four reasons,
one it's interesting,
it's like hard technical problems,
and with very powerful solutions,
so hard problems, but powerful solutions,
we'll see you know those solutions you know for the term.
Second reason is you know used in the real world,
and there's a normal amount of appetite for people,
that actually understand and can build distributed systems.
If you were a grad student or undergrad thinking about research,
it's a great area,
because it's a very active area of research,
there are still many open problems,
and as we go through the semester, will encounter them,
so it's a good area for research.
And finally, if you like building things,
it's sort of a unique style of programming,
and so, in the case of 6.824,
you're gonna get hands on experience with that,
by building you know distributed app and distributed systems in the labs,
and you'll discover it will be,
one it's hard to get them right,
and you know it builds up another skill, type of skill of programming,
that you might not have done in the past.
Let me pause for a second here and see if there are any questions,
also feel free to post in the chat,
I'll try to monitor chat,
if there are questions there,
or you raise your hands,
if you have any questions,
and I'm sure the TAs will also be paying attention to the raising hands at the chat,
so in case I miss something,
you know they'll remind me.
Any questions so far, everything is crystal clear?
Oh, interpret the silence is things are crystal clear.
So let me talk a little bit about the course structure,
after this sort of quick introduction to distributed systems.
So the course structure is as follows,
we have lectures like the one today,
basically focuses on big ideas,
the lectures are typically driven by a paper that we'll seen,
and these papers are often a case study,
a particular big idea that we're covering in lecture,
and we, the papers are all published or posted on the schedule page,
and for most papers,
we ask you to answer a question as well as ask a question,
and we'll try to cover those questions or answer during the lecture,
and so it's important,
you know part of the reason we do that is,
because we'd like you to read the paper in advance of the lecture,
so that we can go a little bit deeper into these papers,
so, I strongly encourage you to read them before class.
Yeah, so another component of the classes, the labs,
the programming labs, there are four of them,
they're split in parts,
but four four major ones.
One is the mapreduce lab,
that we just posted today and it's due next Friday,
where you build basically your own mapreduce mapreduce library,
as similar to the one that actually described in the paper.
Second lab is a lab focuses on replication,
in the presence of failures and partitioned networks,
we're going to implement replication, using a protocol that's called raft.
And this is a lab that consists of multiple components,
but at the end of it, you know you have the library,
that you can use to, what's called you know as you used to build replicated state machines,
namely replicating state machine or multiple machines,
so that if one of them goes down,
one of those machines goes down,
then the service actually keeps running,
and you're gonna use that library to actually build a replicated service,
and in fact, you're going to be able to replicated key values service in lab 3.
And lab 3 is going to basically use multiple machines,
you know for fault tolerance, for applications to build one service,
unfortunately you know as well we just see a lot more,
is that just replication doesn't give you more performance,
you know because these machines actually have to perform a particular order.
And so to actually get performance,
were in lab 4, you can build the sharded key value services,
and that basically consists of many instances of lab 3,
so running concurrently and basically taking care of a part, or a shard of the key value service,
and so that you get parallelism,
and so you can actually use this to actually drive throughput,
and furthermore, we're going to actually move you know keys or key value pairs
from one machine to another machine
in response to what load changes.
So the labs basically labs 2 3 and 4 built on top of each other,
so you have a bug in lab 2,
that might affect you actually in lab 4,
we provide test cases for all of them,
so all the test cases are public,
and we grade you in those test cases,
so you submit your solution,
we run the same test on our computers,
double-check you know you're passing the test,
and if you pass all the tests, you get full score,
it turns out you know these are these test cases are tricky,
and we'll try to take all kinds of corners in your systems,
and so it turns out they are actually reasonable hard to pass,
and so, and they're tricky to debug,
you might actually happen in particular corner case an error,
and it may be very difficult to track down,
when does that happen, why does it happen,
so you know how to fix it,
and so my advice to you is to start the labs early,
it's often the case,
that you know you just start the night or two nights before,
you're going to have difficulty passing all the tests,
because you're gonna get stuck, you know trying to debug one particular aspect,
and run out of time to basically get the other test cases to work.
The, there's an optional project,
so instead of doing lab 4, you can do a project,
and the idea of the project is that,
you can work together or collaborate with a group of two three students,
and do a project on your own,
and the projects are a former similar type systems,
that we read about in the papers,
you propose one that you would like to build,
we'll give you some feedback,
and we'll tell you, well maybe you should just do lab 4,
but if you are excited about doing project,
we certainly like to stimulate that,
and you should start thinking now,
and then hopefully we can have some discussion,
and settle on something that will be cool to do.
Okay, finally, the one other component of the course is actually two exams,
one roughly halfway the semester,
and one in the finals week,
and we expect you of course you know to do all the labs,
and submit read write homework questions for the papers,
and do the two exams,
if you look at the web pages for 6.828, 6.824,
you'll see exactly the balance in terms of grading for the different components,
you know the labs count for most,
the two exams I think are 20 or 30%,
and then some class participation,
but the details are on the web page.
To get you through the semester and help you along,
we have excellent course staff,
we have 4 TAs,
we're running office hours,
and to help you basically get to the labs,
let me do a quick round,
maybe the TAs can introduce themselves,
so you at least know who they are.
Lily, you wanna go first?
Sure, so I'm Lily, I am a third year grad student in PDOS,
and Frans is actually my advisor,
so I know just how good he is in teaching,
so you're in for a treat,
yeah, I'm looking forward to working with you this semester,
I'll pass it off to David.
Everyone, I'm David,
I'm a second semester student,
I took 6.824 last Spring,
when it was like half in person and half remote,
so hopefully we can get the best of [] for this semester,
I'm excited,
yeah, but Jose.
I'm Jose, I'm a fourth year graduate student,
working on machine learning problems,
I took this class my first year as a grad student,
and I really really enjoy it,
so yeah, looking forward to Cel.
Yeah, I'm Cel, I used the pronounce,
I'm a first year master student in PDOS,
like some of the others,
and I took this class few years back,
had a great time taking it,
so I'm excited to help everyone learn it.
Okay, thank you,
so there's a question in the chat,
how is distributed system, how does distributed system with the lab run,
is the machine systems simulated,
yes, we're basically simulating many many machines by running many many different processes,
in fact the labs have their own RPC library,
that like pretend you know you're running on separated physical machines,
but in fact, you're running many many processes on the same machine.
Okay, any questions so far,
before I continue into the direction of actually some technical content.
Is the, the result of lab 4,
is it similar to any existing programs that exist?
Yeah, in fact you know what would be building
has a lot of similarity to sort of popular key value services,
you know think redis or you know some of the other ones,
you know there will be differences,
as we discovered, when we go through this semester,
but the key value services are pretty well-known,
and common a service inside of data center,
and run by many companies and a couple very popular ones,
that use with lots of people,
and they basically struggle with exactly the same issues
as you are going to be struggling within the labs,
we're going to build one that actually has pretty strong semantics,
something a little bit stronger semantics than some people execution practice,
and we'll discuss why, why that happens too,
but yeah, it's very close to what people do in practice,
raft is widely used in practice, for example.
Any other questions?
Yeah, it's a question about the labs again,
if we have a bug on lab 2,
that maybe doesn't even get caught by the testers somehow,
would do we get a like answer to the following labs,
or do we just continue to use our code.
Yeah, you're going to continue using your code,
and we did our best to make the lab, the test as good as possible,
and but I'm sure there are cases that we hard to complete the job,
and you know every time we discover something we missed,
and we basically improve the test,
so you're building, once you pass the test,
we're optimistic that you actually have an implementation,
that actually can support the other use cases,
that we're doing the rest of the semester.
It's not uncommon for people to rewrite rewrite their implementation once or twice,
as you will see in lab 2 and lab 3,
you know the structure,
you have to spend quite a bit of a time
thinking about the structure of your application or your library,
and you know as you've learned,
that you may want to go back and redo it.
To help you along a little bit,
this year we're doing something different than we've done in the past years,
I'm going to run a couple of Q&A lectures,
where I'll share, we'll share our solutions with you,
or we'll walk through our solutions,
and hopefully that will tell you a little bit about,
you know you can learn from that,
and see how that contrasts with your own solution,
and maybe pick up some ideas for future labs.
Any other questions?
Okay?
Again, interrupt me at any time,
I'd like to make this more interactive,
we'll take probably a couple lectures,
but hopefully we'll get there.
Okay, I want talk a little bit,
you know sort of set ourselves up for the case study for today,
but before doing that,
I want to talk a little bit about a bit of perspective for the class,
our focus in the class is going to be on infrastructure,
and you can more or less can tell that from the lab,
that you know were we just discussed,
and so there's going to be somebody
who's writing applications on these distribute systems,
and we're not really concerned too much with the application at all,
we're going to be mostly concerned with
the infrastructure that supports these applications,
and the infrastructure falls out in three different categories,
or very broad speaking,
storage infrastructure, like key value servers, file systems, that kind of thing.
Computation you know frameworks, to actually orchestrate or build a distributed application,
for example again is the classic example is mapreduce,
we'll talk about in a second.
And then that's the third category is communication,
and we'll spend less time on communication,
it's almost more topic 6.829 network systems,
but it will show up,
you know in the sense,
you know there's gonna be some contract between the network system and the distributed system,
and that will be a serious topic,
for example first day, we're gonna be talking about remote procedure call RPC,
and that's like the building block on which all labs are built,
and that's a communication model,
and the questions there are,
what kind of semantics does actually the RPC system provide,
utmost once, exactly once, at least once,
and we'll talk about that in Thursday's lecture,
but that's where sort of communication and distributed systems you know intersect.
If you look at these three,
so basically storage, you can store data durably,
you know computation to run computations
and communication to actually have these different pieces communicate with each other,
and so those are the three basic things,
that sort of, which we build distributed systems.
And what we're looking for are sort of abstractions,
that have been proven to be very helpful in building distributed systems,
there are abstractions, like like remote procedure call or like mapreduce library,
or in a storage system, like a key value service.
And often you know often our goal will be,
to make the abstractions, distributed abstractions
look very much like you know sort of normal standard sequential abstractions,
you've made familiar with,
so for example we build a storage system,
we want our basically distributed storage system
more or less behave like a single machine sequential storage server,
like your regular file system on your laptop,
except you know that you know,
we hope that the storage system is more fault tolerance,
because they use replication,
may be much more high performance,
because it has many many machines,
like the behavior of the system that we're looking for is similar,
the abstraction that we're looking for is similar to a single one.
Turns out in practice actually is very hard to achieve,
and you will see that,
it looks like, but it's not exactly,
and this is a topic that will show up multiple times.
In fact, you know that brings me to sort of like the main recurring themes in this class,
that we're going to see over and over.
And the main topics are fault tolerance, not surprising,
and that has sort of two aspects,
it's actually to define a little bit what fault tolerance means.
One is availability,
so we're looking at techniques,
we're gonna be looking at techniques to make a systems highly available,
and so and what we mean that is that,
they, they continue to deliver their service despite there being failures,
and so this is often expressed as a number of 9,
0.999 reliability,
and so that's gonna be one aspect of fault tolerance.
The second aspect of fault tolerance, that we care a lot about,
these we're going to call recoverability,
when the machine crashes or fails,
we like to bring it back into the system once it reboots,
you know so that we can keep up the availability,
because we didn't like repair the system,
then basically all the machines would down one by one
until we have zero machines
and then we have no service anymore,
so it's important that we repair the distributed system,
the way we repaired to the distributed system is,
basically when the machine comes back up,
you know we're gonna needs to recover its state,
and then we're going to start participating back into the distributed systems,
and it turns out, there's actually hard,
that's a hard aspect.
And key technique for availability is going to be replication,
and the key technique that we're going to use for recoverability is
basically something like logging or transactions,
writing things to durable storage,
so that you know when the power goes out,
but the machine comes back up afterwards,
you know were have the data is still there on disk,
so that's the fault tolerance side.
The second part is something of called consistency,
this is basically the contract,
you know that the servers is going to provide for operations
with respective concurrency and failure,
so loosely speaking, you know what we, when we think about consistency,
basically the ideal is the same behavior as that a single machine would deliver,
so we have a replicated fault tolerant high performance file system setting on many machines,
would like the behavior to be almost identical to the sequential machine,
and so the key question which here is sort of the form.
Let's say we have a key value server does get operation,
return the value of the last put,
and if you run a single machine,
and you have nothing you know concurrent operation,
so you run every operation one by one,
like you do put put put,
then get, then get, then get,
then of course like you know this is this question is trivial to answer,
you would assume that the get will return the value stored by the last put,
but once we have concurrency and with failures,
and we have many machines,
this is actually not so obvious,
you know what the right what the right way, what a good contract is,
and we'll see actually many different contracts,
we see ones that have strong consistency,
you know almost behave like a sequential machine,
or ones that have a very loose guarantees,
and provide very different [],
for example they provide eventual consistency,
you know eventually you will see a get will return the result of a put,
but not immediately.
And the reason, there's sort of different types of consistency,
that's directly related to performance,
you know often one of the goals of distributed system is to deliver high performance,
you know scale for example with a number of machines,
and you know to achieve a performance,
that's sort of almost in conflict with you know consistency and fault tolerance,
you know to actually achieve strong consistency,
requires communication between the different machines,
which might actually reduce performance,
similarly, to achieve fault tolerance,
we need to replicate data,
means we have to communicate data from one machine to another machine,
and if we were write, write that machine data also to durable storage,
you know that operation is expensive,
and so the replication cost the performance.
And so achieving these are three things at the same time,
it turns out to be extremely difficult,
and the fact that people do in practice is,
they make different tradeoffs,
they will sacrifice some consistency to get better performance,
or maybe some fault tolerance that get better performance,
and so we'll see, throughout the semester,
a wide spectrum of different types of designs,
that you know make that tradeoff in differently.
Just a small note of performance,
there's two aspects to it,
like one is throughput,
so you buy more machines,
hopefully the throughput scales with the number of machines,
but there's another sort of part of aspect performance,
basically much harder to achieve,
which is low latency,
and this is particularly important in these websites,
where you have thousands of thousand machines,
and you know maybe one user request when you click on a url,
actually costs a lot of these machines to participate,
and if one of those machines is very slow,
you know, maybe it has some mechanical issues,
where maybe the disk is not working a hundred percent,
or some other aspects weren't just really really work well,
that one slow machine can cost the whole user experience to be slow,
and this is often referred to as tail latency.
And as a concern, that will show up over and over you know throughout the semester,
as we discuss different machines,
and even shows up in the today's paper, the mapreduce paper.
So one other final topic that will show a lot,
at least in the class,
particularly the lab is implementation aspects,
and here goes really how to manage you know concurrency,
how to do remote procedure call implementation,
and just building distributed systems by themselves,
gonna have actually a serious implementation challenges,
and that will come over and over and over throughout the semester.
You know partly it's because,
we want to achieve performance, consistency and fault tolerance,
and depression crashes crashes in concurrency,
which makes [disk] drive complexity.
So those are the main topics,
any questions about this part?
Okay, then let's sort of dive in,
and look at the first case study,
and through the mapreduce paper.
And there's an illustration of many of the topics in 6.824,
you know we're gonna be talking about fault tolerance,
we're going to talk about performance and tail latency,
all kinds of issues that actually we see through the semester,
and we'll see one [cut] or one system that deals with that.
So good illustration with many of the topics,
the paper also very influential,
although Google internally doesn't use mapreduce described in this paper exactly,
you know they have you know systems directly derived from this mapreduce system,
that they are still using day-to-day,
there are other libraries that look a lot like mapreduce,
that are widely used,
and it also inspires different types of computational models than mapreduce itself,
and we'll see one or two more later in the semester,
so hugely influential paper.
And then finally it is actually the topic of lab 1,
which is another good reason to talk about it.
Many probably have you have seen the mapreduce paper,
shows up in 6.033,
if you're an undergrad student at MIT,
otherwise you might have seen in other places,
and, but we're gonna go a little bit deeper than for example 6.033,
because you actually have to implement your own mapreduce library,
and and as always, when you implement something,
problems that you know you might not really thought hard about before,
you know certainly start popping up.
And so by the end of it,
you really understand that mapreduce.
Any questions?
Okay, let me give you a little bit of context you know for this paper,
so this paper is written by you know two engineers from Google,
very well-known,
and the context is sort of the early data centers,
Google has a search engine,
needed to build reverse index of the world wide web,
to basically allow users to query the Internet,
and these kind of computations you know take multi-hours to run,
in the you know process terabytes of data,
multi-hours computations, on terabyte of data, terabytes of data.
And so think web indexing web crawling all of this, particularly web indexing,
so one of the [] application,
in you know as Google you know build these sort of applications internally,
you know Sanjay and Jeffrey Dean, you know the two [],
you know they were very good at that kind of stuff,
but they discovered basically,
there are many other Google engineers
who wanted to write those kind of certain types of applications too,
they wanted to be able to write their own data analysis
over all the web pages that had been crawled,
and so, and they realize you know writing these kinds of applications is difficult,
because if you're running multi-hour computation at many many machines,
it is very likely that one of those machines will crash you know during that computation,
and therefore you have to build in some plan for fault tolerance,
and and you know once you start doing that,
basically requires that you basically have taken something like 6.824
and able to build these kinds of complicated systems,
and their goal was basically to get out of that sort of dilemma,
and make it basically easy for non-experts to write distributed applications.
So that's the motivation for this, for this paper,
and why you are very excited about it.
And so the approach they take,
that mapreduce take is,
it is not a general purpose library,
you can't take any application,
and use mapreduce to actually make it basically fault tolerance,
and so, it has to be written in a particular style,
namely using these map functions and reduce functions,
and those functions are basically functional or stateless,
and, but those are the programmer writes the sequential code,
and then hence these two functions, you know the map and the reduce function to sort of the framework,
and the framework, the mapreduce framework deals with all the distributed [].
So it will arrange that you know the application
or the binary for the programs are run on many machines,
or install on machines runs on many machines,
and deals with load balancing,
it deals with certain machines that are slow,
it will deal with the machines that crash,
so the application writer [],
who wrote the mapreduce function,
don't really have to be concerned about this at all,
and they basically get all that stuff, if you will transparently.
And again to make that happen,
you know the library actually not general purpose,
so for example you wanted to write a key value service,
you can use the mapreduce library,
because it's assumes a particular computational model,
and your application has to fit in that,
the computation model you know []
you know something that they saw a lot at Google,
which is like people wanted to do big data analysis,
on basically all the web pages in the world,
there are many types of computations that just have to process lots of data
and compute values based on that data.
So that's sort of the type of applications that mapreduce targets.
Any questions about the sort of context and the motivation for this paper?
Okay, let me proceed.
So, let me first draw a sort of an abstract view of what's going on,
and then we'll dive into more detail.
So, so you, you sort of need to have in in the background
and understand exactly how mapreduce work,
which is going to be very important for you when you're doing lab 1.
Is there's a bunch of input files,
you know whatever f1 f2 f3, let's say,
of course, there're going to be many, many more in Google's case,
but just for pedagogical reasons,
you're gonna and size, of the size of my display,
I just have three files.
And, basically every, for every file is processed by this map, by map function,
so one written by a programmer,
and you know produce some output, so intermediate output,
for example the classic example to discuss mapreduce is word count,
basically counting how many times a word occurs in the dataset,
or dataset consists of many many, many files,
so for example like you know we're running the word count function on file one,
and it will produce for every word a key value pair,
and the key value pair consists the key with the word and count 1,
if you know a appeared multiple times in this file f1,
you know it would be multiple record, multiple key value pairs you know a,1.
And so maybe you know this file consists of many words
going to maybe has a,1 and b,1,
so the file contains two words,
you know similarly,
you know the function map function does the same thing for the file f2,
and will produce some key values,
and let's say maybe there's only the word b appears in the file once.
And maybe you know f3, the map function also runs the file f3,
and let's assume,
let's just where the [] assume that a shows up once,
and you know word c shows up once.
So basically you know these map functions all run in parallel,
completely independent of each other,
and there's no communication between them,
on their input files,
so this is going to give us hopefully high throughput,
or you know [] scaled much much bigger datasets,
and they [produced] on these intermediate values,
these key value pairs,
a,1 b,1 you know b,1 alone or a,1 c,2.
And then, so the second step is often referred to as shuffle,
is that basically you know run reduce functions on basically each row.
So here we got the row all the as,
and we're going to run reduce function,
and then the reduce function basically takes you know the one key,
aggregates all the,
reduce function gets input, the key plus the aggregated values,
or aggravate the combined values you know from the different outputs of maps,
so in this case,
the reduce function would get you know two intermediate results,
both a key a and two values 1 and 1.
And in this case, in the case of the word count,
we just add them up,
and so you know it would produce the value,
you know key value pair a,2.
And we do basically we're doing, and basically what we're doing we're doing,
we're run reduce for every you know row,
and so this will produce whatever b,2,
and then simply on end c,1 for the last one.
And again, you know the, once we've done to shuffle,
these reduce functions can totally run independent with each other,
you know they can just process whatever row data they have,
and be done with it,
and so the only sort of really expensive piece,
and this is this shuffle in the middle,
where the reduce functions need to
obtain you know their inputs from basically every [mapper],
so when all the mappers are done,
you know the reduce function basically gets
you know needs to contact every mapper,
extract you know the output for,
the output for the map of that particular reduce function
and you know sort you know by key,
and then you know basically run the reduce function.
And so basically we're sort of assuming that,
as paper points out,
the expensive operation is really,
the shuffling of data between the mapper and reducer.
Any questions about this abstract picture?
Okay?
Sorry I have a question,
so, is there,
I know that not all problems can be expressed with in mapreduce stage,
but it is for example like sorting an array,
is it possible to.
Yeah, yeah, so sorting is one of the applications that they talk a lot actually in the paper,
and it would be it's something that's totally done with mapreduce,
so basically you split input files correct in many things,
the mappers sort their piece,
and then, they split the output, say like r buckets,
and then each reduce functions basically sort that particular r bucket,
that gives a total sort of file.
I see, okay.
And in this case, you know sort of interesting,
because basically the input, the intermediate values and the output are the same size,
and some other functions, like maybe the map function
will reduce intermediate state to something much smaller than the input size,
in the case of sort, that is not the case.
Okay, let's look at the paper,
actually you know get a little bit of sense actually how you [write] them.
Well, see if I can actually.
That's just annoying, lost my menu.
It's hold one second.
Okay, it's not so cool,
give me second to,
here we go,
So we go save.
Okay, here the mapreduce.
Okay, can everybody see this?
Okay, there's a couple questions,
let me postpone some of these questions,
for example see them we'll discuss in a second in more detail,
if I don't answer your question, please ask it again.
So the first thing I want to do is actually,
look at one of the examples in the paper of the map and reduce functions,
corresponding to the word count example,
that would be sort of abstractly discussed.
So here's the code for the map and reduce function,
you see that the map function takes key value,
the key is really not important here,
it's the document name, so f1 or f2
and string the value is basically the content of the file,
so all the words that actually appear in the file f1,
and it basically goes through,
you know the pseudo-code goes through the words at the file,
and as an intermediate value,
emits you know these, a,1 b,1 c,1 etc.
Like from the programmer point of view,
you don't really see these intermediate key value pairs at all,
you just write this one simple map function.
And then, the reduce function is also more or less expected,
you know the, it takes two arguments,
you know the key you're like a
and values in this case, word count would be 1 1 1 1,
which a number of times that the word a actually showed up in the intermediate output,
and basically what the function does,
it just goes over to iterate over the list of values,
and basically add 1, plus 1, plus 1, plus 1,
and then it's you know the final result.
And so that's basically you know you can see from this code, right,
like the programmer basically always write,
you know complete straightforward sequential code,
this application very simple, admittedly,
but the code for even more complex application would also be straight,
you know, the sequential might be more code,
but it would be straightforward sequential code.
And in this code, the programmer didn't really worry about the fact that at all,
the machines might crash,
you know there might be loading balance,
that's basically all taking care of the mapreduce library.
So as and so you know the hope,
and I think this has proven out to be true,
is this actually made with lots of lots of people to write distributed applications,
and process gigantic datasets, and like could no way fit on a single machine,
like for example, the whole world wide web.
Does that make sense,
in terms of you know what the programmer actually sees.
Okay, let's talk a little bit about the implementation.
So I'm using the diagram here from the paper,
so the, so we've got the user program,
so the user program is like the map and the reduce function that we just saw,
you submit the map and reduce function to the,
you link it with the mapreduce library, and then forms binary,
and then you give this to the Google job scheduler,
and it will basically find a whole bunch of machines,
and run what they call workers there,
so like you know scheduler will,
for example in the evaluation as we'll see in a second,
you know there are about 1800 machines,
on these 1800 machines,
you know the scheduler will run worker process,
that actually does the actual work,
and evokes you know map and reduce functions when when when appropriate.
There's one other process that is important,
in the paper they call the master process,
in the lab called the coordinator,
and the coordinator [] orchestrates the workers,
and hands jobs or maps jobs to them,
so like the terminology,
here is that a complete application is one job, mapreduce job,
and then reduce, identification of reduce or identification of map is what's called the task.
So you know basically you know the coordinator will assign files to a particular workers,
and the worker will then invoke the map function on that particular file,
and it will produce some intermediate results,
You know here the intermediate results,
those intermediate results are stored on the local disk of the machine,
that actually runs that particular map function.
And when you know worker has run completely particular map function,
basically tells the master, I'm done with that map function,
and you know it tells the master where the intermediate results are.
Then, at some point, when all the maps are basically done,
you know the coordinator will start running reduce functions,
and reduce functions will collect you know the intermediate results from the different mappers,
from the locations that are specified in the result the record,
retrieve that data, sorted by key,
and then basically reduce run,
invoke the reduce function on every key and the list of values,
and that produces an output file,
and that is the you know there's gonna be one output file per reduce function,
and you know you can aggregate the output file,
concatenate the output files to get the final output.
That's sort of the structure,
the input files live in a global file system, that's called GFS,
Google uses a different global file system now,
but you know the paper uses GFS,
we'll actually read about GFS next week,
and the output files also going to GFS,
the intermediate files don't, are not stored in GFS,
that are stored on local machines, where the worker is run.
Any questions about the sort of rough scheduler of implementation?
I have a question about the process [file] for the remote read,
so in the remote read process,
is the file actually actually transferred to the reducer?
Yes, so the, exactly, the,
so the intermediate results are produced or stored
on the disk of machine that runs the mapper, with that map function
and the reduce goes out,
and basically fetches it's you know set of keys from every mapper.
And so at that point, you know the data is transferred across the network,
so the network communication that happens is here,
the reason that there's little network communication,
no network communication here at all,
is because the workers,
the way the coordinator assigns files to workers is basically,
the worker is run on the same machine,
so every machine runs both worker process and a GFS process,
and the workers are basically send to,
or the map function run on a machine that actually has that file locally stored in GFS,
and so basically this actually corresponds to basically local reads
you know through GFS to local disk,
and then the files are produced or map are produced into intermediate files
are stored on local disk too,
so there's no communication happening in this part of the picture.
And then when the reduce functions run,
they actually retrieve files across the network,
and then write it out to GFS,
there's going to be some network communication here,
when the worker is actually produced the files in the global file system.
I have another question,
is the, is the coordinator responsible for partitioning the data,
and putting it on each worker or machine?
No, not really, the basically, the mapreduce run the user program,
basically saying like I want to run it on f1 f2 f3 f4 whatever,
all the input files,
and those input files live in GFS,
and so as part of the job specification,
usually say which files need to be processed.
Okay.
Sorry, how does the the sorting work,
does like who does this sort and how is.
The mapreduce library does a little bit of sorting,
before it hands it off to the mapreduce to the reduce function,
so, for example the intermediate results might have,
like basically all the intermediate results for keys a b and c go to one worker,
and you know there, you know there's just a whole bunch of key value pairs,
like a,1 you know b,1 you know whenever a,1 again,
you know c 1 whatever.
And basically what the mapreduce library does is,
it sorts first by key,
so first all the as together,
and then all the bs together,
and then all the cs together,
and then basically concatenates all the values from one single key,
and hands that off to the reduce function.
Thank you.
Okay, so I want to talk a little bit about fault tolerance now,
and so go back to.
Could I ask a question about the mapreduce paper real quick?
So is the larger idea the,
a lot of functional programming could be reduced to the mapreduce problem?
Yeah.
Okay, yeah.
Yeah, okay.
In fact the name hints that,
because basically there two you know the notion of map and reduce functions
is something very common in functional programming languages,
and use widely in functional programming languages,
or any sort of functional programming style,
and so the basically you know that's where the inspiration came from.
Okay?
So actually there's a good [] to fault tolerance,
because the the idea is that if a worker fails,
then the coordinators are in charge of noticing that the worker fails,
and basically restarts that task,
and so the coordinator reruns map and reduce functions,
Of course, coordinator itself doesn't rerun them,
but basically coordinator to says,
you know that particular map function needs to be run again,
because it appears to the coordinator,
that machine that it handed you know the task to actually is not responding,
and so difficult thing is like,
if the machine doesn't respond to some certain amount of time,
the coordinators are going to assume that machine crashed。
And so, and that means that when another worker becomes free,
and you know was looking for a new task,
and it will hand out the same task,
that had actually handed out earlier and handed out again.
And so that's sort of the basic plan for fault tolerance is that,
if coordinator doesn't hear about particular,
worker reporting back the task is done,
and we'll rerun the task again.
So an instant question is,
like can a map function, get a map run twice,
and even complete twice,
is it possible in this framework,
that you know a particular map will run twice.
I guess it is,
because if the machine is down,
you can't really tell at which point,
so how many of the map tasks that it executed,
during the specific mapreduce instance were actually completed,
so you would just have to rerun all of them, I guess.
Yeah, yeah, so mostly we just think about this one task at a time,
but, so machine like does one task,
then goes back to the coordinator asked for the next task,
and that might be another map task.
And so when the coordinater doesn't hear back,
it will say, like okay go ask another worker to run that map task too,
but it could be the case that is you point exactly out,
that the first worker the first machine didn't actually crash,
just happen to be a network partition
or like the worker coordinator was not able to communicate with the machine,
but actually it's just running happily and actually doing the map task,
and it can produce you know an intermediate set of results.
So the same map function can actually exactly run twice,
and so it's actually one of the reasons you know that map and reduce are functional,
is because, that's okay,
if it's a functional program,
if you run the same program on the same input,
if you run a functional program on the same input,
it will produce exactly the same output.
So there's really matter that it runs twice,
you know in both cases were produced exactly the same output,
and so this is where this functional aspect is actually really important,
it basically has to be functional or deterministic.
You see every run of this map function must produce the same output,
because we're going to use one of them into the total total computation.
So similar, can reduce function run twice?
Yes, I believe so.
Yep, exactly for the same reason,
I mean the machine runs reduce function is no different than map task,
there's really no from the fault tolerance perspective,
there's no really big difference between a map task and a reduce task,
if the machine running the reduce task doesn't report back,
but happens to also will finish the job,
another machine might run, be running exactly the same reduce function,
and they will produce output.
Now the only sort of interesting aspect is,
this is that both reduce function will write you know an intermediate
will write the final output file into GFS,
and if you paid attention to it,
you will notice that what they what they do is actually,
they first produce the file in an intermediate file in the global file system,
and then do an atomic rename,
to name, move the file or rename the file into its actually final name,
and because you know it's atomic,
you know one of the two reduce functions will win,
but it doesn't really matter which one wins,
because they're going to produce exactly the same outcome,
because they're functional.
So just to double check,
so, if we have a machine that's doing a map task,
so a single machine can do like multiple map tasks,
so let's say that it's doing like 10 map tasks,
and it's in the 7th task,
and then for some reason it failed,
and then the master knows that this machine failed,
so then the master will order for all of the 7 map tasks that were completed
to be re-executed distributedly,
maybe on different map machine, so.
Yep, except, you know it's right,
although I think it generally just goes one map at a time,
so basically one machine runs one map function or one reduce function not multiple.
Okay, thank you.
But after the workers done running the map task,
does it immediately write it's file somewhere that's visible to other machines,
or does it just keep that file in its file system for the time [].
It keeps,
map function always produce the results on the local disk,
and so it sits in its local file system.
Right, so then even if you were doing map tasks one at a time,
in the scenario, where you did multiple,
and then the machine crashed, you lose the intermediate work, right.
No, it's sit in the file system,
so when the machine comes back up,
you know maybe the stuff is there.
Oh, I see.
So the data is actually in store durably.
Oh, I see, okay.
And the map or the reduce function directly talk to
the map functions and the machines are actually have the intermediate results.
Okay, so let me talk quickly about a couple other failures,
and all the questions you're asking great question,
in fact, that it all will show up,
when you're actually implementing what mapreduce,
you'll have to decide exactly how you're going to do things.
So a couple other things,
can coordinator fail? I don't think so.
That's correct,
the like your, the cat,
the coordinator cannot fail,
so basically when the coordinator fails,
the whole job has to be rerun.
You know, in this particular implementation,
they have no plan for failures of coordinator,
that's what making the according more fault tolerance is actually a bit more tricky,
because it's actually a state,
state that gets modified,
every time a map function completes or reduce function completes,
and so it actually turns out to be more complicated,
and so basically, this particular library, the coordinator cannot fail.
We will see later in semester, techniques,
that we can use to make the coordinator fault tolerant,
if we wanted to,
but they decide not to do so.
One reason they decided not to do so is,
because a single machine,
they're hoping basically that,
the single machine that just runs the coordinators unlikely to crash,
while it's very likely that,
one of the thousands of machines that run some mapper will crash.
Okay?
How about slow workers?
Sort of another type of failure
to discuss the issue of where machines might be slow,
because like some other computations running on it,
like GFS is also running on the same machine,
maybe it actually is using a lot of the cycles or bandwidth,
or maybe there are like problems with the hardware itself.
Is there anything special that they do?
I think I recall reading something about,
when the job is getting somewhat close to finishing,
the coordinator will assign the remaining tasks to additional machines,
just in case there are like machines that are lagging,
and then they will take the results that finish first.
Yeah, exactly the slower workers are called straggler,
and what they do is like they sort of do backup tasks,
so for example when they're close to,
indeed you'll see,
when we go to computation almost done,
like say there's a handful of reduced task left
or a handful of map task left,
the coordinator actually just basically runs a second instance,
or maybe third instance of that task,
on a separate machine.
And it's totally okay,
that's totally okay to do so, correct,
because you know it's functional,
so it's no problem if we run the same computation several times,
because the it will produce we use exactly the same same output,
because it's given the same input,
and the hope is that one of these other guys will finish quickly,
and so therefore, then we were not the performance is not limited by the slowest worker,
but basically the fastest are the ones that got replicated.
And so this is only one of issues,
where like basically this is a common idea to deal with stragglers
to deal with tail latency,
is to try to basically replicate tasks
and go for the first that finishes.
Okay, I think this is time to wrap up,
so you can go to other classes,
but these are some of the major issues,
that show up in the mapreduce library,
and you will definitely be struggling mostly,
you know the hard part of actually implemented the mapreduce library
is actually doing the fault tolerance aspects,
and but you should keep in mind,
as you're doing that,
all the programmers that are using your library or would use your library
don't have to worry about all the distributedness,
that they would have, you have to deal with.
So you're in there unfortunate situation,
you're not the target of the mapreduce paper,
making your life of writing mapreduce application easy,
you're on the that side of the [equation] here,
you actually have to deal with the distributedness
and become an expert.
Okay?
I'm going to hang around for a little while,
so people want to go, feel free to go,
if you want to ask a couple more questions,
you know feel free to do so,
and I'll see you on Thursday.