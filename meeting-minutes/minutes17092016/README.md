# Minutes of 17.09.2016

Attendees: Aurelie, Behrang, Nandaja, Shobha

## Items to discuss

* Discuss design requirements with Jaison:

adjourned, as Jaison couldn't make it. Perhaps we send him a mail with
requirements?

* State of DHT

Nandaja has the main part of the DHT ready, but needs data in an appropriate
format to add to the hash table. She is working on the daemon to produce this
data. We feel that we should probably first test the hash table itself with
whichever data. Behrang suggested producing random data for this, or use some
we already have. Aurelie will link up with Nandaja to discuss requirements.

* State of indexer, opinions on real-time indexing (daemon, add-on, both?)

Nandaja feels we should really have a browser-independent indexer, so in that
sense the daemon is a good idea. The add-on produced by Andrey is a webext,
though, so that should actually (mostly) be browser-independent. It would be
nice to be able to indicate one's privacy choices for individual pages, and an
add-on is a good idea from this point of view. On the other end, we perhaps
just want to have an install which takes care of everything in a separate
program window, not linked to the browser. We'll see how the various solutions
evolve.

* The repos are in a mess. We're not always very good at checking the
  discussion board.

We have several pull requests open that don't need to be. Many issues haven't
been marked as solved. Aurelie to give everything a clean.

* Documentation

Adjourned to next time.

* Cambridge update

Adjourned. (Really not enough time today!)

* Behrang's PoP python code

Aurelie hasn't had time to look into it first. But we should talk about this in
Cambridge to see how we can implement the open vectors idea.
