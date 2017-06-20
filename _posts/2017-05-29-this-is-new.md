I'm someone who likes to form quick (and often unsubstantiated) opinions, and I'm someone who doesn't listen to the radio very often. And so, after I spent some time focusing on the background music softly wafting through a [put in fake place], I was convinced that today's pop music isn't danceable. Or how I put it to a friend:


> Me: Music is definitely less dance-y now than it was back in the day, you know? Like - music used to be easier to dance to.

> Not Me: That is definitely not true.

But who's to say what makes a song 'danceable'? [Most](https://www.theodysseyonline.com/what-makes-people-dance) [articles](http://www.npr.org/sections/health-shots/2014/05/30/317019212/anatomy-of-a-dance-hit-why-we-love-to-boogie-with-pharrell) [about](https://www.scientificamerican.com/article/experts-dance/) [the topic](http://www.nytimes.com/2013/10/13/magazine/why-dont-we-dance-anymore.html) feature a question mark in the title, which isn't a strong indicator that we've found a unified groove theory. There's some talk of syncopation and mirror neurons, but the general take on danceability seems to be a lot like obscenity: you know it when you hear it. Who would attempt to put a number on something like that?

Well, **[apparently Spotify](https://developer.spotify.com/web-api/get-audio-features/)**. Not only do they provide data (through their excellent API) about 'danceability' for a song, but they take stabs at other attributes for tracks. Continuous values for seemingly subjective concepts? Sounds good to me!

So in an effort to prove my quick-formed thesis correct - that modern pop music is singularly undanceable - I decided to build a dataset of pop music, as set out by weekly Billboard Hot 100 charts, from 1962 until now, and see if I was right. [Spoiler: not really]

## Some sort of divider

After digging around the Spotify API documentation, I realized there's a ton of different things we can pull out for each track. While I was at it, I decided to pull out the following 'audio features' to look at with this analysis: 

- 'danceability' 
- 'valence' ('the musical positiveness conveyed by a track')
- tempo, as expressed by BPM
- loudness (which seems to b e an average across the track)
- and most nebulously, 'energy', which Spotify describes as a measure of 'perceptual features ...includ[ing] dynamic range, perceived loudness, timbre, onset rate, and general entropy.'

[ *Note: This post is light on the details of getting, transforming, and modeling the data. [Check out this post](#) for more details on the code that got me here.*]

I used Billboard.py for to get the titles, ranks, and convienent Spotify track ids for each chart period, and normalized a few of the audio features that Spotify provides, and loaded the entire thing into a pandas frame: 

{% include display.md %}{:class="ipynb_md"}


Ok great let's just graph everything all at once!

![](http://i.imgur.com/Njbdrd1.jpg){:class="img-responsive"}

Pretty... but not super useful, beyond showing the considerable amount of spread for some of our values. Our goal still is to figure out if music has gotten more danceable over the years. We'll want to find some sort of way of representing the data in a central way. 

Since we are trying to capture the general sound of a period of time, it wouldn't make sense for us to weight super popular songs and smaller hits the same. There's a lot of ways we could do this, but for simplicity let's just assume that a top-5 song is something you are going to hear roughly 10 times for every time you might hear a song on the bottom quarter of the charts. Using this, we use that to create a weighted sample for each chart period, and then use that to find a weighted median.

Additionally, we can that weighted data and plot some trend lines in the data using a polynomial regression to give a loose idea of where everything is going. Here's a chart showing the last 55 years for danceability, valence, and energy - which should give us an interesting view into how pop music might have changed in the last half century. 

![](http://i.imgur.com/43sCe6p.png){:class="img-responsive"}

Some insights: 

- Not only are we not in a drought of danceable tunes, we seem to be somewhere near a high point since our data started. In fact, music since 1980 has had much higher danceability values than before. We'll dig deeper into this below.
- The last seven years have been a pretty steep downswing for energy in songs. We seemed to peak most recently around 2010.
- Valence (again: happiness, kinda) is really interesting. Basically, the median track has gotten less happy each year since since 1962. We're currently at a median valence value of ~0.50; compare that to the 1960's and 1970s, where median valence for a chart period often jumped above 0.8.

Let's zoom in on danceability: 

<sup>[note: I'm using [MLPD3](http://mpld3.github.io/) for my some graphs - so you can zoom and drag them as you want. Check for controls in the lower left corner of a figure]<sup>

{% include med_dance.html %}{:class="img-responsive"}

















