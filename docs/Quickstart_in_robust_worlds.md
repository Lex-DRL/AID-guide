# Quick start in robust worlds building in AI Dungeon

#### Disclaimer
> This doc is just a compilation of the info already available on the subject atm of writing. See the [Credits](#credits-and-links) section for details.
>
> I am not a native english speaker, so I'm apologizing for my grammar upfront.
>
> I did my best to make this guide as short and yet as informative as possible, but I did it alongside with learning the subject myself. So there might be some mistakes, missing specifics or too much of flood here and there. Although, I believe it points you to the right direction in general.
>
> Fell free to commit/pull request any corrections you see fit.
>
> — [Lex (DRL) Darlog](https://github.com/Lex-DRL)

- [Introduction](#introduction)
  * [But I'm not a programmer!](#but-im-not-a-programmer)
  * [How AI remembers your WI](#how-ai-remembers-your-wi)
- [First steps: optimising just a plain english](#first-steps-optimising-just-a-plain-english)

## Introduction
If you've got here, I believe you've already played [AI Dungeon (AID)](https://play.aidungeon.io/) and tried to describe your own setting with [World Info (WI)](https://wiki.aidiscord.cc/wiki/World_Info). So you've noticed a few limitations of the AI. Specifically, you must've been frustrated by how much the AI seems to forget everything, even the most recent info. I mean, it's right there, 3 inputs above, how could you possibly forget it already! You must've faced a similar situation more than once.

<details>
  <summary>Why AID's NNs suck and what we can do about it</summary>
  
> Even though AI dungeon might seem a neural-network (NN) auto-magical "next generation of software", it's still just a software. So it has it's limitations. One of the core ones is memory limit. We'll discuss the specifics further, but in short, if you think of AI as of a real person, it would be a really, really dumb one. Set aside, that comparing AI NNs with a real brain is incorrect in general, the current state of technology is only capable of building NNs that can barely compete with an intellect of really primitive lifeforms, like bees or worms, and it can do it only on a very powerful computers. We're nowhere near human level of intellect yet. Well, maybe, if we combine **ALL** of the existing computing power on Earth (including every smart TV or smart watch) to a massive cloud server, it can be comparable to a single human brain, but that's it. And that brain won't be an Einstein one.
>
> So AI Dungeon's NN models (Griffin and Dragon) are (and inevitably will be in any foreseeable future) incapable of truly mimicking a living narrator / game master, that can understand any of your requests and always produce something meaningful.
>
> With that important thing said, I've got good news for you. You still can drastically improve the AI output by simply building your WI "the right way". According to tests/evidences, provided by the AID community, a "properly" made WI does make night and day difference, producing more consistent output, making the AI forget less and generating more relevant output in general. How do you accomplish this?
</details>

Well, you need to stop thinking about the AI as of "really dumb person" and start thinking of it as of what it actually is: a really smart software.


### But I'm not a programmer!
The good news is, it's great if you are, but you don't need to be. As long as you understand how the AI works (even in vague terms), you can significantly enhance the output, even staying completely away from "programming" the WI.

So first things first, there are two aspects the AI struggle with:

1. Vague/unclear WI entries;
2. Too long, non-informative WI entries.

The first might be not as obvious as you think. For instance, the canonical `has`/`is` difference mentioned in official AID FAQ: you can say that a `character has green eyes` or that the `character's eyes are green`. It seems the same to you, but for the AI, the former would be much harder to understand (the connection is weaker) than the latter. More on that below, here it's just as an example.

And let's talk about the the second problem, being informative...

### How AI remembers your WI

To correctly understand what statement is informative **for the AI**, we need to discuss how the AI represents your input in general. Again, I try to stay away from specifics for programmers, but we need to grasp at least the concept.

AI doesn't remember **words** you input. Neither it stores some IDs of those words. Nor it understands the meaning of those. Instead, as the very first step, AI parses (disassembles) your text into so-called **tokens**. Tokens are in essence just a common combinations of characters. So, for example, the word `appearance` is represented by 3 consequent tokens: `AP`, `PE`, `AR`, `ANCE`. Those tokens are the actual information the AI works with.

Here's an example of few common words [tested for tokens by the community](/AID%20WI%20Research%20Sheet.md#tokenization---understanding-limitations-and-special-characters):
![CATEGORY tokens](/imgs/cat-tokens.png "CATEGORY tokens")

So, back to the track. You can make an entry which have many **characters** but not so much **tokens**, and vice versa. Or you can make a descriptive entry in english which, when represented by tokens, doesn't make much sense for the AI. We want to use at least tokens as possible while keeping them as informative as possible.

Another important thing about AI memory is it's size. With each input you give, only about 2.8k charcters are fed to the NN. It's not so much even on it's own, but it's even less considering that this limit is shared between your `Remember` section, any relevant WI that AI found for the given input, the input itself and, well, the history of previous text. The specifics on how this memory shared can be found [here](/AID%20WI%20Research%20Sheet.md#remember-worldinfo-authorsnotes-worlds-and-how-the-game-handles-them). But for now — let's mark two things:
* The **overall** limit for `Remember` + `WI` + `Author's notes` (premium feature, but can be used on free account with scripts) + your `Input` + most recent part of story = 2772 chars. 
* We want to use those chars as effectively as possible, trying not to waste any of them.

## First steps: optimising just a plain english



## Credits and links
