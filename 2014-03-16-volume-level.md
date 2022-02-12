---
title: "The volume of my level"
date: "2014-03-16"
categories: 
  - "audio"
  - "culture"
  - "dossier"
  - "pinned"
tags: 
  - "english"
---

Let's say you bought a rather good microphone, plugged it into your DAW (GarageBand, Logic, ProTools, Live, whatever) either directly or through some sort of preamp or mixer, and recorded what you consider a good podcast you would like to share with the world.

Excellent idea.

But questions arise...

You've read a few technical blogs and other advices about volume and loudness, but you don't know if your recorded voice is loud enough, has the correct 'loudness', and you have no idea how to judge that to begin with.

And those graphs and formulas... oh my gosh, _what the heck_, who are these crazy people?!

> Heck is a place for people who believe in Gosh.

Don't panic.

There's a reason why working with sound is a craft and why it's often called engineering: it's freaking complex! But I'll spare you the equations: I don't like them so much either...

My goal here is to give you the essential tools to be able to _judge_ and _understand_ why your voice sounds loud or not when recorded.

In a perfect world, I would be able to explain this with a few sentences while casually drinking a coffee.

But... yeah, so I first have to explain a few concepts and ideas, name a bunch of stuff and give you a scale of things before I can even begin to answer the question.

But I do answer the question. :)

Although I urge you to remember that there's no magic rule about 'How loud should it be', and the numbers I give you are examples; the real key to the treasure chest is _the ability to understand the context and adapt to it_.

Fasten your seatbelts, here we go.

![mixing deck](https://aya.io/blog/images/console.jpg)

# BIG WORDS

Volume is the amount of pressure in our ears caused by waves of energy transmitted by the environment (we call these waves 'sound').

Volume is a location in a range: between very low (silence) and very high (unbearable).

There's a unit to measure sound volume, the decibel: 'dB' or 'db'.

But this unit is very confusing...

For many reasons:

- it comes with a big family (dbV, dbA, dbFS, dbSPL, dbRMS, etc)
    
- the scales are relative
    
- it's exponential and logarithmic (but we won't talk about that)
    
- it's used to measure different things
    

I will try and keep things simple, and focus only on the parts that are relevant to our question.

_This is not a tutorial about pro audio engineering, but I have to make some sort of introduction nonetheless..._

![](https://aya.io/blog/images/ear.jpg)

# DUDE, WHAT ARE WE TALKING ABOUT?

## VOLUME!

"It's too loud, it hurts, pull it down!"

That's when the pressure in your ears is too strong.

We're talking about Sound Pressure Level (SPL).

"One minute I can't hear a thing, and then it's too loud!"

That's when the movie, or the music album, has a wide _dynamic range_.

It means that the tiny sounds like footsteps are very low (like 40db), and the big explosions are very high (like 110db) on the SPL volume scale.

I just used absolute values in decibels to talk about volume.

I did it in dbSPL, because I was measuring real world sound pressure.

dbSPL scale: 'normal' sounds are at 50db on average.

A conversation between two adults is often at 70db. We love to listen to music at 85db and dance to it at 100db.

Most people start feeling severe discomfort at 110db. At a reasonable distance a jet taking off is emitting a sound pressure of 120db. At 130db the pain begins to be unbearable, and the hearing losses are irremediable. At 140db and higher it's nausea and dizzyness. Then all your organs begin to fail under the pressure. Wow!

Indeed, wow, because we're talking about pressure, a _physical_ phenomenon!

And your ear is just a membrane (with tons of complex engineering behind it) that resonates under the variations of this pressure.

As does the membrane of a microphone ('the diaphragm'), which transforms this real world phenomenon into a quantifiable signal.

![](https://aya.io/blog/images/oldmikes.jpg)

## LEVEL!

This leads us to the second most important topic... the signal LEVEL.

Which is not the same as the signal VOLUME, even if it's not wrong to use one word for the other.

> A signal level is an amount of volume within the dynamic range of a medium.

In English: with the knob on your iPod you change the _volume_ emitted by the device.

But at the same playing volume, all along the song, the level changes between low and high.

The recorded song has itself a dynamic range of, say, 90db.

That's what the sound engineer worked with: a range between silent (0db) and the maximum loudness permitted by the medium (90db).

Contrary to these dbSPL, that have no boundary on the upper-side, the way to measure the sound level in the digital realm _starts from an upper-side boundary_ that is called 0dbFS (FS means Full Scale), 'the ceiling', the maximum level available.

It reaches down to absence of signal, which means silence, at a negative value that is the end of the range of the medium.

Let's now translate this in English again: in the digital world (if you work in 16bits resolution, but let's assume it's the case), you will have roughly 90db of range to work with.

That means you can start from silence at -90dbFS and work all your way up to maximum mayhem at 0dbFS.

But at which _volume_ exactly will be this mayhem? The volume of the knob on your iPod.

And that leads us to...

# COMPRESSION

_Notice for the distracted reader: this has nothing to do with the compression of MP3s or the compression of ZIPs. :p_

Now that you envision that in the digital you work with negative values (dbFS), you need to know a little bit about dbRMS (root mean square):

- The measure of the amount of average volume that is perceived independently of the _peak levels_.

Wow, that's another beast. Let's try again. But before, a thought for the late Hal Douglas...

\[embed\]https://www.youtube.com/embed/fVDzuT0fXro\[/embed\]

## PEAK & RMS

### PEAK LEVEL

When you clap your hands, the 'clap!' sound has a peak of intensity, its higher point.

Let's say it peaks at -20dbFS in your gizmo recorder.

It means that it peaks at 20db from the maximum possible that your gizmo can record.

And you don't have to care about the amount of SPL decibels it's at if it's not your job. We're now in the digital world.

### RMS LEVEL

A sound that evolves in the long term, let's say the sound of your voice when you talk, is made of a lot of little peaks around an average value. (A word would be stronger than an other, etc, and they all have different peaks, more or less close one from another.)

Guess what? That average value is expressed in dbRMS.

On a given amount of time, you take the average of the peaks (the maximums) and the average of the lows (the whispers) and you make an average that represents the _strength_ of your signal _level_ over time, independently of its numerous peaks. This is "the average of overall amplitude".

And now, _le plat du jour:_

> That's the volume we feel: the level within in a dynamic range on average over time.

A detail: dbRMS are noted in two ways, absolute and relative, but they keep the same value in each case.

- absolute: "My mix has 14dbRMS"
    
- relative: "My mix is at -14dbRMS"
    

The first one says that your mix has a headroom of 14db on average, the second one says you are at -14dbFS on average, and it's exactly the same.

### EXAMPLES

Ok, take the Hollywood movie for example.

Lots of explosions at 0dbFS (strong peaks) and lots of music at -14dbFS with very few calm moments at -30dbFS. Oh, and some dialogue at -12dbFS, but not much. Sometimes they yell and groan at -9dbFS, though. All sounds loud... and it's on purpose. Very low dynamic range. High level. Maybe 14dbRMS.

Now take a classical music recording.

Typically, there would be a lot of calm moments between -60dbFS and -25dbFS, and a few strong peaks at -9dbFS when the orchestra gets crazy. You will find a very high dynamic range for this record, because, well, you got the point now, contrary to the movie there will be a wide range between the two extreme possible values. Low level. Maybe 30dbRMS.

Film dialogue (not Hollywood): voices are often between 18dbRMS and 24dbRMS.

Metal bands, hip-hop, EDM... Sometimes they go so loud they're at the same average level than extreme radio ads: 6dbRMS. That's freaking super loud.

### ONE MORE THING...

I said I wasn't going to talk about the exponential and logarithmic nature of the decibel scale. I lied. :)

Ok, no, don't panic, just a few simple assertions about it, to give you a glimpse about the topic:

- there's much more _perceived_ difference between 90db and 93db than between 40db and 43db
    
- splitting a signal in half means losing 3db of power: the half of 12db is 9db
    
- doubling a signal means gaining 3db of power: the double of 10db is 13db
    

That's over-simplified, but I had to at least mention it...

## COMPRESSION, I SAID!

"What? I didn't hear you over the music playing! The RMS level of this album is way too high!" -click-

Yeah, rock albums, ads on tv, radio shows, they all have something in common: they have a very high RMS level ("high" because high on the dbFS scale).

_They sound very loud, but they have the same maximum peak as your podcast, which doesn't sound loud at all...?!_

That's because they're [compressed](http://music.tutsplus.com/articles/encyclopedia-of-home-recording-compression--audio-12409). Sometimes a lot.

> Compression? Taking the peaks and pulling down their level while taking the lows and making them louder.

That means that your record, atfer compression, has now a lower peak value on average.

If the peaks were at -20dbFS, maybe they're at -30dbFS now.

"But it sounds less loud!?"

Of course: your ears sums up the amount of times the peaks appear in order to make an estimation of the volume it perceives, so now that we tamed the peaks, it feels -and is- less loud, even if your average voice is at the same place.

But here's the magic: now we can _make-up the gain_, meaning, we can compensate the loss of peak level by pulling up the general level!

And we can do this because we gained 'headroom'.

That means: before, when the peaks were at -20dbFS, we had 20db of headroom until the maximum possible, and now we have 30db of headroom because we squashed the peaks by 10db.

Then we put up the general level by 10db.

And suddenly it sounds way louder than before, because not only we put back the peaks where they were at the beginning, at -20dbFS, but we took the low levels with us and pulled them up by the same amount!

The lows that were at -50dbFS? They're now at -40dbFS. I'm simplifying, but you get it.

Now the sound has more _strength_.

The "belly" of the sound is higher.

What? Loudness-wise, most sounds have hollow feet, big low belly, normal high rib cage and light head. Compression makes them keep the hollow feet and light head but takes the low belly and transforms it into rib cage muscles. Sorry for the poor image, but I often find that it works when I explain this kind of things...

In a nutshell: **compression + gain = louder with same max peaks.**

![](https://aya.io/blog/images/vumeter.jpg)

# TO SUM IT UP

## TECH

Amount of sound pressure: dbSPL, positive values from minimum (0db) to infinite (but our ears can't survive over a certain volume, neither our bodies).

Amount of sound in digital: dbFS, negative values from the top ceiling (0dbFS) to the floor, be it silence or a certain resident noise (at -140dbFS for wav 24bits, -90dbFS for 16bits CD, -60dbFS for FM radio, etc).

Amount of sound you feel over time: dbRMS, the amount is in absolute values but you place it on the dbFS scale.

_ProTip: power = energy / time._

## NON TECH

We measure the sound as the amount of difference between the minimum and the maximum pressure a system can emit, enclose or endure.

There's various scales but it's always the same thing: peaks or averages, positives or negatives, the values represent a state within a range.

But let's forget all this now and have some fun!

![](https://aya.io/blog/images/loud.jpg)

# SOLUTIONS

Ah, at last! :p

Well, I couldn't see how I could give you any advice without explaining first the words and concepts I'm gonna use for that...

## AT WHAT VOLUME SHOULD I LISTEN TO THINGS?

When listening to music that's not overly compressed, the average in the population is to listen around **85dbSPL**.

That's normal music played at what is considered a normal volume in a normal environment.

A rock concert in a club is at 110dbSPL. Super loud.

Smooth jazz in the backround at the cocktail party is not so loud, sometimes it's even lost behind the voices: let's say 70dbSPL.

For dialogue, radio or podcast monologue: your iPod or hi-fi should be at roughly 80dbSPL. Well, that's what people like on average anyway.

I have three reference levels to test my mixes in the studio: 72db, 85db and 95db, all at a distance of 1.5 meters. My amplification system gives me accurate numbers: that's not always the case with some brands...

Oh, and be aware that listening and mixing with headphones is an entirely different thing. The proximity effect induced by the headphones amplifies our perception of the low levels and distorts the perception of the high levels. With headphones, your mental representation of the sound is biased and you should always judge the final result on regular monitors instead. And please always listen at a moderate volume with headphones, and make regular pauses to rest your ears.

![](https://aya.io/blog/images/decibels.png)

## AT WHAT LEVEL SHOULD I PRINT MY VOICE?

For a podcast:

It depends if your voice has a lot of compression or not.

Ok... Does your podcast have a lot of peaks?

If so, when your listener will encounter a big peak, he will pull down the volume a little, fearing for the next peak.

So the overall perceived volume will be lower, because the average level of your voice is way lower than the peaks, and your listener just pulled them down!

If the peaks were at 85dbSPL: now they're at 75dbSPL.

And when your normal voice was at 70dbSPL, now it's at 60dbSPL and it's hard to get what you say.

So you compress your voice then make-up the level...

No more peaks. Yes, you have a smaller dynamic range, but your sound is so "full", so "strong", has so much "presence" that you immediately put it in your iTunes feed.

Oh, that big radio voice. The listener is gonna listen to me again, even if he pulled down the knob!

But now it's too loud, and it induces ear fatigue...

Because for your ears, no peaks is the same thing as an infinite succession of peaks! Well, it's more like your ear doesn't have time to rest anymore between the peaks, actually, but... potato/potato.

Big compression is bad because the recording sounds always loud.

There isn't any nuance, all is racing towards the ceiling.

Bad, bad, bad. Ok, Jay-Z and Metallica?

## I SAID, AT WHAT LEVEL... MY VOICE... ???!

> **Stay around -14dbRMS, slightly compressed; the peaks shouldn't go beyond -9dbFS nor the lows beneath -30dbFS.**

_That's for voice, for one person talking, typically a podcast recorded with a rather good mic._

But it's just a rule of thumb, because... compression changes everything: a voice with a reduced range (heavily compressed) will be better sitting at -20dbRMS (because it sounds louder on average) for example.

## WHY -9dbFS MAX PEAK AND NOT 0dbFS?

I mean, people can pull down their volume button if they want, so why not put the maximum peak level at the maximum possible value?

Oh but you can. I do it all the time! When I give a MP3 to the client for validation, etc.

But not when recording or for diffusion. _There's millions of reasons why_, but I will just say a word about three of them.

### RECORD

When you record, you want to keep some headroom between your expected peaks and the accidental but probable louder peaks.

Because in digital if you go over the ceiling, things sound terrible, you have to make place, just in case.

### MIX

When you mix, it's better to align all your tracks relatively low, so that you keep room for peaks and the general summation.

You want to have headroom to add up later and not feel limited.

### DIFFUSION

Once the mix is done and the general level brought up to a reasonable peak value, and the RMS values are not too reduced but the dynamic range isn't too wide either, you have something that you can give to the world.

But if your voice sounds as loud as a metal band, there's something wrong... so you leave headroom to keep some sort of cohesion with what's aired before and what's aired after you. Tough topic, people are a bit voodoo about this.

## EXAMPLE

In '[Back to work](http://5by5.tv/b2w)', Dan Benjamin likes to have a heavily compressed voice, he sounds rather loud but the mix is ok so it doesn't induce much fatigue.

On the other hand, Merlin Mann is often on Skype with no dynamic compression but a reduced quality and has a habit of suddenly yelling something from time to time.

He is less loud than Dan on average, but often sounds louder because of the higher peaks.

Dan _feels_ louder, Merlin _is_ louder.

Both are good and no one is wrong... except that I'm afraid of Merlin's screams and Dan sounds like he's talking directly into my brain... :p

This example is not perfect: in some episodes, Dan makes up the gain a lot and _is_ very loud, so... it was just an example. :p

![](https://aya.io/blog/images/ua.jpg)

# COMPARE

_This is very important._

Once your podcast is finished and bounced, but not before, listen to 30 seconds of another podcast, maybe one with an especially good sound. Try and catch the differences with yours in your head while listening. Then immediately listen to 30 seconds of yours; then _silence_.

Think.

Replay the two in your mind.

Do you think you're too loud on average? Apply less/no compression or pull down the level. Or both.

Do you think you're loud sometimes but too low on average? Apply more compression then make-up the gain.

Do you think you're not loud enough at all? Apply gain first, then compression only if the peaks are too high.

Do you think you're ok on average but not loud enough sometimes? Apply a little compression and don't make up the gain too much.

# TIPS

Apply gain to make a track louder, not compression. Only apply compression if you need it. Don't normalize.

If you compress, know why and act accordingly. Are you just taming the stronger peaks? Or are you also making the average level louder? Etc.

Anyway, try using the slower 'attack' and even way slower 'release' values possible when using compression to keep the sound natural. Don't use radical values in other parameters either like ratio or threshold. Work by layers of small modifications that add up.

Never go in the red (over 0dbFS). NE-VER.

Oh, and is your mix/voice muddy or dull or boxy or noisy or else?... wait, these are entirely different topics, we were focusing _solely_ on volume and level here. :)

# CONCLUSION

Don't try and sound as loud and as clear as a recording studio or radio station, because guess what, you can't.

And more: you don't care.

What you care about:

Try and walk this middle path with a lot of curves and hills but where you can still see the horizon at any moment.

Too much average level: get out of my ear drums, you perv.

Too few average level: lower parts are not understandable. Mumble grumble.

Peaks too high too often: I will stop listening to you immediately, you can't jump in my ears and pierce them with white hot metal like that.

But no peaks = no life. If the mix is flat and all is at the same level, there's no fun and my ears will get bored, then I'll get bored.

People will listen to your voice at very different volumes, in very different locations and contexts, but they always will understand what you say if you achieved a balance between all the level constraints we've talked about.

Anyway... trust your ears, enjoy your life and ignore the haters. :)
