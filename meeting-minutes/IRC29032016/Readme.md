## Casual IRC Logs from 29-03-2012
* Now talking on #pears
* Topic for #pears is: Channel to discuss PeARS development, usage and everything else. https://pearsearch.org
* Topic for #pears set by gem!~gem@111.92.125.46 at Mon Mar 28 22:27:23 2016
-ChanServ- [#pears] "Welcome to official IRC channel of PeARS! Keep it friendly, folks! :-)"

**stultus** : hey gem minipa1 :) 

**gem** : stultus, hey :)

**minipa1** : stultus, hello!

**stultus** : minipa1, one quick question.  how difficult is it to create  vectors from a single webpage? (vectors as in the vectors of wikiwoods.db) 

**minipa1** : stultus, what do you mean by 'creating from'? If you try to create a word vector from a tiny amount of data, your vector won't be very good...

**minipa1** : Give me some context :)

**stultus** : minipa1, I was thinking about the possibility of creating the contents of wikiwoods.db locally. as the users visits a website or something (I was simply thinking about the possibility). 

**minipa1** : stultus, I see... you want the database itself to emerge from browsing. So at the beginning, there would only be a few words in it, and as more people browse more pages, it would grow. Correct?

**minipa1** : If so, you've just hit on a hard research question ;)

**stultus** : minipa1, yeah, that was what I was thinking :) 

**minipa1** : So... there are several problems with this...

**minipa1** : first, a word vector is defined in terms of other words, which are the dimensions of the vector space. So if you want your vocabulary to grow from nothing, your space is gonna have to be able to grow to.

**minipa1** : second, the weights of the vectors along each axis of the space are usually a function of 1) the probability of co-occurrence of two words; 2) the probability of occurrence of those words taken separately. This means  that probabilistically, you need a closed world assumption .

**minipa1** : This said, there might be ways around this. @languagerecipes is a good person to talk to, as he works on random indexing models which give you a bit more freedom with setting the weights of the vectors.

**minipa1** : Similarly, neural network models can help with the weighting.

**minipa1** : But it's just an unsolved problem, so perhaps not for pears yet, I'm afraid :-S

**minipa1** : Now you got me thinking... ;)

**minipa1** : There's of course the problem of the search query, which might use words that are not included in the pages.

**minipa1** : But one thing that could be done is recording simple co-occurrence frequencies from people's browsing histories, and share that.

* **stultus** is taking notes

* **stultus** has quit (Ping timeout: 248 seconds)

**minipa1** : If we let the space emerge from nothing, we would have a situation at the beginning where no one can understand each other, because they might have browsed fairly different things types of pages

**stultus_** : did I miss anything after the taking notes message?
* You are now known as stultus

**minipa1** : I was just thinking aloud :)

**minipa1** : Repeat: we have to think of the shared semantic space as people's shared understanding of a particular vocab (in our case, so far, English)

**minipa1** : Repeat:  If we let the space emerge from nothing, we would have a situation at the beginning where no one can understand each other, because they might have browsed fairly different things types of pages

**stultus** : minipa1, I see 

**minipa1** : but there is something attractive about the idea of developing a personalised vocabulary for each user.

**minipa1** : Were you thinking about this in terms of updating the vector database?

**minipa1** : As in, what do we do when we want to change it?

**stultus** : minipa1, I was thinking about creating the vector database itself collaboratively 

**stultus** : minipa1, which includes the updating part also

**minipa1** : yes, that's very nice, and as I said before, I think we could collaboratively record the co-occurrence frequencies. That would be a big start.

**stultus** : okey

**stultus** : minipa1, so ideally there will be a vector in the db corresponding to each word in a dictionary right?

**minipa1** : yes, that's the ideal case

**stultus** : minipa1, okey. 

**stultus** : minipa1, what I'm thinking is this 

**minipa1** : and we have the problem I mentioned a while ago, that we need to cater for new words

**stultus** : minipa1, okey. 

**stultus** : minipa1, so this is the idea 

**stultus** : minipa1, in a torrent network, there is a DHT which contains the information about the peers 

**minipa1** : okay...

**stultus** : minipa1, the network is using the DHT for routing purpose, and the data is exchanged using the torrent protocol 

**minipa1** : okay

**stultus** : minipa1, each node will contain information about nearby nodes, and some little less information about far away nodes. 

**minipa1** : yup

**stultus** : minipa1, the dht also somehow stores which node has a particular chunk of data. 

**minipa1** : ok... just a quick question, when you said 'nearby' node, what is the distance criterion?

**stultus** : minipa1, that I'm not sure, I'll have to read. 

**minipa1** : ok

**stultus** : minipa1, I'm trying to have a top level understanding now.. 

**minipa1** : sure, and I'm getting my understanding from you ;)

**stultus** : minipa1,and I was thinking about a similar implementation. instead of the chunk of data, we'll be storing the word - vector data and routing information 

**minipa1** : yes, understood. That's very nice :)

**stultus** : minipa1, so if we don't have a vector corresponding to a word, we will be downloading it from the network 

**minipa1** : is there a way to know which words have been observed over the network?

**stultus** : minipa1, observed as in 

**stultus** : ?

**stultus** : minipa1, are you referring to the privacy aspect?

**minipa1** : Sorry, I'm a bit slow... let's say the people on the network have browsed several billions of pages, but they've never seen the name of that new game console called JFADF8... Now, someone browses a page where the word JFADF8 occurs. Could we build a vocab somewhere that records everything that everybody, collectively, has seen?

**stultus** : minipa1, oh okey. I'm yet to think about this scenario 

**minipa1** : You know, this is a very cool idea. And say we stored the co-occurrence frequencies,

**minipa1** : we could have a system where everybody can build their own vectors on the fly from that info.

**minipa1** : So the DHT would have info about where to find occurrences of the word.

**minipa1** : This might get big, though :-S

**stultus** : :) 

**stultus** : so again to torrent system 

**stultus** : there is this thing called a tracker based system and a tracker-less system 

**minipa1** : ok...

**stultus** : a tracker is a computer holding routing information about a swarm 

**minipa1** : what's a swarm?

**stultus** : * routing information of all the nodes in a swarm 

**stultus** : a group of peers connected to each other 

**minipa1** : ok

**stultus** : for example, if there is a file that is being shared,  all the computers sending and receiving forms a network 

**stultus** : it is called a swarm 

**minipa1** : ok!

**stultus** : (these are very loose definitions) 

**minipa1** : :)

**stultus** : so the torrent file will contain the information about the tracker, so that each node will be contacting the tracker and they will be depending on the tracker for the routing info 

**stultus** : now after implementing the dht based system, each node is a tracker.  and this dht based implementation is called trackerless torrents 

**minipa1** : hang on, you're losing me... ;)

**minipa1** : in our case, which info exactly would be in the tracker?

**stultus** : minipa1, I'll try to explain again 

**minipa1** : sorry... :-S

**stultus** : it is fine, I

**stultus** : I am also having a clear idea, while trying to explain :) 

**minipa1** : :)

**stultus** : so there is a torrent network

**minipa1** : ok

**stultus** : and suppose we are sharing a file using that network, 

**minipa1** : ok

**stultus** : then there will be a subnetwork which will be sharing this particular file among the peers 

**stultus** : this sub network is called a swarm 

**minipa1** : ok

**stultus** : so each nod in this swarm need routing information to other nodes, so that the data can be exchanged. 

**minipa1** : yes

**stultus** : and if there is a central system that co-ordinates the exchange of this routing information, that is called a tracker 

**minipa1** : ok, and the central system has info about the IPs of the peers, and also which bits of data they have??

**stultus** : minipa1, afaik it has the info about the ips only 

**minipa1** : ok...

**stultus** : minipa1, and based on the response from the tracker, the nod will contact other nodes, and start transfering the data. 

**stultus** : this is tracker based implementation. 

**minipa1** : yes, I see.

**stultus** : and in a trackerless implementation, there will be dht holding the routing information. 

**minipa1** : ok

**stultus** : and each peer will have some routing information about the nearby nodes 

**stultus** : this makes each node a tracker 

**minipa1** : aaaah! I get it now :)

**minipa1** : and if I ever need something from a distant node, I have to hop several times?

**stultus** : yeah 

**minipa1** : right, nice

**stultus** : DHT can also work alongside traditional trackers. For example, a torrent can use both DHT and a traditional tracker, which will provide redundancy in case the tracker fails.

**minipa1** : ok

**stultus** : this is how the torrent system works. 

**minipa1** : thanks, much clearer now :) :)

**minipa1** : so we could have a system where distance is semantic distance, right?

**stultus** : hopefully

**minipa1** : i.e. the vectors that are closer in the space are also 'closer' on the network

**stultus** : I'm yet to read the complete dht specification. 

**minipa1** : sure

**minipa1** : i guess there are two types of info to consider...

**stultus** : in our case, I was thinking about having a centralized tracker which distributes the vectors to the swarm

**minipa1** : right

**minipa1** : ... one type of info are the word vectors, the other the page that people have visited

**minipa1** : pages...

**stultus** : yeah 

**minipa1** : it is not completely clear to me who should have which word vectors so that it makes sense

**minipa1** : can we have two DHTs sitting alongside each other?

**stultus** : I was also thinking about having two dhts 

**minipa1** : cool :)

**stultus** : but we should have  a complete idea after reading the full specification. 

**minipa1** : yes, right

**minipa1** : I think this is all very cool.

**minipa1** : We should talk to @languagerecipes about this. He's got that idea about having a standard for 'open vectors',

**stultus** : minipa1, so right now, everything that I said is about sharing the data from the wikwoods.db

**minipa1** : yes, understood

**stultus** : minipa1, I think we can share this conversation with others 

**minipa1** : yes, we should. Where is that bot? ;)

**stultus** : gem, be the bot for the time being :P 

**minipa1** : stultus, but the same principle will apply to the sharing of document vectors, right?

**stultus** : minipa1, yes it should. will share my thoughts on this after reading and understanding our current pear choosing logic

**stultus** : minipa1, also I'll be updating materials that I read(or mark as to-read) in this file - minipa1, also I'll be updating this file with the docs I rea

**stultus** : minipa1, also I'll be updating materials that I read(or mark as to-read) in this file - https://github.com/stultus/2016/blob/master/to-read-articles.md

**minipa1** : Oh, that's great! I should read on this too...

**stultus** : minipa1, in the distributed systems section. 

**minipa1** : Great! Thanks!

**minipa1** : Well, that was productive and got me thinking :) Hopefully, I'll dream about it and understand everything by morning ;)

**stultus** : minipa1, :) 

**minipa1** : oh, just one more thing...

**minipa1** : about the demo, what shall we do?

**minipa1** : should we just have a few smallish demo nodes?

**minipa1** : in which case I would create some...

**stultus** : minipa1, yeah. that is a good idea, we will add some tour to the page, in which it will walk the user through the process 

**minipa1** : ok, cool, then I'll put it on my to-do list. We're sticking to the current wikiwoods.db for now, right?

**stultus** : minipa1, yeah. 

**minipa1** : great stuff...

**minipa1** : then I'll go off and do my things... good night :)

**stultus** : minipa1, also I've added a small caching(for experimental purpose) to the pear selection method 

**minipa1** : oh wow, nice!

**stultus** : minipa1, it will cache the last 2048 results 

**stultus** : minipa1, so if we are using the same queries again, it will just return the past result.  instead of calculating again. 

**stultus** : minipa1, I think it is working 

**minipa1** : very nice. I'm forever visiting the same pages...

**stultus** : minipa1, I've pushed  code here - https://github.com/stultus/PeARS

**minipa1** : thanks! will take a look!

**stultus** : minipa1, sure 

**stultus** : minipa1, so good night :) 

**minipa1** : thanks a lot!! Good night :)

**minipa1** : Good night, gem :)

**stultus** : minipa1, :) 

* minipa1 (~minipa@93-34-239-8.ip52.fastwebnet.it) has left #pears

**stultus** : gem, good night  :-)
