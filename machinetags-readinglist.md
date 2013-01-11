machinetags-readinglist
==

This document was originally compiled for the [Machine Tags: Theory, Working Code and Gotchas (and Robots!)](http://aaronland.info/talks/mw10_machinetags/) workshop at the 2010 Museums and the Web conference, in Denver. This is what I wrote at the time:

_This is an outrageously long reading list. It is not expected that youʼll sit down one day and diligently visit each 
site. Rather, I hope that you will hang on to this list as something you might think to look at over coffee or while youʼre 
waiting for another task to complete and it will stir your imagination and send you off in an entirely other direction. People 
really have said this much about “machine tags” and it really is this varied and
this interesting!_ 

This is an early draft and re-jiggering of that original document which was
produced as a PDF file. The formatting (as Markdown) probably still needs some
finessing.

The order and structure of the content reflects how I chose arrange this in
document 2010. There's nothing precious about and it is entirely open to being
changed, especially as new entries are added.

Sadly, there's probably a some amount of linkrot so it might be worth archiving
local copies of links (somewhere in this repository).

Introducing Machine Tags
--

This is an excepted version of a piece originally published on Flickr, 24 January 2007

http://www.flickr.com/groups/api/discuss/72157594497877875

### What are machine tags?

Machine tags are tags that use a special syntax to define extra information about a tag.

Machine tags have a namespace, a predicate and a value. The namespace defines a class or a facet that 
a tag belongs to ('geo', 'flickr', etc.) The predicate is name of the property for a namespace ('latitude', 
'user', etc.) The value is, well, the value.

Like tags, there are no rules for machine tags beyond the syntax to specify the parts of a machine tag. 
For example, you could tag a photo with :

* flickr:user=straup

* flora:tree=coniferous

* medium:paint=oil

* geo:quartier="plateau mont royal"

* geo:neighbourhood=geo:quartier

Flickr has already used machine tags, informally, on a couple of occasions :

* When we launched Maps, we provided a way for people who had "geotagged" their 
photos to import their location data. This was done using the "geo:lat=..." and "geo:lon=..." tags.

* When a user tags an event with an upcoming ID (for example : 
"upcoming:event=81334") we display a link back to the upcoming.orgsite. A similar example is the excel-
lent "Flickr Upcoming Event" greasemonkey script : http://userscripts.org/scripts/show/5464

Dan Catt wrote a very good piece about machine tags - he called them "triple tags" - last year : http://geobloggers.com/2006/01/11/advanced-tagging-and-tripletags/

Update : Dan's gone and written another excellent piece about all of this stuff now that we've launched 
machine tags: http://geobloggers.com/2007/01/24/offtopic-ish-flickr-ramps-up-triple-tag-support/

### What is the spec for machine tags?

Machine tags are divided in to three parts :

#### A "namespace" :

Namespaces MUST begin with any character between a - z; remaining characters MAY be a - z, 0 - 9 and 
underbars. Namespaces are case-insensitive. 

#### A "predicate" :

Predicates MUST begin with any character between a - z; remaining characters MAY be a - z, 0 - 9 and 
underbars. Namespaces are case-insensitive. 

#### A "value" :

Values MAY contain any characters that a "plain vanilla" tags use. Values may also contain spaces but, 
like regular tags, they need to wrapped in quotes.

Namespace and predicates are separated by a colon : ":"

Predicates and values are separated by an equals symbol : "="

For example :

* flickr:user=straup

* geo:locality="san francisco"

### How do I add machine tags?

By adding tags! No, really.

Machine tags are added *exactly* the same as any other tag whether it is done through the website or the 
API.

When the Flickr supercomputer processes your tags, we take a moment to check
whether it is a machine tag. If it is we leverage the powerful Do What I Mean engine to, well, do what you 
mean.

### How do I query machine tags?

Via the API!

Specifically, using the "machinetags" parameter in the 'flickr.photos.search' method. Like tags, you can 
specify multiple machine tags as a comma separated list.

Can I query the various part of a machine tag?

Yes. Aside from passing in a fully formed machine tag, there is a special syntax for searching on specific 
properties : 

#### Find photos using the 'dc' namespace :

	{"machine_tags" => "dc:"}


#### Find photos with a title in the 'dc' namespace :

	{"machine_tags" => "dc:title="}

#### Find photos titled "mr. camera" in the 'dc' namespace :

	{"machine_tags" => "dc:title=\"mr. camera\"}

#### Find photos whose value is "mr. camera" :

	{"machine_tags" => "*:*=\"mr. camera\""}

#### Find photos that have a title, in any namespace : 

	{"machine_tags" => "*:title="}

#### Find photos that have a title, in any namespace, whose value is "mr. camera" : 

	{"machine_tags" => "*:title=\"mr. camera\""}

#### Find photos, in the 'dc' namespace whose value is "mr. camera" :

	{"machine_tags" => "dc:*=\"mr. camera\""}

### Are machine tag namespaces reserved?

No. Anyone can use a namespace for anything they want.

If you are concerned about colliding namespaces you should consider adding an additional machine tag 
to define your namespace. For example :

	dc:subject=tags
	xmlns:dc=http://purl.org/dc/elements/1.1/

Like tags, in general, we expect (hope?) that the community will develop its own standards by consensus 
over time.

### Is the predicate _really_ a predicate?

You are in a dark cave. In the corner is a fire and a man making bunny shadows on the wall with his 
hands. Whether or not it's really a 'predicate' depends on how much time you spend on the semantic-web  
mailing list. ;-)

It's close enough to being a predicate that it makes for a good short-hand.

### Wait, aren't machine tags just RDF?

No, machine tags are not RDF; they could play RDF on television, though.

See also : http://weblog.scifihifi.com/2005/08/05/meta-tags-the-poor-mans-rdf

### Huh, what is RDF ?

RDF Describes Flickr. That's really all you need to know about RDF. 

The story we (flickr) told ourselves
==

### Introducing Machine Tags

"We are rolling out a new feature called "machine tags" that allows users to be more precise in how they tag, 
and how they search, their photos."

http://www.flickr.com/groups/api/discuss/72157594497877875/

### Flickr Developer Blog » Machine Tags, last.fm and RockʼnʼRoll

http://code.flickr.com/blog/2008/08/28/machine-tags-lastfm-and-rocknroll/

### Flickr Developer Blog: Wildcard Machine Tag URLs

"Which brings us to the part where I tell you that weʼve added the ability to search for machine tagged photos in 
plain old tag URLs (as well as in tag searches on the Flickr search page) using the facetted query syntax that 
has always been available in the API."

http://code.flickr.com/blog/2008/07/18/wildcard-machine-tag-urls/

### Flickr Developer Blog : Machine Tag Hierarchies

"For example, lots of people have added exif: related machine tags to their photos but there hasnʼt been a way 
to know what kind of EXIF data has been added: exif:model? exif:focal_length? exif:tunablaster? Or what about 
all the planespotters who have been diligently adding machine tags to their photos using the aero namespace: 
What are the predicates that theyʼre tagging their photos with?"

http://code.flickr.com/blog/2008/12/15/machine-tag-hierarchies/

### Flickr Developer Blog : extra:extra=extra

"Machine tag 'extras' are what we call the entire process of using a machine tag as a kind of foreign key to 
access data stored on another website. Small pieces (of data) loosely joined (by the Internets)."

http://code.flickr.com/blog/2009/07/06/extraextraextra/

### Flickr Developer Blog: Thatʼs maybe a bit too dorky, even for us.

"The technical terms for this process is “Adding the machine tags extra love“. You may have noticed that there 
are a bunch of other key-value pairs in that example, like the name of the architect, that we donʼt do anything 
with. Which attributes are we looking for, then? The short answer is: Not most of them. The complete list of map 
features in OSM is a bit daunting in scope and constantly changing. It would be nice to imagine that we could 
keep pace with the discussions and the churn but thatʼs just not going to happen. If nothing else, the transla-
tions alone would become unmanageable."

http://code.flickr.com/blog/2009/09/28/thats-maybe-a-bit-too-dorky-even-for-us/

### Flickr Developer Blog: Small Bridges (to Proximate Spaces)

"You can either add the special machine tag yourself or ask noticin.gs to do it for you automatically. To enable 
automagic machine tagging youʼll need to log in to noticin.gs and change the default settings. If youʼre worried 
about creating yet another account for an yet another online service, donʼt be: noticin.gs uses the Flickr Auth 
API itself to manage user accounts so “logging in” is as simple as authorizing noticin.gs to access your Flickr 
account (the way you would any other Flickr API application)."

http://code.flickr.com/blog/2009/10/19/small-bridges-to-proximate-spaces/

Stuff that's influenced me along the way
--

### Simon Willisonʼs notes from Tom Coatesʼ "Native to a Web of Data"

"Start designing with data (objects), not with pages"

http://simonwillison.net/notes/2006/summit/coates.txt

### Dave Beckett : Semantics Through the Tag

"[H]ow to go from a Tag to the Semantics that a human can understand."

http://xtech06.usefulinc.com/schedule/paper/135

### Matt Biddulph: Mobile Social Location

"Concordance A major problem when you work with disparate large datasets is mapping information from data-
set to dataset. A concordance between two datasets (e.g. mapping from Yahooʼs WOE place IDs to Geonames 
IDs) allows us to combine data in interesting new ways. Flickr is implicitly building sets of concordances through 
their machine tag integrations. A photo of a restaurant in San Francisco may have tags indicating its IDs both in 
Foursquare and in Dopplr. Hopefully theyʼll open up this concordance data through their API eventually."

http://www.slideshare.net/mattb/mobile-social-location

### Dr. Macro's XML Rants: I was wrong (sort of) about namespaces

http://drmacros-xml-rants.blogspot.com/2006/02/i-was-wrong-sort-of-about-namespaces.html

Paul Mison
--

### Paul Mison: Flickr, EXIF, Machine Tags

http://blech.vox.com/library/post/flickr-exif-machine-tags.html

### Paul Mison: Snaptrip: some thoughts

"Why a website? Well, I thought I'd like a nice interface as much as anyone, and I also know that to make a 
machine tag truly useful you need as many people as possible using it. Asking folk to download a script, get a 
key, and use a command-line interface - or no interface at all - isn't going to work."

http://blech.vox.com/library/post/snaptrip-some-thoughts.html

### Paul Mison: A Flickr Machine Tag Browser

"it's still sufficient for users to see that the astrometry.net system has been able to solve about 85% of the im-
ages it's processed; that three images have had an ImageMagick Lomo effect applied before upload; the names 
of Len Peralta's monsters by mail; and where people take screenshots in Second Life."

http://blech.vox.com/library/post/a-flickr-machine-tag-browser.html

### Paul Mison: Flickr Machine Tag Browser on Flickr

This client-side application uses the flickr.machinetags API methods to implement a browser for machine tags 
in use across the Flickr website.

http://www.flickr.com/services/apps/72157609564084232/

### Paul Mison: Thoughts From the Open Platform.

"More specifically, machine tags are foreign keys. (Well, they can be other things, too. But they're very good at 
that in particular.) For example, I can imagine a script that adds tags to delicious based on the Guardian's tags 
for their own stories, but prefixed with "guardian:" or "guardian:tag=" so that they don't clutter my tags. Similarly, 
snaptrip links Flickr to Dopplr, like the popular lastfm: and upcoming: machine tags, while the recently-launched 
Friends on Flickr Facebook app uses, guess what, facebook:user= machine tags."

http://husk.org/blog/arch/open_platform.html

Astrotags
--

### Flickr Developer Blog : "Introducing astrotags"

"Weʼve written about astrotags before, in a couple of posts titled “Found in Space” and “Tags in Space“, and 
earlier this year Fiona Romeo, Head of Digital Media at the National Maritime Museum, spoke about the Obser-
vatoryʼs astrotagging project asking the question “whatʼs the space equivalent of geotagging”? at Webstock09."

http://code.flickr.com/blog/2009/09/16/introducing-astrotags/

### Introducing astrotags on Vimeo

"Astrotags are a new way to label your astronomy photos with their celestial subject and its location. This short 
film, made by Jim Le Fevre and Mike Paterson for the Royal Observatory's Astronomy Photographer of the Year 
exhibition, shows you how. So have a watch, then astrotag your pictures at the Astronomy Photographer of the 
Year group on Flickr. If everyone joins in we can make a beautiful and accurate map of the night sky... so pass 
the word on."

http://www.vimeo.com/6469344

### Flickr Developer Blog : Found in space

"Needless to say this is one of the coolest uses of Flickr groups and the API that weʼve ever seen. I recently 
discussed the project with team member Christopher Stumm, since he was the one who had the idea to hook it 
into Flickr."

http://code.flickr.com/blog/2009/02/18/found-in-space/

### Fiona Romeo and Natasha Waterson: Flickr as Platform: Astronomy Photographer of the Year

"To build extra interest, weʼve invited professional astronomers to join the group and curate their own galleries 
from the pool. Among them will be non-UK and US astronomers and women – so addressing both our aims on 
these fronts. We hope that from now until the competition closes there will be a new ʻguest-curated ʼ gallery 
every month. The astronomers that produce them will also be invited to contribute to discussions about the 
science behind the pictures theyʼve chosen, and about their professional work. We think this will complement 
the active discussions about how to photograph astronomical subjects, and encourage members to create their 
own Astronomy Photographer of the Year galleries."

http://www.archimuse.com/mw2010/papers/romeo/romeo.html

### Flickr celestial coordinates

"An open table definition which extends the flickr API to add celestial coordinates, RA and Dec, to flickr photos. 
Values are parsed from flickr machine tags and returned as a new table, flickr.photos.astro, with columns for 
photo id, title, url and coordinates. This should allow location-based searching for astro photography."

http://developer.yahoo.com/hacku/hackuhandler.php?appid=us&op=showhack&hackid=279

### Mad Astronomy: The Robot Who Helps Astronomers Identify Stars

"Eventually a group of university researchers created a robot for her who can look at any photograph of a group 
of stars and figure out where they are, simply by using geometry. The robot exists entirely in software, and lives 
in the museum's Flickr photo storage account online."

http://io9.com/5169232/the-robot-who-helps-astronomers-identify-stars

### Flickr/Google Sky mashup with YQL

http://eatyourgreens.org.uk/testapps/yql/

### How the Astrometry.net robot works

"The Astrometry.net robot makes astrometry much easier! It finds photos of the night sky on Flickr and auto-
matically annotates them with astronomical information using notes and machine tags."

http://www.nmm.ac.uk/visit/exhibitions/astronomy-photographer-of-the-year/astro-robot/

noticin.gs
--

### noticings: the blog - Flickr machine tags + more fine features

"When you add the tag noticings:id=x to your photos, Flickr automatically fetch details of the noticing and its 
scorings from us and display it alongside the photo. To make this super easy for you to do, Noticings can write 
these tags for you, so you donʼt even need to it yourself. To turn it on for your account, sign into Noticings, click 
on ʻyour accountʼ, and change your machine tag settings. Weʼll start updating your photos within 24 hours, so 
you might need to wait a while."

http://blog.noticin.gs/post/214569483/flickr-machine-tags-more-fine-features

WildlifeNearYou
--

### WildlifeNearYou can now tag your Flickr photos for you | WildlifeNearYou

"The first four machine tags identify which photo, species, trip and place on WildlifeNearYou are associated with 
the image. The identifiers are the same as the ones we use for our wlny.eu URL shortener, so you can visit 
wlny.eu/s8a to see our species page about squirrels."

http://www.wildlifenearyou.com/blog/2010/feb/4/tag-flickr-photos/

### Flickr Developer Blog : 5 Questions for Simon Willison

"This is pretty powerful stuff, and itʼs all a natural consequence of writing machine tags back to Flickr." 

http://code.flickr.com/blog/2010/02/10/5-questions-for-simon-willison/

Burning Man
--

### Flickr Blog: Burning Man Machine Tags

"For all of those going to Burning Man this year, you can now tag your photos on Flickr and have them show up 
on the Burning Man Earth pages for theme camps, events, and art installations."

http://blog.flickr.net/en/2009/08/28/burning-man-theme-camp-machine-tags/

### Burning Man Gets an API (and a Whole Lot More) - O'Reilly Radar

"There is also a move to take advantage of Flickr's machine tags. For example if you take a picture of Area 47 
(with the online directory entry: http://earth.burningman.com/brc/2009/themecamp/2234/) then use 
burningman:camp=2234. The photo will appear on that locations page. We will see how many photos end up 
using these machine tags. I suspect that V2 of the iPhone app will add a camera that can apply those tags 
automatically and that we'll see more uptake then."

http://radar.oreilly.com/2009/08/burning-man-gets-an-api-and-a.html

### "Lookup Burning Man Machine Tags" tool

http://jsbin.com/ogeku/

Open Library
--

### Open Library Blog ― Small Pieces, Loosely Joined

"There was a funny example yesterday, where dumbledad asked whether it was OK to tag this “action shot” of 
himself reading a book sitting outside with the openlibrary:id= machine tag. The response is, yes! Go for it! Or, 
create your own machine tag that seems to work for you, perhaps openlibrary:actionshot= or 
openlibrary:inside=, and weʼll just see what happens."

http://blog.openlibrary.org/2009/07/08/small-pieces-loosely-joined/

### James Bridle: Flickr + OpenLibrary = Bookdata goodness

"I think itʼs really important we start moving beyond covers as the defining “image” of a book - so in particular, I 
hope people start tagging interior photos. Iʼm also aware of the possible uses at projects like the Book Seer and 
bkkeepr (as Tom notes), so… well, weʼll wait and see…"

http://booktwo.org/notebook/flickr-openlibrary-bookdata-goodness/

### Tom Taylor: extra:extra=extra

"Perhaps augmenting my reading history on Bkkeepr, with photos Iʼve taken of quotes and pages. Or knitting 
together photos of places with geodata, as a way of letting people explore the places mentioned in stories."

http://scraplab.net/2009/07/06/extraextraextra/

Presentations
--

### Harry Chen: Machine Tags

A really fantastic presentation by Harry Chen (ed.)

http://www.slideshare.net/hchen1/machine-tags

### Aaron Straup Cope: rose:rose=rose

http://aaronland.info/talks/hackdayuk07/

Open Plaques
--

### Open Plaques: Building an 'open content' community from scratch

"Launching initially at a developer 'Hack Day' in London, Open Plaques (http://www.openplaques.org) aims to 
be a one-stop resource for information plaques and heritage markers. Data is manually collected and curated 
by a growing community of enthusiasts, as well as being donated by supportive heritage organisations. Photo-
graphs are added via Flickr, using 'machine tags' which link a photo to an individual plaque (and which also 
allow geo co-ordinates to be imported)."

http://www.archimuse.com/mw2010/abstracts/prg_335002264.html

### Frankie Roberto: Open Plaques project update

"To link them together, I used special tags called ʻmachine tagsʼ, which are like normal tags except that they 
contain some slightly more structured data. Itʼs very simple though – each plaque on the Open Plaques website 
has an ID number (which can be found at the end of the URL), and the corresponding machine tag for that 
plaque is openplaques:id=999 (where 999 is the ID number). Another script then uses the Flickr API to find all 
the photos tagged with a relevant machine tag, checks to see if they are Creative Commons licenced, and then 
to displays them on the Open Plaques website, with a credit and a link back to the Flickr photo page"

http://www.frankieroberto.com/weblog/1454

Dopplr
--

### Matt Jones: Dopplr/Flickr machine-tagging

""This popped up on Flickr this week I think, and Iʼm finding it quite addictive to create places on Dopplrʼs “Social 
Atlas” just to be able to nab a shortcode to use as a machine tag on my flickr pictures of lunch and have the 
name of the place appear automagically…"

http://magicalnihilism.com/2009/06/20/dopplrflickr-machine-tagging/

### Dopplr Blog: Help illustrate the Social Atlas on Flickr

"When you take a picture of a great restaurant, hotel or other place to explore, you can now add a special ʻma-
chine tag ʼ when you upload it to Flickr. Within minutes, Flickrʼs computers will talk to Dopplrʼs computers and 
figure out the place you mean, adding a direct link with the correct title on the relevant pages."
 
http://blog.dopplr.com/2009/07/06/help-illustrate-the-social-atlas-on-flickr/

Jeremy Keith
--

### Adactio: Journal―Welcome to the machine tag

"Thereʼs something about the mix of rigidity and haphazardness in machine tags that appeals to me. While they 
all share the same structure, everyone is free to invent their own usage. If machine tags were required to go 
through a specification process we would have event:lastfm=... and event:upcoming=... instead of 
lastfm:event=... and upcoming:event=... but really, it simply doesnʼt matter as long as people are actually doing 
the tagging."

http://adactio.com/journal/1535

### Adactio: Journal - Ghost in the Machine Tags

"For now, Iʼve gone ahead and integrated Flickr machine tagging here… but this works from the opposite direc-
tion. Instead of tagging my blog posts with flickr:photo=[ID], Iʼm pulling in any photos on Flickr tagged with 
adactio:post=[ID]."

http://adactio.com/journal/1274

### Adactio: Journal―Small pieces, loosely joined by machine tags

http://adactio.com/journal/1617/

### Adactio: Journal - Machine Tags of Loving Grace

http://adactio.com/journal/1277

### Adactio: Journal―Machine tag browsing

"After I started rewarding machine tagging on Huffduffer with API calls to Amazon and Last.fm, people started 
using them quite a bit. But when it came to displaying tag clouds, I wasnʼt treating machine tags any differently 
to other tags. Everything was being displayed in one big cloud. I decided it would be good to separate out ma-
chine tags and display them after displaying “regular” tags. That started me thinking about how best to display 
machine tags."

http://adactio.com/journal/1580

### Adactio: Journal―Machine-tagging Huffduffer

"I set aside a little time to do a little hacking with Amazonʼs API. Now you can tag stuff on Huffduffer with ma-
chine tags like book:author=steven johnson, book:title=the invention of air or music:artist=my morning jacket. 
Other namespaces are film and movie. Anything matching that pattern will trigger a search on Amazon and 
display a list of results."

http://adactio.com/journal/1547

### Adactio: Journal―Machine-tagging Huffduffer some more

"So when I wanted to find a Last.fm userʼs profile picture―having figured out through Googleʼs Social Graph 
API when someone on Huffduffer has a Last.fm account―it made far more sense for me to use hKit to parse 
the microformatted public URL than to use the API method."

http://adactio.com/journal/1548

Semantic Web
--

### Buzz Anderson: Meta Tags, The Poor Man's RDF

weblog.scifihifi.com/2005/08/05/meta-tags-the-poor-mans-rdf

### Geonames, rdf, triplr, json, Yahoo! Pipes and the Semantic Web, oh my!

http://geobloggers.com/2007/03/31/geonames-rdf-triplr-json-yahoo-pipes-and-the-semantic-web-oh-my/

### Codelog: Freebase, Flickr and Machine Tags

"I made the Flickr API in Freebase / Acre to a very limited extent (patches welcome!); and then on top of that, 
did a very basic find things on flickr tagged with wikipedia tags that can be attached to freebase."

http://clockwerx.blogspot.com/2009/10/freebase-flickr-and-machine-tags.html

### RDF-3T - RDF in Machine Tags

"RDF-3T is a Metaformat(a language used to describe another language [3]) that uses a Triple Tag syntax to 
describe RDF triples in XHTML."

http://weborganics.co.uk/RDF-3T/

### More Tags Released to the Linked Data Cloud - Open Blog - NYTimes.com

"Like the 5,000 person-name subject headings released last October, we have mapped our latest crop of sub-
ject headings to DBpedia, Freebase and ― in the case of our geographic subject headings ― GeoNames."

http://open.blogs.nytimes.com/2010/01/13/more-tags-released-to-the-linked-data-cloud/

### Geonames machine tags  (GeoNames Blog)

http://geonames.wordpress.com/2007/03/29/geonames-machine-tags/

### danbriʼs foaf stories » Flickr & MusicBrainz Machine tags: If youʼve got it, flaunt it

http://danbri.org/words/2009/03/03/397

### namespace lookup for RDF developers | prefix.cc

"The intention of this service is to simplify a common task in the work of RDF developers: remembering and 
looking up URI prefixes."

http://prefix.cc/

Wikipedia
--

### Wikipedia Machine Tags

http://hackday.bigmedium.com/about.html

### Lightning! Blimps! Submarines! And, um, Machine Tags!

“So my idea was to create a machine-tag format based on Wikipedia topics, allowing any content creator to tag 
content with any topic in Wikipedia. By using Wikipedia as an index, this format provides very specific identifica-
tion of content across a vast knowledge domain. Call it the Dewey Decimal System for the web: “The Wiki 
Decimal System.”

http://globalmoxie.com/blog/hackday-wikipedia-machine-tags~print.shtml

### Flickr: Wikipedia Loves Art

“In order to properly score everyone's entries will be adding machine tags [they:look="like this"] to your photo-
graphs. So, please don't delete these tags, even if they look a little weird.”

http://www.flickr.com/groups/wikipedia_loves_art

### Brooklyn Museum: Wikipedia Loves Art: Lessons Learned Part 3

“Erin has cleaned the entire pool and scored every entry. In some cases, this meant 3 or more machine tags per 
clean photo. Iʼm sure sheʼll give you the total tomorrow, but the most basic math would indicate something along 
the lines of 30,000+ machine tags.  Please keep in mind, thatʼs 30,000 tags applied by hand to organize and a 
pool of 13,000 images. To say that our plans here didnʼt scale is putting it a bit mildly. Erin, we all seriously owe 
you more than one drink.”

http://www.brooklynmuseum.org/community/blogosphere/bloggers/?p=379

RightScale
--

### RightScale Release: RackSpace, RightLink, Chef, Machine Tags, VPC, and more!

"But thereʼs more! Weʼve started to add Flickr style machine tags to RightScale resources. A machine tag is a 
tag that follows a special triplet syntax of namespace:predicate=value and the purpose of machine tags is to 
allow anyone or any external application to attach metadata to RightScale resources. Right now tags are only 
available for Servers, Images, and EBS Snapshots. Rather than start attaching tags everywhere we preferred to 
start using tags ourselves for something concrete so we can ensure we have a good feature set. Weʼre using 
tags now for snapshots to control the rotation of backup snapshots and to organize snapshots of multi-volume 
stripes. Weʼll soon use tags to encode the features provided by images, e.g. whether theyʼre RightImages, sup-
port RightLink, support the freezing of repositories, etc. But most importantly weʼll add API access to tags so 
you can attach your automation to tags."

http://blog.rightscale.com/2009/09/16/rackspace-rightlink-chef-machine-tags-vpc/

### RightScale ServerTemplate Library and Machine Tags - RightScale Blog

"We introduced Flickr style machine tags recently and weʼre expanding their use with this release. One of the 
really exciting new features is that servers now have tags and weʼve integrated the tags with the routing of mes-
sages between servers, with Chef (via the RightLink agents) and with the UI. All this is still in alpha but itʼs start-
ing to take shape. Our first real use-case is the registration of application servers with load balancers. The way 
it works is that when a load balancer comes up and is ready for operation it adds a “loadbalancer:lb=www” tag 
to say “Iʼm a load balancer for the www vhost”. When an app server starts up, it requests all servers in the de-
ployment with a “loadbalancer:lb=www” tag to run a Chef recipe that adds the app server to the load balancer 
rotation. This way, the app server doesnʼt need to know which or how many load balancers there are. The tag 
matching, communication, and running of the Chef recipe are all done by the RightLink agents."

http://blog.rightscale.com/2009/10/28/rightscale-servertemplate-library-and-machine-tags/

Encyclopedia of Life

### Encyclopedia of Life - taxonomic links

"Give us your feedback on the new taxonomic URLs that we are trialling. Just add the name (Latin or vernacu-
lar) of the organism to the link: www.eol.org/platypus or www.eol.org/lugworm." -- EOL has no permalinks for 
news items; just linking to ...uh the news page so I have something to store in del.

http://www.eol.org/content/news

### Flickr: Encyclopedia of Life Images

"The image is tagged using machine tags with the scientific name of the organism(s) featured..."

http://www.flickr.com/groups/encyclopedia_of_life/

### Flickr: Discussing List of acceptable machine tags in Encyclopedia of Life Images

"Here is the official list of machine-readable tags recommended for the group. To suggest improvements, leave 
a message in the Machine tag thread."

http://flickr.com/groups/encyclopedia_of_life/discuss/72157612488733900/

Other projects
--

### Phil Gyford: Flickr machine tags for film photos

http://www.gyford.com/phil/writing/2009/11/04/flickr.php

### Typedia: Blog: Machine Tags for Type

"Working with the folks at Flickr and smart gents like Tom Coates, weʼve defined a set of machine tags that will 
specify a good chunk of the information about the type in an image. Even if the minimum you feel comfortable 
tagging a photo with is the “face” machine tag, it will go a long way towards making Typedia more useful. Hereʼs 
the syntax for tagging a typeface, style, foundry, and designer:"

http://typedia.com/blog/post/machine-tags-for-type/

### Inside Photophlow: an interview with Neil Berkman

“One of my favorite features makes use of  machine tags. We let you specify custom “photo emotes” – for ex-
ample if you type /smile as a chat message weʼll show a photo youʼve tagged as  phlow:emote=smile.”

http://code.flickr.com/blog/2008/04/24/inside-photophlow-an-interview-with-neil-berman/

### The Code4Lib Journal - Developing an Academic Image Collection with Flickr

http://journal.code4lib.org/articles/74

Theory and practice
--

### Flickr: Machine Tags Group

"Discussion of the new machine tags feature in the Flickr API and possibly the development of a standardized 
system."

http://www.flickr.com/groups/mtags/

### ActiveState Launches New and Improved Code Site | ActiveState Blog

"Improved tagging – Including the addition of structured tags (also known as machine tags) to allow contributors 
to be more precise in how they tag and make searching for specific recipes more effective." -- why did no one 
tell me about this?

http://blogs.activestate.com/2010/02/activestate-launches-new-and-improved-code-site/

### Speaking and writing webscale identifiers (Jon Udell)

"Iʼve long imagined a class of equivalence services that would help us bridge the gap between vocabularies we 
can speak and write and those weʼll never speak and need help to write."

http://blog.jonudell.net/2009/09/17/speaking-and-writing-webscale-identifiers/

### Joining web namespaces (Jon Udell)

"It would be straightforward to create a service that would take the Yahoo Pipes trick to the next level. Instead of 
editing and saving a Yahoo Pipe, youʼd just command that service to merge the set of feeds for some tag. That 
command might best take the form of a URL:"

http://blog.jonudell.net/2010/03/09/joining-web-namespaces/ 

### Unthinkingly.com » Archive » “Slashtags” for citizen editors

"Common opinion seems to be that they are too “dorky” to be usable at this point, considering especially that 
any good taxonomy is constantly in slight flux. (Though Flickr has made great use of them to kick of custom 
actions in their UI)."

http://unthinkingly.com/2009/11/09/slashtags-for-citizen-editors/

### FaceTaggr on Flickr 

"Yahoo Open Hack Day ʻ08 took place this weekend (a year ago), and although employees & interns arenʼt 
supposed to produce a hack, I did it anyways (take that!). Itʼs nothing big, I wrote a greasemonkey script that 
will add a list of your contacts on a flickr photo page. When you click on the personʼs name, a machine tag of 
their flickr username will be added to the photo. I call it facetaggr."

http://www.flickr.com/photos/tehf0x/3999116128/in/pool-flickrhacks/

### Flickr: Discussing "Friends on Flickr" for Facebook in Flickr API

"I've developed a Facebook Platform application for Flickr users called "Friends on Flickr" that focuses on 
Facebook friend tagging of Flickr photos using machine tags and a simple, straightforward profile tab for sharing 
both your own public content and content tagged with your Facebook id in the larger public repository."

http://www.flickr.com/groups/api/discuss/72157615334960342/

### DiSo / activity-streams-machine-tags

"strict parsers tend to throw out stuff they don't recognize, and machine tags, encapsulated in Atom category 
elements, would maintain their fidelity over time"

http://wiki.diso-project.org/activity-streams-machine-tags

### Machine tagging relationships | FactoryCity

"By machine tagging relationships, not only do we maintain the fidelity of the relationship with context, but we 
inherit a means of querying against this dataset in a way that maps to the origin of the relationship." 

http://factoryjoe.com/blog/2008/05/25/machine-tagging-relationships/

### Flickr: Discussing Commons Curator in Flickr Commons

"Develop a collection you'd like to see, and tag images in that set with the machinetag 
commons:collection="your-slug-here". Slugs can be anything, provided they are only lowercase letters and 
hyphens (just for ease-of-coding)"

http://flickr.com/groups/flickrcommons/discuss/72157611394509319/

### Blogging Section of SLA-IT: Flickr Machine Tags

http://sla-divisions.typepad.com/itbloggingsection/2008/07/flickr-machine.html

### about Scriblio : Spelling Suggestions & Machine Tags

"The machine tag support will allow fixing of records and even original cataloging inside Scriblio. ... The catalog-
ing for Beyond Brown Paper archive is done entirely in machine tags."

http://about.scriblio.net/scribbles/108

### Push Button Paradise | Blog Archive | Machine tags

http://dubinko.info/blog/2008/01/23/machine-tags/

### Amazon SimpleDB thoughts - snarfed.org

"tuplespaces"

http://snarfed.org/space/amazon+simpledb+thoughts

### Messing Around With Metadata - Open - Code - New York Times Blog

http://open.blogs.nytimes.com/2007/10/23/messing-around-with-metadata/

### Hack Day: Machine Tags : Meaningful Data

http://meaningfuldata.wordpress.com/2007/06/21/hack-day-machine-tags/

### Brain Off : Hacking Google Street View

http://brainoff.com/weblog/2007/06/03/1253

### Machine tags and ISBNs | clagnut/blog

"Is an ISO namespace something likely to be used in the future? Is it fatally flawed, and if so how would you 
suggest machine tagging ISBNs instead?"

http://clagnut.com/blog/1907/

### Caroline Mockett: Flickr And Self-Referential Folksonomy

"As long as you know that a person in one of your pictures is a Flickr member, you ought to be able to drag their 
icon onto a picture to set up the tagging, even if they are not in your friends, family or contact lists"

http://cazmockett.blogspot.com/2007/02/flickr-and-self-referential-folksonomy.html

### Rise of the machine tags

http://ebiquity.umbc.edu/blogger/2007/01/28/rise-of-the-machine-tags/

### dystmesis  : Fields are from Mars and Tags are from Venus: oh really?

http://dystmesis.net/2007/01/26/fields-are-from-mars-and-tags-are-from-venus-oh-really/

### cldwalker's has_machine_tags at master - GitHub

"A rails tagging plugin implementing flickr's machine tags + maybe more (semantic tags)"

http://github.com/cldwalker/has_machine_tags/tree/master

### Newspaper mtags bookmarklet

"This is just a simple helper script that generates machine tags from an article on the National Library of Austra-
lia's Australian Newspapers site. Just drag this Newspaper mtags bookmarklet to your bookmarks toolbar, find 
an article, then click on the bookmarklet. This page will open with easy-to-use, hand-crafted machine tags ready 
to do your bidding. The machine tags will enable you to assert a semantic relationship between the item that 
you tag and the newspaper article."

http://semweb-helper.appspot.com/

### Machine Tags in Drupal - Dan Karran's blog

"I think what's really needed is a Machine tags module that plugs into the existing taxonomy system which is in 
the core of Drupal."

http://www.dankarran.com/blog/archives/2007/01/27/machine_tags_in_drupal.php

### Machine Tags module for Drupal

"The machine tags module is meant to fill a void between people-friendly tagging and machine-friendly hierar-
chy."

http://drupal.org/project/machine_tags

### Amazon Machine Tags | Plugins

"Identifies any tag in the machine or triple tag form book:isbn=1234567890 or amazon:asin=1234567890. 
Works with native tags from WordPress 2.3 and later, Bunnyʼs Technorati Tags, and Jeromeʼs Keywords."

http://www.blogdev.info/bd/wordpress/plugins/amazon-machine-tags.htm

### Midgard gets geotagging/machine tags

"Midgard gets geotagging. Midgard's geo capabilities have now been amended by supporting the Flickr-style 
machine tags. This enables people submitting content to Midgard via email or for example Flickr integration to 
position and tag their content easily.”

http://bergie.iki.fi/blog/midgard_weekly_summary-68-march_2nd_2007.html

### Flickr Machine Tags and Amarok - neofreko's posterous

"As we all know, Amarok 2.1 comes with a snazzy Photo widget[3]. This widget will pull photos from flickr, re-
lated to the currently playing song. But what a little bit disappointing is how it pull non relevant photos. But don't 
fret, we have machine tags[1] in Flickr."

http://neofreko.posterous.com/flickr-machine-tags-and-amarok
