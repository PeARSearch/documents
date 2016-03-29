# Untitled meeting at #pears, 2016-03-29 19:19

#### Meeting started by gem

*   <span style="font-weight: bold">Action:</span> start implementation of chord DHT in Python.


**minipa1** : and also the semantic space itself... that's what stultus was
saying: if a new word appears, we can gossip it.

**stultus** : minipa1, yeah, I was thinking about this new word case

**minipa1** : not mentioning the fact that some words change their meaning
over time

**minipa1** : one famous example is 'bush', which completely took over the
hated us president sense

**gem** : stultus, minipa1 so in this new words appearing case, how exactly
will it be stored? A db?

**minipa1** : it's as if the current wikiwoods.db was expanding, so yeah, I
guess

**gem** : ah cool. so the torrent protocol way itself

**stultus** : gem, yeah, we were talking about a hypothetical(for now)  case
where the wikiwoods entry is populated by the peers

**gem** : stultus, isn't that different from the new words scenario?

**stultus** : gem, (or by special peers whenever a new word is found)

**minipa1** : the thing is...

**minipa1** : whenever someone (either any peer or a special peer) finds a
new word, it will only find it in a small context (just one webpage)

**minipa1** : and if this word becomes popular for some reason, it will be
seen more and more and its vector should be adapted to reflect all the
usages it's been seen in

**minipa1** : so the gossip thing would be really cool to update the meaning
of the word

**gem** : ah now it's getting clearer

**gem** : rookie question:

**gem** : what is a special peer?

**minipa1** : :D

**minipa1** : I don't actually think there should be special peers...
* gem feel stupid

**stultus** : gem, hypothetically, if calculating the vector space is a
process which needs certain computing powers, all peers cannot calculate
this, we can have special peers which will be able to calculate the
data.

**stultus** : and other peer can find this special peers using gossip

**minipa1** : yeah, stultus is right...

**minipa1** : I'm just playing with the idea we were talking about
yesterday...

**stultus** : minipa1, hence I added the hypothetical case :P

Meeting started by gem

**gem** : stultus, should there be  dedicated nodes that does the
computing stuff?

**gem** : stultus, because the nodes we are talking about are
client installations right?

**gem** : stultus, we can have dedicated compute servers that
does this

**stultus** : gem, from yesterdays discussion what I understood
is that, the process creating wikiwoods vectorspace collaborativ
ely is still a research topic

**gem** : stultus, minipa1 will that contradict our completely
decentralized philosophy?

**minipa1** : yes, I don't like the idea of needing special
super-computers...

**stultus** : my idea is this

**minipa1** : that's why I started thinking yesterday, and was
wondering whether we could use the co-occurrence frequencies publ
icly available over the network to compute new vectors

**minipa1** :
**stultus is faster than me** :

**gem** : waits for stultus' idea

**stultus** : currently we have a centralized wikiwoods file.
which is any way calculated in a centralized manner

**stultus** : so if we can have another systems which can
calculate these vectors as part of our network, it will make it more d
ecentralized right?

**gem** : currently it doens't have any personal user data

**gem** : but when we start populating it dynamically it involves
personal data

**stultus** : agree that ideally all peers should be equal

**gem** : okay mangoes and oranges :P

**minipa1** : gem, stultus, I need to think about this... I'm
wondering whether some clever neural net implementation might do i
t...

**stultus** : okey

**minipa1** : the nice thing about the NNs is

**minipa1** : that they don't require the probability
distributions I was talking about yesterday

**minipa1** : We might be able to tweak this, though
[8/1893]

**gem** : since the wikiwoods part is heavily under discussion,
how about writing a simple prototype DHT implementation that wil
l find the best pear and do the querying?

**gem** : we have been a lot of talking but very less coding :)

**stultus** : okey lets do this

**minipa1** : sounds like a good idea. I guess the implementation
can be reused for other types of information anyway

**stultus** : there are two popular dht implementations, chord
and kademlia

**gem** : I read cool things about kademlia

**stultus** : chord is the simple one, and it is more popular
among academics,  whereas implementers are using kademlia more

**stultus** : bittorrent is using kademlia

**minipa1** : (that's because academics can't code...)

**gem** : one another thing

**stultus** : my suggestion is to use chord for now, so that we
can understand things easily, and once we have a working prototy
pe. lets port that to kademlia

**gem** : the other day Behrang was asking if we are planning to
stick on to Python

**gem** : I feel strongly about coding in Python. Mostly because
I am heavily biased. :P

**gem** : what are your thoughts minipa1 stultus ?

**stultus** : gem, I think we don't have to think based on the
language, we can have different components in different languages

**minipa1** : I don't think my thoughts should count for much...
but I only understand Python and C++.......

**gem** : stultus, I am asking for this initial DHT
implementation

**gem** : stultus, in case we plan on using threads and stuff,
GIL is messy

**stultus** : gem, so my suggestion is to stick to python itself
since we have already started. and we can think about another l
anguage if we have any blocking issues that are related to the language

**gem** : cool

**minipa1** : how about efficiency? does anybody know that?

**gem** : minipa1, Python is a bit notorious when it comes to
that

**gem** : performance is not as good as what C would give

**gem** : but implementation in C can be a pain

**minipa1** : right, although for the scientific stuff, there are
good wrappers... I'm just wondering about the DHT

**gem** : if the spacial complexity exceeds, we can port to much
efficient languages like Go

**minipa1** : okay

**gem** : Go is easier to pick up and has all the cool features
of JVM

**stultus** : we can always switch languages and write wrappers
to interconnect

**gem** : start implementation of chord DHT in Python.
ACTION: start implementation of chord DHT in Python.

**stultus** : brb

**gem** : I am done for the day folks

**minipa1** : sure, it's late there :)

**gem** : minipa1, yeah :)
Meeting ended by gem, total meeting length 1320 seconds



#### Meeting ended at 19:41:55 UTC
