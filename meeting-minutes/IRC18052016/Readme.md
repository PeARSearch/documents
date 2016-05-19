<html>
<head>
<meta charset="utf-8">
</head>
<body>
<h1>Untitled meeting at #pears, 2016-05-18 16:53</h1>
<h4>Meeting started by gem</h4><ul>
<li><a href="http://arxiv.org/pdf/1509.02897v1.pdf">Practical and Optimal LSH for Angular Distance</a></li>
</ul>
<h4>Meeting ended at 08:36:15 UTC</h4>
</body>
</html>

**stultus**:  minipa, yeah. but I need 20 mins. on a hangout with the student I'm mentoring for GSOC :D

**minipa**:  ok! No probs! :)

**stultus**:  minipa, here :)

**minipa**:  stultus, hello! How are things?

**stultus**:  minipa, all is well :)

**stultus**:  minipa, that is a hindi movie dialogue btw :P

**minipa**:  :D

**minipa**:  I'm practicing for when we have our

**minipa**:  next PeARS meeting in India :P

**stultus**:  minipa, hehe

**stultus**:  minipa, I pined you the other day to ask you one thing.

**stultus**:  minipa, in shared pear ids

**minipa**:  yup...?

**stultus**:  minipa, each pear id is based on the indexed pages on that pear right?

**minipa**:  correct!

**stultus**:  minipa, so when each one of our pears start indexing the pages, the pear id will change

**minipa**:  Right, I think the name 'id' wasn't particularly well chosen...

**minipa**:  We should have one id which is the fixed identifier of that pear

**stultus**:  minipa, okey

**stultus**:  minipa, so if that is true, how can I calculate the new pear id?

**minipa**:  and one vector which is, well, its vector...

**stultus**:  minipa, yeah. what is the logic to calculate that vector?

**minipa**:  Ok...

**minipa**:  you have all the vectors for all the pages that this person wants to share. ok?

**minipa**:  And then, you sum them all together, and that gives you a representation for that person.

**stultus**:  okey. so this calculating vector part is not there in our code right?

**minipa**:  Yes, it is. In... hang on... I've forgotten...

**minipa**:  (minipa is looking for code...)

**stultus**:  okey

**minipa**:  Right, in mkProfiles.py (demo folder)

**minipa**:  https://github.com/PeARSearch/PeARS/blob/development/demo/mkProfiles.py

**stultus**:  minipa, okey. I will check this

**minipa**:  Oops. What is pears-bot doing??

**stultus**:  minipa, it is telling the title of the link :D

**minipa**:  Oh... :D

**minipa**:  stultus, did you have an idea about the pears ids?

**stultus**:  minipa, so mkProfile.py is adding up the vectors right?

**minipa**:  yes

**minipa**:  And doing some other stuff

**stultus**:  minipa, but when indexing, we have to calculate the vector of each page?

**minipa**:  yes...

**stultus**:  minipa, how can I do this?

**stultus**:  minipa, sorry that was the original question I wanted to ask :D

**minipa**:  minipa looks for code again :)

**minipa**:  https://github.com/PeARSearch/PeARS/blob/development/demo/runDistSemWeighted.py

**stultus**:  minipa, okey. now I see

**minipa**:  Well, this is the demo code. It runs on Wikipedia pages...

**minipa**:  Have a look at the README in demo/

**stultus**:  minipa, yeah I somehow missed to check the demo code :(

**minipa**:  The code is all there and would only need tiny modifications to run on whichever page...

**minipa**:  No probs :)

**minipa**:  It wasn't obvious :)

**stultus**:  minipa, okey. now one hypothetical question .

**minipa**:  ok...

**stultus**:  minipa, is it possible to create a single vector for a particular topic ? and classify queries based on the vector?

**stultus**:  minipa, for example vector1 for 'computer science' and tell 'computer keyboard' is related to vector1

**minipa**:  Sure, no problem.

**stultus**:  minipa, also is there any way to make a single digit/singlehash representation for a n dimensional vector?

** gem **: ants to listen to this one

**stultus**:  minipa, we are brainstorming about creating the unique identifier based on the vectors

**stultus**:  brb. someone knocked the door. gem please continue

**minipa**:  Yes, I think so. Although I've never done it. I think this is related: http://arxiv.org/abs/1509.02897

**gem**:  minipa, when we say a vector representing a topic or a pear, how should we expect its type to be? an array? a list? some other data type?

**minipa**:  As it is implemented, it is a numpy array.

**gem**:  minipa, Hello, btw. Hope yo\u are doing good. :-)

**minipa**:  Hi gem! I'm good :) You?

**gem**:  minipa, Great. Thanks! :)

**gem**:  minipa, So that is the problem we are hitting at the moment

**minipa**:  Ok... so...

**gem**:  minipa, we can't have an array represent a pear. we need a singular representation like stultus mentioned

**minipa**:  that indeed brings up the problem of having the id changing whenever the browsing history changes...

**minipa**:  yes :)

** gem **: akes note of issues to tackle

**minipa**:  but hang on...

**minipa**:  oh, hang on number 2... should we record this conversation with pears-bot??

**gem**:  ah yes!

**gem**:  yes!

**minipa**:  well done!

**gem**:  bows

**minipa**:  :D

**minipa**:  Ok, so we're talking about

**minipa**:  generating a representation for a single user.

**minipa**:  And it should be fixed, so we can't use the vector of that user.

**gem**:  The most obvious problem we have regarding the creation of DHT is this

**minipa**:  Yes, I see. Let me think just a moment...

**minipa**:  How bad would it be if that id did change, but only once in a while, like every year or so?

**gem**:  That is fine. we can update the ids stored in a couple of other pears in the DHT in O(logn) times

**gem**:  so shouldn't be that bad

**minipa**:  I'm thinking this...

**minipa**:  we create a vector which encapsulate the core of that person's interest.

**minipa**:  Then, perhaps they browse stuff outside of their main area but that doesn't get reflected in the vector.

**minipa**:  We check once in a while that they haven't completely changed their life

**minipa**:  ...

**minipa**:  hang on, I don't like it...

**minipa**:  just babbling away... :(

**gem**:  hmm... so the browses (s)he made outside his/her area of interest aren't significant to us?

**gem**:  think out loud :)

**minipa**:  Well...

**minipa**:  the point is that if a computer scientist spends her life on stack overflow...

**minipa**:  and once in a while visits a site on beekeeping...

**minipa**:  her pages on beekeeping won't be easy to find anyway.

**gem**:  makes sense, yes.

**minipa**:  Because the vector of that person will be heavily biased towards computer science.

**minipa**:  So...

**minipa**:  perhaps what we have to do is to decide what that person is...

**minipa**:  oh, hang on, I think I might have an idea!

**gem**:  is all ears

**minipa**:  We 'classify' that person in terms of a few topics. The person is a computer scientist, a beekeeper and interested in astronomy.

**minipa**:  The words 'computer scientist', 'beekeeper' and 'astronomy' are points in the semantics space.

**minipa**:  So we can create a new point which is the sum of those word vectors. That vector gets hashed and

**gem**:  oooh I like it!

**minipa**:  becomes the DHT representation of that person.

**minipa**:  Problem:

**minipa**:  how to ensure that everyone is unique.

**gem**:  actually we can make use of the key for this

**minipa**:  aaah!

**minipa**:  Problem 2:

**gem**:  we can hash the person, may be using his IP?

**minipa**:  Uh? But if we hash them using the IP, why can't we use their vector in the first place?

**minipa**:  minipa is confused...

**minipa**:  I thought similarity was calculated on the hash itself...

**gem**:  No no. we can use the vector.

**gem**:  The issue is the datatype of the vector

**minipa**:  minipa requests explanation for dummies...

**gem**:  right now, like you mentioned, the vector representing the user is an array, right?

**minipa**:  yup

**gem**:  how can we hash an entire array is the question.

**gem**:  we need one single representation for the entire array

**minipa**:  ah, I see!

**gem**:  thinks tuples are hashable in python, but that would make the DHT whole lot clumsier. Can't easily locate the buckets.

**minipa**:  Let me just take a look at that paper, quickly...

**gem**:  okay

**minipa**:  gem, stultus, this is too clever for me but I think it might be what we're looking for: http://arxiv.org/pdf/1509.02897v1.pdf

**minipa**:  can you make sense of it?

**gem**:  minipa, Let me go through this at once and see

**gem**:  #link http://arxiv.org/pdf/1509.02897v1.pdf

**17**: 12:25] LINK: http://arxiv.org/pdf/1509.02897v1.pdf [None]

**minipa**:  Also the python implementation: https://pypi.python.org/pypi/FALCONN

**gem**:  minipa, on a side note, we found something very similar to want we want for pears (for the DHT) https://github.com/bhavishya235/Distributed-Editing

**minipa**:  Ah, nice!

**gem**:  for our first prototype p2p network, we are trying to use this one. That's when this single representation issue arising.

**gem**:  is halfway through the introduction and she is totally loving the theory

**minipa**:  Also this: http://www.sciencedirect.com/science/article/pii/S0888613X08001813

**minipa**:  :)

**stultus**:  is back

**stultus**:  reading the logs

**gem**:  has to attend an early morning call tomorrow, so has to hit the bed now

**gem**:  Good night minipa stultus :)

**minipa**:  G'night gem! Sleep well! :)

**gem**:  minipa, :)

**minipa**:  stultus, don't know where you are in your reading... but do you think that python library could help?

**stultus**:  minipa, I'm reading that angular distance paper. will check the library and let you know

**minipa**:  Hey gem, can you possibly close yesterday's meeting so it gets updated on GitHub? I couldn't do it yesterday cos I'm not a chair.

**minipa**:  Thanks :)

**gem**:  minipa, oops!

**gem**:  .stopmeeting

**gem**:  .stop

**gem**:  dng it

**minipa**:  :D

**minipa**:  I think it's .endmeeting

#### Meeting ended by gem, total meeting length 56560 seconds



