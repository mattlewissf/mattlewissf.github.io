I've been noodling around with a dataset I put together that tracks audio features of Billboard Hot 100 songs over the last 55 years. And one thing that kept drawing my eye was a big spike in values - specifically in the Spotify-defined features of danceability, valence, and energy - in the late 1970s, which a crash in the early 1980s. 

{% include disco_first.html %}


What could cause such a crash in the feel-goodiness of music at the time? What might have stopped the boogie? 

Why, the death of disco, of course! 

### So apparently disco is dead

I wasn't lucky enough to be alive during the disco era, but I feel like the general idea of disco was that it didn't exist, then people liked it, then they liked it too much, until there was a backlash against it and people couldn't even be around it anymore. I have a similar relationship with gummi bears. 

A crude understanding of the disco lifecycle: 

![](http://i.imgur.com/kpttSm8.png){:class="img-responsive"}


But when was the point where everyone collectively decided that disco was over? It turns out there was a specific time of death: Disco apparently died on July 19th, 1979, at Kominsky Park in Chicago, which is a weird place for a music genre to die. 

That was the night of a promotional event, being held after the Chicago White Sox game, called "Disco Demolition Night." The idea was that patrons would bring their disco records, and then they would be exploded on the field. The event, somehow!, devolved into pandemonium. 

![A reasonable public response](http://media.chicagomag.com//images/cache/cache_4/cache_3/cache_a/C201607-C-The-Night-Disco-Died-main-87a4ba34.jpeg?ver=1482341622&aspectratio=2){:class="img-responsive"}


But as the event made national news, it took on significance beyond local hooliganism and became 'the night the disco died.' The way that it is told, this was the high water mark for disco, which would singificantly lose chart prowess in the months to come, and cease to be a major factor in American pop music within a few years. 


### Something else 

We know that there was a big upswing and downswing in valence and danceability numbers that coincide with the timeline of the rise and fall of disco. But did disco songs themselves actually disappear from the charts? We need some genre data to help us see if disco was actually responsible for what we are seeing. 

Getting genre data, however, is really difficult. While Billboard has different charts based on something close to genre, they don't make a stab at categorizing tracks that come into the Hot 100. Everything is just Hot. And while Spotify has reams of information for each track (if you really want to go down the rabbit hole, check out their audio anaylsis endpoint), they don't have track level genre tagging. What you can do is get a track ID, do a separate API call to get all of the track information, and then parse that to get an album ID. Then, you can use get_albums to get genre information about the album. Exciting!  Except often, there's nothing there. And when there is, there are a number of conflicting tags ('rock', 'pop', etc).

So I decided to do it manually. Using just a spreadsheet and my ears, I took just the top 20 songs from the Hot 100 chart during this period and classified them as being disco or not. Since I'm already operating under the assumption that top hits get heard a lot more than bottom charters, I decided to only try to categorize the top 20 songs from each chart period. According to my weighting rules, that's pretty much ~50% of all listens for a weekly period anyway. 

Then, I charted it against the audio feature data that we had for the same period: 

![](http://i.imgur.com/8K0EfgJ.png){:class="img-responsive"}

What we see suggests that disco chart dominance maxed out just before the night disco died, and that, while disco didn't just die overnight, the number of disco hits in the charts did significantly decrease afterwards. We also seem to see coordinated movement between our danceability and valence numbers and the number of disco hits in the top 20 as well. 



### Is this the biggest chart change we can observe? 

This brings up an interesting question: how can we measure the amount that pop music changes from period to period? And what were the periods where pop music underwent the most change? 

One way we could measure this is to look for a central attribute for the different audio features we are tracking, and see how this moves over time. 







What makes a song disco? 








<iframe src="https://embed.spotify.com/?uri=spotify%3Auser%3A1222829066%3Aplaylist%3A5tKF7pBywYzFWuKvp6sThz" width="300" height="360" frameborder="0" allowtransparency="true"></iframe>