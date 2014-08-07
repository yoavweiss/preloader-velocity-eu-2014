Once upon a time, in a land far far away, there was a village.
The village was a humble one, 

4 sheep pass the bridge at a time
HTML is the village leader.
He crosses the bridge, talks to the parser and comes back with a list of
sheep that would eat today.
The parser star passing the sheep over the bridge, four at a time.
Some sheep are important ones, so the parser brings them on their own to
eat while all other sheep wait. They can suddenly speak up and modify
the list.
Feeding took a long while...

Then came preloader.

What if, even if the parser needs to spend quality time with the
important sheep, the rest of the sheep can eat in the mean time?
We already have the list!

Villagers - Web devs
Feeder - parser
Sheep - HTTP requests
Bridge - network


# Past
Once upon a time in a land far far away, browsers were fetching Web
pages.
The way they were doing that was that a user would typein a URL, or go
to a link. The browser would then fetch the HTML and start parsing it.
Once it encountered a subresource that needs downloading, it would add
it to the download queue, and continues parsing out more resources.
But, when the parser encountered a resource that may change the HTML,
mostly javascripts, it would halt and wait for all the resources that
may impact running of this javascript to download and get
evaluated and executed, before it would continue the parsing work.
That meant that for pages with multiple external scripts and CSS files
(which is the lot of them), the resource downloading process was
extremely inefficient.
Users got frustrated by the waiting. Web developers got frustrated by
their poor performing sites. Books were written with workaround
techniques.
And evetually, browsers decided to do something about it.
Around 2007-2008, browsers added, each on its own, a mechanism called
the preloader.
Well, no one actually called it the preloader. IE called it the
look ahead parser, Firefox called it the speculative parser, and in
WebKit it was called the preloadScanner.
The different implementations were different, but the basic idea behind
them was the same. Peek into the HTML coming in from the network and
start an early fetch of the resources that will most probably be requested later on.


## Why did JS and CSS block the parsing anyways?

Well, There are several reasons for that:
* JavaScript can alter the HTML, which means that the parser can
  reliably continue parsing, adding stuff to the DOM and only then run
the javascript. That may cause the javascript to break (since it
rightfully expecting the DOM to be in a certain state when it runs).
It can also mean, if the javascript has a document.write directive, that
all HTML beyond the script tag may be entirely altered.
Consider for a second the following example:
"Script opens an HTML comment using document.write and then images after
it"
* Javascripts (both internal and external) can look into style
  information on the current DOM. That means that if the external CSS
wasn't fully downloaded, the browser have to wait for it to arrive, and
apply it, before running scripts that are later on in the page.
Some browsers optimized that to do that only when scripts actually
include such directives, while others didn't bother with it (citation
needed).

#Present
## How does parsing and preloading work together?
Despite rumors, the preloader is not some weird regex engine.
In order to explain the preloader, a quick detour into how HTML parsing
works - what happens between the time that the browser gets the HTML as
bytes on the wire(less) and the time it has a complete DOM tree.
BLABLABLA
Tokenization & parsing
The preloader basically picks up the HTML tokens from the tokenizer, and
processes them before passing them to the parser.
That means that comments for example won't be detected as actual tags
that require resource loading. 

## Which resources are fetched in the different browsers?

## Where's the spec to all of this

## How can we make sure that all the resources are preloaded?

## How can devs avoid having their resources preloaded?

## Don't assume anything regarding newtork download order

## Controversy

### Can't load MQ based resources
I fixed that. Done!

### Prevents developers from modifying resources before they are downloaded
Never was possible, regardless of preloader

### Prevents dirty hacks

## Resource download priorities

# Future
## Future improvements
### Not going through the main thread
### @import in external CSS
### background images
### Web fonts

# Conclusions
The preloader is your friend! Be kind to him, and he'd be kind with you
and your users load times


