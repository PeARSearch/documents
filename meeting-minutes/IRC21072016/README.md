## Casual IRC discussion on our design doc

**gem** : Hey minipa !

**minipa** : hey gem :)

**gem** : minipa, How are you?

**minipa** : U on top of a mountain?

**minipa** : Fine. Next week, I have holiday :) :)

**gem** : minipa, Oh yes! From the foothills of Himalayas! :-)

**gem** : minipa, That's good news :)

**minipa** : Seen snow yet? (Falling, I mean.)

**gem** : Not falling :/ Just saw some glacier here and there though. Have to be satisfied by this I guess

**minipa** : :D It could come, still, I'm sure...

**gem** : Did you get time to have a look at the doc minipa ?

**gem** : It is extremely clumsy I am afraid :/

**minipa** : Yes, sorry I didn't get time to write back -- the last two weeks were mad.

**minipa** : The doc is not clumsy, but *I* am. I'm afraid I didn't get everything...

**minipa** : Let me open it, then I can ask questions.

**gem** : I was just trying to summarise the entire thing to one paragraph and paste it on top, so people would just run away or get me arrested :P

**minipa** : :D

**minipa** : ok, stop here (where you're writing now...) :)

**minipa** : what do you mean by 'distribute our vector values across the network'?

**minipa** : the vectors have a fixed location, right? Cos they 'belong' to a specific user.

**minipa** : gem, also, does your terminology of pear vs node correspond to 'indexer' vs 'queryier'?

**gem** : minipa, ah! I guess I didn't explain it well enough

**gem** : minipa, when I said distribute the vector values, what is means is:

**gem** : we have one numpy array corresponding to each one of our pears client, right?

**minipa** : yup

**minipa** : aah... you mean those vectors, not the doc vectors...

**gem** : yep, these vectors

**minipa** : ok, clear now :)

**gem** : can you suggest a better term that I should use?

**gem** : I don't want that confusion to happen again :)

**minipa** : should we define the concept of 'pear profile' somewhere and reuse that?

**gem** : and pear vs node is completely different from indexer vs queryier

**minipa** : :( **feeling stupid** :

**gem** : 'peer profile' sound good

**gem** : actually, the pear vs node thing is not entirely necessary. I added it the first thing in the doc, just because I read in somewhere :P

**minipa** : :)

**gem** : but it is probably important to know the difference since we should keep the DHT and the client part apart

**minipa** : It sounded like this: the peers are the things that get hit through TCP to retrieve docs -- so they are in the role of indexer there.

**minipa** : Ok. When you mean client, you mean the client at search time.

**gem** : that's true. But nodes come into picture both in the indexing and querying process

**minipa** : Ah, ok, I see.

**gem** : more or less. I tend to think of our pears installation itself as the client.

**minipa** : Because the DHT gets filled at indexing time, right?

**gem** : clint - the user facing side of it. the part excluding the DHT and the fancy networks

**gem** : yes that's correct

**minipa** : ok, makes sense. So let me re-read :)

**gem** : and we look up the DHT at querying time, so

**minipa** : gem, next question: shouldn't the ring be organised so that more similar pear profile are also closer on the ring?

**gem** : minipa, In conventional DHT yes. But when we are considering LSH it changes a bit.

**minipa** : Ah!

**gem** : minipa, What happens is, we create hashes of our data point, to get values, that would come closer to the node IDs

**gem** : Hence we map the hashes to identical node IDs

**gem** : (again, this is one way of doing it)

**minipa** : what are data points here? pear profiles?

**gem** : Oh yes! (I am so inconsistent )

**minipa** : :) gem, could you make the doc writeable? Then I can put comments/questions directly in the text.

**gem** : In real time, it is quite tough to compare multi-dimensional values. So if we start arranging the nodes based on these values the comparison becomes tough

**gem** : sure

**gem** : minipa, Now I think you would be able to comment

**minipa** : why is it so hard? it's just doing cosine over a matrix, right?  With the right factorisation, it should be fast enough...

**gem** : not just that. We are talking about n multi-dimensional values spread across the network.

**gem** : Hitting one at a time would we extremely inefficient.

**gem** : so in our present infrastructure,

**minipa** : Ah, so the pear profiles are not cached locally..

**gem** : to an extend, yes. But more than that, will make the local machine go slow

**gem** : so coming back,

**gem** : in our present infrastructure, we hash our pear profile twice

**gem** : hash 1, H - It will hash the peer profile p to get a value H(p) which will correspond to a hash bucket in our hash table.

**minipa** : ok

**gem** : hash 2, G - It will hash the above value H(p) to the ID corresponding to a node G(H(p))

**minipa** : Aah, right! Understood!

**minipa** : And so, how does the similarity calculation take place?

**gem** : So assume that the user has a query. As per our current infrastructure, we create a multi-dimensional vector for this query as well right?

**minipa** : yes

**gem** : let us call that array 'q'

**minipa** : ok

**gem** : We are trying to get all the peers with profile closer to q

**minipa** : yup

**gem** : according to LSH, the data points closer are highly likely to hash to the same value or a value very close to that

**minipa** : ok -- this is what you call hash buckets?

**gem** : that's correct

**gem** : so we are trying to find the proper hash bucket and before that the exact hash table(which is basically the node which has the table)

**gem** : here, we consider an offset to our query vector(this is suggested as per LSH and is open to modifications) **gem** : We have our hash functions H and G

**gem** : ideally, we can do H(q) and G(H(q)) getting the bucket and the node respectively

**minipa** : Ok, so let me summarise to make sure I get it:

**gem** : but according to entropy LSH, we consider as candidates the points mapping to close hash values.

**minipa** : q gets hashed and ends up in a hash bucket B. B correspond to a value H(p) which is the hash of a profile. We retrieve the actual node by doing G(H(p)).

**gem** : not exactly

**minipa** : =(

**gem** : we are not directly hitting a profile. instead we are hitting machines that are most likely to store tables with closer profiles

**gem** : let me try to explain it a bit more clearly:

**minipa** : Right, that's what I meant.

**gem** : okay :)

**minipa** : Which bit was wrong in what I said? (Just so that I repair misunderstandings...)

**gem** : B does not directly correspond to the hash of a profile

**gem** : B is basically the ID of the hash bucket. It is just going to be similar to the hash of the profile(s)

**gem** : or closer

**minipa** : Urgh. Ok, then I didn't get it. I thought G(H(p)) was the node.

**minipa** : Ah, stop, delete what I said...

**gem** : Okay, let me start over the querying part

**minipa** : ok, right. got it :)

**gem** : are you sure? :)

**minipa** : :D No.........

**gem** : He he :D

**gem** : starting over:

**minipa** : Please don't get crossed with me ;)

**gem** : Of course not :D

**gem** : We have a query coming up and the corresponding vector point is q

**minipa** : ok

**gem** : we are trying to get all the nodes with pear profile closer to q

**minipa** : yes

**gem** : the following is a suggestion as per entropy LSH

**gem** : we consider several offset values along with q

**minipa** : ok, stop

**gem** : yes

**minipa** : you mean we are generating offsets from q? how?

**gem** : no no. We consider significantly small vector values and add it to q to get a set of vector that lie closer

**gem** : Why I propose this is, this will reduce the number of hash tables necessary to implement the schema

**minipa** : ok, so we're generating n random vectors which lie very close to q...?

**gem** : yes.

**minipa** : ok

**gem** : we then hash all these values, to get a set {GH(q + δi ) | 1 ≤ i ≤ L}

**gem** : where  δi are our offsets

**minipa** : and L the number of generated vectors...

**gem** : correct

**minipa** : ok

**gem** : So the thing is, since our  δi value is so small, the GH(q + δi ) for all values ranging 1 **= i **=L, is going to be same

**minipa** : ok

**gem** : but the hash bucket to which all these values map to are going to be different

**minipa** : ok, define hash bucket again...

**gem** : i.e. H(q + δi ) will yield a number of hash buckets

**gem** : okay, so let us say we have a hash table (in our case it is a node itself)

**minipa** : each bucket only has one value in it??

**minipa** : ok

**gem** : each hash table will be divided into n buckets

**minipa** : ok

**minipa** : hang on, are we now talking of hash tables for documents?

**gem** : we can use a hash function to put values inside each of these hash bucket. in our implementation there will be collision. that is more that one value can go into same bucket

**gem** : this is considered the best thing about LSH. close values under same hash bucket

**gem** : no no. we are not talking about documents at all

**gem** : did I confuse you even more? :(

**minipa** : Sorry, it's my fault... bear with me...

**minipa** : you said a hash table is a node, but then

**minipa** : a node is an actual PeARS install, right?

**minipa** : I don't understand what is stored in that hash table that is the node.

**gem** : yes. and we have a hash table(a linked list preferably) implemented in each of these nodes

**gem** : ah I get your doubt now

**minipa** : :)

**gem** : the vital information now for us, are: The pear profile and the IP address of the node that has that pear profile for proper routing

**minipa** : ok

**gem** : so these pear profile value and node ID mapping will be populated in the buckets inside our hash table

**minipa** : i.e. each node contains a subset of the IP-profile pairs on the entire network?

**gem** : exactly

**minipa** : :)

**minipa** : and what are the buckets on a single node?

**minipa** : IP-profile pairs for nodes that are similar?

**gem** : this is again a mechanism to reduce the number of hash tables necessary

**gem** : and to reduce look up overload

**minipa** : ok, I think I start getting the gist...

**gem** : what we does is again divide the hash table to buckets, each bucket storing a range of values

**gem** : so when we hashed our query offset, q+x, to get hash H(q+x), we take only the hash bucket with ID H(q+x) in the machine GH(q+x)

**minipa** : ok, and you said earlier that H(q + δi ) yields different hash buckets. Why is that, if δi is so small...?

**gem** : That is the significance of the Hash function again

**minipa** : Ah, so the hash could result in values that are further apart than the offset vectors.

**gem** : The δi is small enough that the value G(H(q + δi )) is same for all values of i

**gem** : But it is large enough that H(q + δi ) can yield different bucket ID in that machine for each value of i

**minipa** : ok, nice.

**gem** : so let us say we got 5 buckets matching the  H(q + δi )  values

**gem** : we retrieve the pear profile-node ID mappings from all these machines

**gem** : now we can do our cosine similarity on all these pear profiles

**gem** : and we will get the list of the best pears say 10 of them

**minipa** : And the profile-node mappings on a particular machine will correspond to nodes that are anyway similar to this machine, right?

**gem** : that's correct

**minipa** : I think I'm nearly there :)

**minipa** : So if you didn't do the offset thing...

**minipa** : you wouldn't select enough buckets and would risk missing some good nodes?

**gem** : that's correct. To work around that, we will have to make more hashtables so the query would hit the most closest one

**gem** : which is really inefficient - space issues and network load

**minipa** : ok, clever.

**gem** : now,

**gem** : we have a list of pears

**minipa** : yes

**gem** : the querying machine will have to hit these machines directly to get all the documents

**minipa** : yup

**gem** : We extend the pear client to have an API that will open up these files to the network

**minipa** : what does this mean?

**gem** : just that we haven't yet implemented a way to index and make these files available on an HTTP request. we will have to right that part.  Just calling it API to make it sound fancy :P

**minipa** : :D

**gem** : the rest happens the same way as it does now.

**minipa** : Cool, sounds great :)

**gem** : Now a couple of corner cases,

**minipa** : ok

**gem** : 1. IP address of the machine changes:

**minipa** : urgh

**gem** : In this scenario it is the duty of the machine itself to update its presence in the network

**minipa** : yes, makes sense.

**gem** : Fortunately all the present DHTs have taken care of this issue and is going to be a re-implementation of that :)

**minipa** : :)

**minipa** : Stupid question: what happens with a machine that is e.g.  behind Tor?

**gem** : a packet with old value and new ID is circulated and the corresponding tables are updated - is a gist of it

**gem** : This is one issue I wanted to mention :/

**minipa** : ok

**gem** : Everywhere it says, DHT over tor is a bad idea

**minipa** : hm, okay. Because the IP changes too often?

**gem** : yes

**gem** : the thing is,

**gem** : tor only supports TCP protocol

**gem** : the developer can decide to use the UDP protocol to communicate

**gem** : so we can make it work even when the user sets a proxy that can't be used

**minipa** : Ok. But then I guess there is no easy alternative for distributed systems over Tor, or is there?

**gem** : according to this blog post: https://blog.torproject.org/blog/bittorrent-over-tor-isnt-good-idea, there isn't much we can do

**gem** : let me do some more research on this, though

**minipa** : Ok, well, we have to start somewhere so let's not worry about it straightaway...

**minipa** : What is corner case 2? The profile changes? :)

**gem** : yes :)

**minipa** : urgh again

**minipa** : My feeling about this is...

**gem** : so in conventional DHT, there is this process of checking if a node has gone bad or not. Every 20 minutes or so it pings a machine and sees if it is alive

**minipa** : for the minute, let's stick to a dirty solution where we recreate the node entirely now and then, and update the network.

**minipa** : ok

**gem** : what we can do is, along with the alive check we can check if the profile has changed. If yes, we don't do anything immediately, we just flag the value

**minipa** : ok, sounds sensible

**gem** : We can run a periodic updation job once or twice a week that corrects these flagged values

**gem** : It is going to be heavy on the entire load if we do it more often

**minipa** : That would be the responsibility of each node, right?

**minipa** : Why don't we run a local check: if the profile has changed a lot, it should be updated.

**gem** : each node can check it locally, yes. But updating the wrong values across the huge network can take a toll on efficiency

**minipa** : Hm, yes.

**gem** : again, I am not completely sure what the time complexity of such a process would be. I am just assuming for the time being.

**minipa** : I wouldn't expect those values to change very often, though. At least not dramatically.

**minipa** : We should probably cross the bridge when we get there, once we have 'real' data. What do you think?

**gem** : I think this issue is to be tackled once we have the real network up and running

**minipa** : :)

**gem** : can't agree more :)

**gem** : I think this is a good point to start the development.

**gem** : of the DHT

**minipa** : Yup, that all sounds super great.

**minipa** : Are you happy to start coding?

**gem** : Very much! I have found a proper base for myself. I will be staying here for a while.

**minipa** : Nice :) I'm imagining you in a little house under the snow, at the foot of a glacier...

**minipa** : In the meantime,

**gem** : well, it is a bit more green than that :P

**minipa** : :D

**minipa** : I want to concentrate on doing some indexing work.

**minipa** : There are some bits of code lying around that need to be combined into something proper.

**gem** : That sounds great. Have you recovered completely now? Don't put too much pressure otherwise

**minipa** : Actually, hands are starting hurting... irc a bit tough on them ;)

**minipa** : I'll use my week holiday to do some PeARS thinking :)

**gem** : Okay :)

**minipa** : Thanks for all the explanations today :)

**gem** : I would like to do some more cleaning up on the doc. Talking with you made it clear, where all I should make changes :)

**minipa** : Cool, I'll take a look once you've revised it (and probably ask more stupid questions) :)

**gem** : I will hit everyone's inbox once that is done

**gem** : Please do :)

**minipa** : Brilliant!

**minipa** : Then, I'll go and have dinner ;)

**gem** : Talk to you soon. :-)

**minipa** : Sure. Enjoy the mountains!!

**minipa** : CU

**gem** : Bon appétit! See you :)

**minipa** : :)**gem** : Hey minipa !

**minipa** : hey gem :)

**gem** : minipa, How are you?

**minipa** : U on top of a mountain?

**minipa** : Fine. Next week, I have holiday :) :)

**gem** : minipa, Oh yes! From the foothills of Himalayas! :-)

**gem** : minipa, That's good news :)

**minipa** : Seen snow yet? (Falling, I mean.)

**gem** : Not falling :/ Just saw some glacier here and there though. Have to be satisfied by this I guess

**minipa** : :D It could come, still, I'm sure...

**gem** : Did you get time to have a look at the doc minipa ?

**gem** : It is extremely clumsy I am afraid :/

**minipa** : Yes, sorry I didn't get time to write back -- the last two weeks were mad.

**minipa** : The doc is not clumsy, but *I* am. I'm afraid I didn't get everything...

**minipa** : Let me open it, then I can ask questions.

**gem** : I was just trying to summarise the entire thing to one paragraph and paste it on top, so people would just run away or get me arrested :P

**minipa** : :D

**minipa** : ok, stop here (where you're writing now...) :)

**minipa** : what do you mean by 'distribute our vector values across the network'?

**minipa** : the vectors have a fixed location, right? Cos they 'belong' to a specific user.

**minipa** : gem, also, does your terminology of pear vs node correspond to 'indexer' vs 'queryier'?

**gem** : minipa, ah! I guess I didn't explain it well enough

**gem** : minipa, when I said distribute the vector values, what is means is:

**gem** : we have one numpy array corresponding to each one of our pears client, right?

**minipa** : yup

**minipa** : aah... you mean those vectors, not the doc vectors...

**gem** : yep, these vectors

**minipa** : ok, clear now :)

**gem** : can you suggest a better term that I should use?

**gem** : I don't want that confusion to happen again :)

**minipa** : should we define the concept of 'pear profile' somewhere and reuse that?

**gem** : and pear vs node is completely different from indexer vs queryier

**minipa** : :( **feeling stupid** :

**gem** : 'peer profile' sound good

**gem** : actually, the pear vs node thing is not entirely necessary. I added it the first thing in the doc, just because I read in somewhere :P

**minipa** : :)

**gem** : but it is probably important to know the difference since we should keep the DHT and the client part apart

**minipa** : It sounded like this: the peers are the things that get hit through TCP to retrieve docs -- so they are in the role of indexer there.

**minipa** : Ok. When you mean client, you mean the client at search time.

**gem** : that's true. But nodes come into picture both in the indexing and querying process

**minipa** : Ah, ok, I see.

**gem** : more or less. I tend to think of our pears installation itself as the client.

**minipa** : Because the DHT gets filled at indexing time, right?

**gem** : clint - the user facing side of it. the part excluding the DHT and the fancy networks

**gem** : yes that's correct

**minipa** : ok, makes sense. So let me re-read :)

**gem** : and we look up the DHT at querying time, so

**minipa** : gem, next question: shouldn't the ring be organised so that more similar pear profile are also closer on the ring?

**gem** : minipa, In conventional DHT yes. But when we are considering LSH it changes a bit.

**minipa** : Ah!

**gem** : minipa, What happens is, we create hashes of our data point, to get values, that would come closer to the node IDs

**gem** : Hence we map the hashes to identical node IDs

**gem** : (again, this is one way of doing it)

**minipa** : what are data points here? pear profiles?

**gem** : Oh yes! (I am so inconsistent )

**minipa** : :) gem, could you make the doc writeable? Then I can put comments/questions directly in the text.

**gem** : In real time, it is quite tough to compare multi-dimensional values. So if we start arranging the nodes based on these values the comparison becomes tough

**gem** : sure

**gem** : minipa, Now I think you would be able to comment

**minipa** : why is it so hard? it's just doing cosine over a matrix, right?  With the right factorisation, it should be fast enough...

**gem** : not just that. We are talking about n multi-dimensional values spread across the network.

**gem** : Hitting one at a time would we extremely inefficient.

**gem** : so in our present infrastructure,

**minipa** : Ah, so the pear profiles are not cached locally..

**gem** : to an extend, yes. But more than that, will make the local machine go slow

**gem** : so coming back,

**gem** : in our present infrastructure, we hash our pear profile twice

**gem** : hash 1, H - It will hash the peer profile p to get a value H(p) which will correspond to a hash bucket in our hash table.

**minipa** : ok

**gem** : hash 2, G - It will hash the above value H(p) to the ID corresponding to a node G(H(p))

**minipa** : Aah, right! Understood!

**minipa** : And so, how does the similarity calculation take place?

**gem** : So assume that the user has a query. As per our current infrastructure, we create a multi-dimensional vector for this query as well right?

**minipa** : yes

**gem** : let us call that array 'q'

**minipa** : ok

**gem** : We are trying to get all the peers with profile closer to q

**minipa** : yup

**gem** : according to LSH, the data points closer are highly likely to hash to the same value or a value very close to that

**minipa** : ok -- this is what you call hash buckets?

**gem** : that's correct

**gem** : so we are trying to find the proper hash bucket and before that the exact hash table(which is basically the node which has the table)

**gem** : here, we consider an offset to our query vector(this is suggested as per LSH and is open to modifications)

**gem** : We have our hash functions H and G

**gem** : ideally, we can do H(q) and G(H(q)) getting the bucket and the node respectively

**minipa** : Ok, so let me summarise to make sure I get it:

**gem** : but according to entropy LSH, we consider as candidates the points mapping to close hash values.

**minipa** : q gets hashed and ends up in a hash bucket B. B correspond to a value H(p) which is the hash of a profile. We retrieve the actual node by doing G(H(p)).

**gem** : not exactly

**minipa** : =(

**gem** : we are not directly hitting a profile. instead we are hitting machines that are most likely to store tables with closer profiles

**gem** : let me try to explain it a bit more clearly:

**minipa** : Right, that's what I meant.

**gem** : okay :)

**minipa** : Which bit was wrong in what I said? (Just so that I repair misunderstandings...)

**gem** : B does not directly correspond to the hash of a profile

**gem** : B is basically the ID of the hash bucket. It is just going to be similar to the hash of the profile(s)

**gem** : or closer

**minipa** : Urgh. Ok, then I didn't get it. I thought G(H(p)) was the node.

**minipa** : Ah, stop, delete what I said...

**gem** : Okay, let me start over the querying part

**minipa** : ok, right. got it :)

**gem** : are you sure? :)

**minipa** : :D No.........

**gem** : He he :D

**gem** : starting over:

**minipa** : Please don't get crossed with me ;)

**gem** : Of course not :D

**gem** : We have a query coming up and the corresponding vector point is q

**minipa** : ok

**gem** : we are trying to get all the nodes with pear profile closer to q

**minipa** : yes

**gem** : the following is a suggestion as per entropy LSH

**gem** : we consider several offset values along with q

**minipa** : ok, stop

**gem** : yes

**minipa** : you mean we are generating offsets from q? how?

**gem** : no no. We consider significantly small vector values and add it to q to get a set of vector that lie closer

**gem** : Why I propose this is, this will reduce the number of hash tables necessary to implement the schema

**minipa** : ok, so we're generating n random vectors which lie very close to q...?

**gem** : yes.

**minipa** : ok

**gem** : we then hash all these values, to get a set {GH(q + δi ) | 1 ≤ i ≤ L}

**gem** : where  δi are our offsets

**minipa** : and L the number of generated vectors...

**gem** : correct

**minipa** : ok

**gem** : So the thing is, since our  δi value is so small, the GH(q + δi ) for all values ranging 1 **= i **=L, is going to be same

**minipa** : ok

**gem** : but the hash bucket to which all these values map to are going to be different

**minipa** : ok, define hash bucket again...

**gem** : i.e. H(q + δi ) will yield a number of hash buckets

**gem** : okay, so let us say we have a hash table (in our case it is a node itself)

**minipa** : each bucket only has one value in it??

**minipa** : ok

**gem** : each hash table will be divided into n buckets

**minipa** : ok

**minipa** : hang on, are we now talking of hash tables for documents?

**gem** : we can use a hash function to put values inside each of these hash bucket. in our implementation there will be collision. that is more that one value can go into same bucket

**gem** : this is considered the best thing about LSH. close values under same hash bucket

**gem** : no no. we are not talking about documents at all

**gem** : did I confuse you even more? :(

**minipa** : Sorry, it's my fault... bear with me...

**minipa** : you said a hash table is a node, but then

**minipa** : a node is an actual PeARS install, right?

**minipa** : I don't understand what is stored in that hash table that is the node.

**gem** : yes. and we have a hash table(a linked list preferably) implemented in each of these nodes

**gem** : ah I get your doubt now

**minipa** : :)

**gem** : the vital information now for us, are: The pear profile and the IP address of the node that has that pear profile for proper routing

**minipa** : ok

**gem** : so these pear profile value and node ID mapping will be populated in the buckets inside our hash table

**minipa** : i.e. each node contains a subset of the IP-profile pairs on the entire network?

**gem** : exactly

**minipa** : :)

**minipa** : and what are the buckets on a single node?

**minipa** : IP-profile pairs for nodes that are similar?

**gem** : this is again a mechanism to reduce the number of hash tables necessary

**gem** : and to reduce look up overload

**minipa** : ok, I think I start getting the gist...

**gem** : what we does is again divide the hash table to buckets, each bucket storing a range of values

**gem** : so when we hashed our query offset, q+x, to get hash H(q+x), we take only the hash bucket with ID H(q+x) in the machine GH(q+x)

**minipa** : ok, and you said earlier that H(q + δi ) yields different hash buckets. Why is that, if δi is so small...?

**gem** : That is the significance of the Hash function again

**minipa** : Ah, so the hash could result in values that are further apart than the offset vectors.

**gem** : The δi is small enough that the value G(H(q + δi )) is same for all values of i

**gem** : But it is large enough that H(q + δi ) can yield different bucket ID in that machine for each value of i

**minipa** : ok, nice.

**gem** : so let us say we got 5 buckets matching the  H(q + δi )  values

**gem** : we retrieve the pear profile-node ID mappings from all these machines

**gem** : now we can do our cosine similarity on all these pear profiles

**gem** : and we will get the list of the best pears say 10 of them

**minipa** : And the profile-node mappings on a particular machine will correspond to nodes that are anyway similar to this machine, right?

**gem** : that's correct

**minipa** : I think I'm nearly there :)

**minipa** : So if you didn't do the offset thing...

**minipa** : you wouldn't select enough buckets and would risk missing some good nodes?

**gem** : that's correct. To work around that, we will have to make more hashtables so the query would hit the most closest one

**gem** : which is really inefficient - space issues and network load

**minipa** : ok, clever.

**gem** : now,

**gem** : we have a list of pears

**minipa** : yes

**gem** : the querying machine will have to hit these machines directly to get all the documents

**minipa** : yup

**gem** : We extend the pear client to have an API that will open up these files to the network

**minipa** : what does this mean?

**gem** : just that we haven't yet implemented a way to index and make these files available on an HTTP request. we will have to right that part.  Just calling it API to make it sound fancy :P

**minipa** : :D

**gem** : the rest happens the same way as it does now.

**minipa** : Cool, sounds great :)

**gem** : Now a couple of corner cases,

**minipa** : ok

**gem** : 1. IP address of the machine changes:

**minipa** : urgh

**gem** : In this scenario it is the duty of the machine itself to update its presence in the network

**minipa** : yes, makes sense.

**gem** : Fortunately all the present DHTs have taken care of this issue and is going to be a re-implementation of that :)

**minipa** : :)

**minipa** : Stupid question: what happens with a machine that is e.g.  behind Tor?

**gem** : a packet with old value and new ID is circulated and the corresponding tables are updated - is a gist of it

**gem** : This is one issue I wanted to mention :/

**minipa** : ok

**gem** : Everywhere it says, DHT over tor is a bad idea

**minipa** : hm, okay. Because the IP changes too often?

**gem** : yes

**gem** : the thing is,

**gem** : tor only supports TCP protocol

**gem** : the developer can decide to use the UDP protocol to communicate

**gem** : so we can make it work even when the user sets a proxy that can't be used

**minipa** : Ok. But then I guess there is no easy alternative for distributed systems over Tor, or is there?

**gem** : according to this blog post: https://blog.torproject.org/blog/bittorrent-over-tor-isnt-good-idea, there isn't much we can do

**gem** : let me do some more research on this, though

**minipa** : Ok, well, we have to start somewhere so let's not worry about it straightaway...

**minipa** : What is corner case 2? The profile changes? :)

**gem** : yes :)

**minipa** : urgh again

**minipa** : My feeling about this is...

**gem** : so in conventional DHT, there is this process of checking if a node has gone bad or not. Every 20 minutes or so it pings a machine and sees if it is alive

**minipa** : for the minute, let's stick to a dirty solution where we recreate the node entirely now and then, and update the network.

**minipa** : ok

**gem** : what we can do is, along with the alive check we can check if the profile has changed. If yes, we don't do anything immediately, we just flag the value

**minipa** : ok, sounds sensible

**gem** : We can run a periodic updation job once or twice a week that corrects these flagged values

**gem** : It is going to be heavy on the entire load if we do it more often

**minipa** : That would be the responsibility of each node, right?

**minipa** : Why don't we run a local check: if the profile has changed a lot, it should be updated.

**gem** : each node can check it locally, yes. But updating the wrong values across the huge network can take a toll on efficiency

**minipa** : Hm, yes.

**gem** : again, I am not completely sure what the time complexity of such a process would be. I am just assuming for the time being.

**minipa** : I wouldn't expect those values to change very often, though. At least not dramatically.

**minipa** : We should probably cross the bridge when we get there, once we have 'real' data. What do you think?

**gem** : I think this issue is to be tackled once we have the real network up and running

**minipa** : :)

**gem** : can't agree more :)

**gem** : I think this is a good point to start the development.

**gem** : of the DHT

**minipa** : Yup, that all sounds super great.

**minipa** : Are you happy to start coding?

**gem** : Very much! I have found a proper base for myself. I will be staying here for a while.

**minipa** : Nice :) I'm imagining you in a little house under the snow, at the foot of a glacier...

**minipa** : In the meantime,

**gem** : well, it is a bit more green than that :P

**minipa** : :D

**minipa** : I want to concentrate on doing some indexing work.

**minipa** : There are some bits of code lying around that need to be combined into something proper.

**gem** : That sounds great. Have you recovered completely now? Don't put too much pressure otherwise

**minipa** : Actually, hands are starting hurting... irc a bit tough on them ;)

**minipa** : I'll use my week holiday to do some PeARS thinking :)

**gem** : Okay :)

**minipa** : Thanks for all the explanations today :)

**gem** : I would like to do some more cleaning up on the doc. Talking with you made it clear, where all I should make changes :)

**minipa** : Cool, I'll take a look once you've revised it (and probably ask more stupid questions) :)

**gem** : I will hit everyone's inbox once that is done

**gem** : Please do :)

**minipa** : Brilliant!

**minipa** : Then, I'll go and have dinner ;)

**gem** : Talk to you soon. :-)

**minipa** : Sure. Enjoy the mountains!!

**minipa** : CU

**gem** : Bon appétit! See you :)

**minipa** : :)

>>>>>>> adding the log from 21/07/2016
