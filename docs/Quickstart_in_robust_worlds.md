# Quick start in robust worlds building in AI Dungeon

#### Disclaimer
This doc is just a compilation of the info already available on the subject atm of writing. See the [Credits](#credits-and-links) section for details.

I ([Lex Darlog](https://github.com/Lex-DRL)) am not a native english speaker, so I'm apologizing for my grammar upfront.

I did my best to make this guide as short and yet as informative as possible, but I did it alongside with learning the subject myself. So there might be some mistakes, missing specifics or too uch of flood here and there. Although, I believe it points you to the right direction in general.

Fell free to commit/pull request any corrections you see fit.

## Introduction
If you've got here, I believe you've already played [AI Dungeon (AID)](https://play.aidungeon.io/) and tried to describe your own setting with [World Info (WI)](https://wiki.aidiscord.cc/wiki/World_Info). So you've noticed a few limitations of the AI. Specifically, you must've been frustrated by how much the AI seems to forget everything, even the most recent info. I mean, it's right there, 3 inputs above, how could you possibly forget it already! You must've faced a similar situation more then once.

Even though AI dungeon might seem a neural-network (NN) auto-magical "next generation of software", it's still just a software. So it has it's limitations. One of the core ones is memory limit. You can read the specifics [here](/AID%20WI%20Research%20Sheet.md#remember-worldinfo-authorsnotes-worlds-and-how-the-game-handles-them), but in short, if you think of AI as of a real person, it would be a really, really dumb one. Set aside, that comparing AI NNs with a real brain is incorrect in general, the current state of technology is only capable of building NNs that can barely compete with an intellect of really primitive lifeforms, like bees or worms, and it can do it only on a very powerful computers. We're nowhere near human level of intellect. Well, maybe, if we combine **ALL** of the existing computing power on Earth (including every smart TV or smart watch) to a massive cloud server, it can be comparable to a single human brain, but that's it. And that brain won't be an Einstein one.

So AI Dungeon's NN models (Griffin and Dragon) are (and inevitably will be in any foreseeable future) incapable of truly mimicking a living narrator / game master.

With that important thing said, I've got good news for you. You still can drastically improve the AI output by simply building the WI "the right way". According to tests/evidences, provided by the AID community, a "properly" made WI does make night and day difference, producing more consistent output, making the AI forget less and generating more relevant output in general. How do you accomplish this? Well, you need to stop thinking about the AI as of "really dumb person" and start thinking of it as of what it actually is: a really smart software.

## But I'm not a programmer!
The good news is, it's great if you are, but you don't need to be. As long as you understand how the AI works (even in vague terms), you can significantly enhance the output, even staying completely away from programmatic style of the WI.

So first things first, there are two things the AI struggle with:

1. Vague/unclear WI entries;
2. Too long, non-finformative WI entries.




## Credits and links
