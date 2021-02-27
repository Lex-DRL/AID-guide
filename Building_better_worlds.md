# Building better worlds <sub>*(in AI Dungeon)*</sub>
An introductory guide for game masters / somewhat experienced players who want to enhance `AI Dungeon`'s output and make it generate a more believable story, with a detailed/developed world.

<details>
<summary>Disclaimer</summary>
  
> 1. Everything presented on this page is a result of other people's research. You can call this article a meta-research, a shameless rewrite or a compilation of the already available info. I call it an introductory  guide. See the [Credits](#credits-and-links) section.
> 2. I need to apologize for my english upfront. I'm not a native english speaker (hey from Russia, btw 👋🏻🙂).
> 3. I did my best to make this guide as short and yet as structured and informative as possible, but I was making it alongside with learning the subject myself. So there might be some mistakes, missing specifics or too much of them here and there. Although, I believe it points you to the right direction in general.
>
> Feel free to suggest any corrections you see fit.
>
> — [Lex (DRL) Darlog](https://github.com/Lex-DRL)
</details>

<details>
<summary><b>Table of contents</b></summary>

- [Introduction](#introduction)
  * [But I'm not a programmer!](#but-im-not-a-programmer)
  * [How AI remembers your WI](#how-ai-remembers-your-wi)
  * [Testing](#testing)
- [First steps: optimising just a plain english](#first-steps-optimising-just-a-plain-english)
  * [Mention the subject in entry](#mention-the-subject-in-entry)
  * [Use `is` instead of `has`](#use-is-instead-of-has)
  * [Avoid negatives](#avoid-negatives)
  * [Avoid long sentences](#avoid-long-sentences)
  * [Avoid using words with broad meaning](#avoid-using-words-with-broad-meaning)
  * [Use known categories](#use-known-categories)
  * [Don't use emojis and special characters](#dont-use-emojis-and-special-characters)
- [Next step: World Info formats](#next-step-world-info-formats)
  * [A couple of notes relevant for all formats](#a-couple-of-notes-relevant-for-all-formats)
  * [Author's note](#authors-note)
  * [The best format atm](#the-best-format-atm)
  * [Format examples](#format-examples)
 - [Last step: Scripts](#last-step-scripts)
</details>

#### Who's the guide for
By no means this guide is a comprehensive research on the subject of Machine-Learning (ML) techniques in AID. If you're one of those data scientists / ML enthusiasts, skip it entirely and go directly to [AID WI Research Sheet](/AID%20WI%20Research%20Sheet.md).

This guide is for **players**, who just want to make the game's responses look less like the ones of a grandma with alzheimer.

People with different backgrounds might be reading this guide. So it's split into 3 sections.<br />
Currently, the best and also simplest way to build an optimized world info is using scripts (section 3). But to fully utilize this approach, you need to be familiar with techniques in first two sections, anyway. So those are ordered not by what's more recent/effective but by it's complexity, going from simplest to hardest to understand.

Each section is self-sufficient on it's own, so you can stop whenever you feel for it and (maybe) return later for a more advanced stuff.

Also, before you continue, I strongly suggest reading [World Info guide on the community wiki](https://wiki.aidiscord.cc/wiki/World_Info).

#### List of used terms
> The `AI Dungeon` (AID) community uses some special terms and abbreviations. No need to learn them right now, I'll explain them as I introduce them on the way. But if for some reason you skipped it, you can revisit this section.
<details>
<summary>Terms and abbreviations</summary>
  
- AID - AI Dungeon
- A/N - [Author's note](#authors-note), a premium feature.
- ML - machine learning
- NN - neural network
- [token](#how-ai-remembers-your-wi) - a combination of a few characters that the AI splits all your input into. E.g., tokens for `APPEARANCE` are: `AP`, `PE`, `AR`, `ANCE`.
- WI - World Info
</details>

## Introduction
If you've got here, I believe you've already played [AI Dungeon (AID)](https://play.aidungeon.io/) and tried to describe your own setting with [World Info (WI)](https://wiki.aidiscord.cc/wiki/World_Info). So you've noticed a few limitations of the AI. Specifically, you must've been frustrated by how much the AI seems to forget everything, even the most recent info. I mean, it's right there, literally at the same screen, how could it possibly forget it already! You must've faced a similar situation more than once.

<details>
<summary>Why AID's NNs suck and what we can do about it</summary>
  
> Even though AI dungeon might seem a neural-network (NN) auto-magical "next generation of software", it's still just a software. So it has it's limitations. One of the core ones is memory limit. We'll discuss the specifics further, but in short, if you think of AI as of a real person, it would be a really, really dumb one. Set aside, that comparing AI NNs with a real brain is incorrect in general, the current state of technology is only capable of building NNs that can barely compete with an intellect of really primitive lifeforms, like bees or worms, and it can do it only on a very powerful computers. We're nowhere near human level of intellect yet. Well, maybe, if we combine **ALL** of the existing computing power on Earth *(including every smart TV or smart watch)* to a massive cloud server, it can be comparable to a single human brain, but that's it. And that brain won't be an Einstein one.
>
> So AI Dungeon's NN models (Griffin and Dragon) are (and inevitably will be in any foreseeable future) incapable of truly mimicking a living narrator / game master, that can understand any of your requests and always produce something meaningful.
>
> With that important thing said, I've got good news for you. You still can drastically improve the AI output by simply building your WI "the right way". According to tests/evidences, provided by the AID community, a "properly" made WI does make night and day difference, making the AI forget less, producing more consistent and overall more relevant output in general.
>
> How do you accomplish this?
</details>

Well, you need to stop treating the AI as a "really dumb person" and start treating it as what it actually is: a really smart software.


### But I'm not a programmer!
The good news is, it's great if you are, but you don't need to be. As long as you understand how the AI works (even in vague terms), you can significantly enhance the output, even staying completely away from "programming" the WI.

So first things first, there are two general problems the AI struggle with:

1. Vague/unclear WI entries;
2. Too long, non-informative WI entries.

The first might be not as obvious as you think. For instance, the well-known `has`/`is` difference: you can say that a `character has green eyes` or that the `character's eyes are green`. It seems the same to you, but for the AI, the former would be much harder to understand (the connection is weaker) than the latter. More on that below, here it's just as an example.

And let's talk about the the second problem, being informative...

### How AI remembers your WI

To correctly understand what statement is informative **for the AI** (not for human), we need to discuss how it represents your input in general. Again, I try to stay away from specifics for programmers, but we need to grasp at least the concept.

AI doesn't process the **words** you input. Neither it stores some IDs of these words. Nor it understands the meaning of them. Instead, as the very first step, AI parses (disassembles) your text into so-called **tokens**. Tokens are in essence just a common combinations of characters. So, for example, the word `APPEARANCE` is represented by 4 consequent tokens: `AP`, `PE`, `AR`, `ANCE`. Those tokens *(and their combinations, making words for you)* are the actual information the AI works with.

Here's an example of a few common words [tested for tokens by the community](/AID%20WI%20Research%20Sheet.md#tokenization---understanding-limitations-and-special-characters):
<details>
<summary>Screenshot</summary>
  
![CATEGORY tokens](/imgs/cat-tokens.png "CATEGORY tokens")
</details>

So, back to the track. You can make an entry which have many **characters** but not so much **tokens**, and vice versa. Or you can make a descriptive entry in english, which, when represented with tokens, doesn't make much sense for the AI. We want to use at least tokens as possible while keeping them as informative as possible.

Another important thing about AI memory is it's size. With each input you give, only about 2.8k characters are fed to the NN. It might seem a lot, but if you consider that this limit is shared between **EVERYTHING** you send to the NN, that's not so much. That "everything" includes your `Remember` section, any relevant WI that AI found for the given input, the input itself and, well, some part of history to work with. The specifics on how exactly this memory is shared between different parts can be found [here](/AID%20WI%20Research%20Sheet.md#remember-worldinfo-authorsnotes-worlds-and-how-the-game-handles-them). But for now — let's mark three points:
* The **overall** limit for `Remember` + `WI` + `Author's notes` (premium feature, but [can be used on free account with scripts](#authors-note)) + your `Input` + most recent part of story = 2772 chars. 
* We want to use those chars as effectively as possible, trying not to waste any of them...
* ... but at the same time feeding as much **relevant** data as we can at each input.

### Testing
Regardless of which approach you choose (stick to the plain english or go all the way to scripts), you need to test how changes in your descriptions affect the output.<br />
Both fortunately and unfortunately, the AI's output is non-deterministic, and the models keep changing with each backend update.
So the community haven't agreed on a single standardized set of tests to check the quality of your world descriptions **objectively**.

However, there are a few approaches that the community embraced as somewhat-standard ones. The idea is, you need to put your description and immediately after it enforce the AI to spit out how it understood you.

The first way to do so is putting a description with immediate request for the AI to "interpret" it.

`Mr.Accountant` (a discord community member) suggested doing it in a simple way:
<details>
<summary>Mr.Accountant approach</summary>

> ```
> <blablabla>
> I interpret this as
> ```
> Here, replace `<blablabla>` (including `<>`) with your description. Note that `I interpret this as` is also a part of the same input, at a new line. It's an enforcement for the AI to continue the sentence.
</details>

Another discord user, `Onyx`, suggested different way of doing the same thing:
<details>
<summary>Onyx approach</summary>

> First, define the AID character:<br />
> `You are a researcher sitting at the terminal of an advanced supercomputer talking to an AI named AID. You are testing the AI's reasoning abilities. You sit down at the console and begin typing.`
>
> Then, put the testing text:<br />
> ```
> You: AID, please interpret the meaning of the following:
> <blablabla>
> 
> AID: I interpret this as
> ```
> 
> You should also have the AID character defined in your `Remember`. Like the following (don't worry about this cypher for now, just copy-paste it; it's explained in [formats section](#next-step-world-info-formats)):<br /> 
> `AID:[Advanced AI. APPE:hologram;MENT:professional∕confident∕practical∕sophisticated∕mature;SUMM<AID>:linguistic AI∕genius∕fast processing&reply∕omniscient∕knows everything∕accurate.]`
</details>

As you can see, even here there's no universal way to do it. However, I find Mr.Accountant's approach much more appealing for it's simplicity.

The second way of testing is with `Detailed Description`:<br />
You add an entry with your character description to the WI, and then trigger it with:
```
Detailed Description of <Character Name>:
```

Also, here's `Mr.Accountant`'s comment on the subject:
> I have 3 levels of substantive testing.<br/>
> First is a Surface Level test, this is the `Detailed Description:` (or `Interpret this`). This checks to see if the AI can even understand what I am talking about.<br />
> Next is a Contextual Test. Usually around 550chars of prompting for dragon. Here I test how the entry works with some context. Is the AI understanding what the character is supposed act like?<br />
> Finally there is a third level of testing. The 2k Prompt, it holds 2000 chars in initial prompt, a good chunk of memory. And should test MULTIPLE world entries at once.
> This is to simulate going through a mid-story.

A few things to keep in mind: depending on your `Randomness` setting, you may have different results. What's already present in your WI / Remember / history - also affect the output. So for best results, you should set up a clean scenario.

Now, with all that prelude out of the way, we can finally start tweaking WI.

## First steps: optimising just a plain english
Here's a (somewhat) full list of tips I've found so far. These tips don't require "hacking" the WI in any way. As with all other tips, I intend to extend this list with other hints as I find them.<br />
From now on, we're talking about text for **entries**, not for keys. Also, the examples I'm gonna show are in Mass Effect setting *(since that's the scenario I want to make and the one I'm learning the subject for)*.

#### Mention the subject in entry
When you mention a thing in `Keys` section, also mention it in the `Entry` itself.
<details>
<summary>Example</summary>
  
❌ Bad:
> `Keys`: citadel
>
> `Entry`: A colossal deep-space station that serves as the capital...

✔ Good:                                                                                                                                          
> `Keys`: citadel
>
> `Entry`: ***Citadel*** is a colossal deep-space station that serves as the capital...
</details>

#### Use `is` instead of `has`
As [stated above](#but-im-not-a-programmer), `has` is much weaker than `is`. To a degree that the AI [can loose the connection entirely](https://wiki.aidiscord.cc/wiki/World_Info#Entries). Ideally, you should move to a special WI formatting altogether (more on that later), but if you don't, at least use `is`.
<details>
<summary>Example</summary>
  
❌ Bad:
> `Entry`: Shepard has a deep low voice...

✔ Good:                                                                                                                                          
> `Entry`: Shepard's voice is deep and low...
</details>

#### Avoid negatives
I'l just put [birb's wording](/AID%20WI%20Research%20Sheet.md#personality-keywords) here in a direct quote:
> AID has been known to be notoriously bad at negatives. For example the community has known for a long time that `White hates apples` is a better alternative to `White dislikes apples` as the AI doesn't seem to respect the intent of the latter statement at all.
>
> Words starting with dis- or un- rarely get respected by the AI due to tokens and how bad it's with negative prefixes. -less is a suffix that works somewhat better, but isn't recommended if you have synonyms known to be more explicit or to have unique tokens.

#### Avoid long sentences
Even though the AID devs explicitly tell that the AI can understand long sentences, it's bad at this. So you should describe your world with the  shortest statements you can. I myself am one of those who love describing stuff with a single nuanced thought expressed with a long self-interconnected sentence instead of a few smaller ones. The last sentence shows that. But for AI, you need to stay as short and clear as possible. 

Roses are red. Violets are blue. Future is Skynet. AI loves you.<br />
That's it.

I know how tempting it is to go into intricacies of how vibrant those violets' blue colors are, reminding you of massive nebulas in endless deep space... But unless you're a really good writer capable of making a true words porn who also happened to be a native english speaker, stay away from this. But don't go too simplistic in your descriptions, because you also need to... 

#### Avoid using words with broad meaning
As a non-native english speaker, I have a small vocabulary myself. But whenever you can, you need to choose the most specific and descriptive words that carry as many meaning as possible, and this should be the same meaning. Ideally, your text should look like hokku, where each word carries a whole ocean of rich associations about the same thing. Remember those ridiculously clickbaity screaming tabloid headlines that yellow journalism likes to use? Like that. Each word there carries a whole image. Check yourself:
```
Titanic Survivors Found Onboard
Vampires Attack US Troops
Alien Bible Found, They Worship Oprah
```

A list of words proven to be descriptive to define a character is at the same [Personality Keywords section](/AID%20WI%20Research%20Sheet.md#personality-keywords) I quoted about negatives.

<details>
<summary>Example</summary>
  
❌ Bad:
> Ironically, `bad` itself 😄
>
> Also, `evil`, `mad`.

✔ Good:
> `cruel`, `sadistic`, `lunatic`.
</details>

#### Use known categories
Even if you won't go any further to specific formatting styles, you can (and should) utilise the keywords proven to give good results.
The list is really long and gets updated so I won't duplicate it here and I'll just give a [link to the table of common categories](/AID%20WI%20Research%20Sheet.md#categories-table).

Some of the most noteable are: `SUMMARY`, `MIND`, `APPEAR`, `WORN`, `DESC`, `LIMIT/LACK`. You can read about them at the link above.
Note that all of them are in `UPPERCASE`. That's not by accident. Generally, it's a matter of preference whether you use `UPPERCASE`, `lowercase` or `ProperCase` (aka `CamelCase`). Again, read about differences [here](/AID%20WI%20Research%20Sheet.md#useful-categories). But if you just want the "recommended" approach for beginners, it's definitely `UPPERCASE`.
<details>
<summary>Example</summary>
  
(assuming you still use a somewhat-like raw prose and not a specific WI format)

> `Entry`:
>
> Shepard:<br>
> SUMMARY: human male, 30y, military, Alliance forces, first human Spectre.<br>
> APPEAR: 189cm tall, 102.5kg, muscular, short military haircut, dark hair_color, brown eyes_color.
</details>

Note #1: the above example shows the use of special phrases like `30y` (no space). They're not just allowed but recommended to use: common phrases are treated as a single token and easy to understand for the AI.

Note #2: the AI has shown that it correctly detects shortened keywords, like `APPE` and `SUMM`. Use those to reduce both chars and tokens count.

Note #3: the underscore (`_`) character [is treated by the AI specially](/AID%20WI%20Research%20Sheet.md#on-certain-characters). It connects adjacent words stronger (harder-better-faster... 😄) than a space. So for some sub-categories it's better to use names like `hair_color` instead of `hair color` or even just `color`. This way the AI understand better that you mean specifically **hair** color: not just some arbitrary color.<br>
Earlier, a dash (`-`) char did the same thing, but currently it's treated more like a mathematical minus, so if you see a recipe using dash to connect words, replace it with underscore instead. 

#### Don't use emojis and special characters
Unicode emojis are supported but they cost 2 tokens. Use with caution, only if you really want to use those or an emoji as actually shorter and carries more semantic value than a regular word.

Non-ASCII unicode characters like `ù` should be avoided in all cases.

Special characters like `<>`, `[]`, `{}` and other symbols used in programming are treated... well, like in programming. The AI is trained on an immense dataset gathered by scraping internet, so it learned the meaning for those chars from where it've seen them the most: in the source code.

This is a good thing, and the WI formattings utilize that. But unless you're using one of those formats or testing your own, you should avoid these chars in general. What all the brackets do is grouping words together. So `<hair color>` does the same thing as above. But different brackets have a different meaning for the AI, so if you're going into this territory, you're better off using an already established format.

And that would be a good place to discuss those.

## Next step: World Info formats
Now we're stepping into somewhat hacky area.

As stated above (and you might already know), modern AI learns from it's experience. So inevitably, there will be some patterns that the AI have seen more and therefore recognizes them better. That's the whole idea of so-called **WI formatting/formats**. You can't program AID directly to build the world you want, but you can format your WI entries in a specific (somewhat program-alike) style, which AI would understand much, much better. So therefore it would generate a mich more meaningful output.

That's what AID community discovered from practice, confirmed with a plenty of tests/evidences and came to the conclusion that it's a much superior way to describe a world than a regular prose. So yes, you can type just a plain natural language into WI entries, and AID will automagically understand it. But you **shouldn't** do it this way. Instead, you should describe your world in a more machine-readable format. Don't worry, you won't cause the AI to generate a machine-like text by doing so, quite the opposite: since it understands the world better, it produces more believable results. So, yes, counterintuitively, to make the output more reasonable for a human, you should describe WI in a more cryptic way.

That's where the main WI formats emerged from. The few most used ones are called `JSON Formatting` (named after the actual JSON file format), `Zaltys Formatting` (named after the discord community member, Zaltys 🐍#5362, who invented it) and a few formats designed by Monky: `Caveman` which evolved to `Neanderthal` which in turn evolved to `Futureman`.

### A couple of notes relevant for all formats
* All of them use forementioned [categories](#use-known-categories), the up-to-date [table of which can be found here](/AID%20WI%20Research%20Sheet.md#categories-table).
* Also, as stated above, sub-category name like `hair_color` is better than `hair color`.
* Grouping with `<>` [is better](/AID%20WI%20Research%20Sheet.md#birb-research) than `()`.
* New line is a very strong (good) way to separate groups/traits. Though, each new line takes 2 characters.

### Author's note
The A/N feature is a premium one, it's intended to enforce "meta": to make the overall narration to have a specific style or go a certain way. But the community research has shown that it can be used even in free accounts since it's no different from simply appending a formatted message like this to every third input:

`[Author's note: This novel is esoteric and descriptive. Author: Terry Pratchett. Writing style:  Metafiction, in the style of Deadpool. Genre: Witty, talkative.]`

`[Author's note: We now switch focus on Mary.]`

Or even a shortened one, saving on characters (also utilizes JSON formatting):

`A/N: [{"writing style":["descriptive", "elegant", "gritty"], "wording":["archaic", "Cockney accent"], "current state":"indoors"}]`

Doing so manually would be tedious, but with addition of scripts feature (which became available for free, too) it can be automated.

Read more about it here: [Authors Notes specifics](/AID%20WI%20Research%20Sheet.md#authors-notes-specifics).

### The best format atm
The in-depth comparison of those formats is also in the colossal "AI Dungeon World Info Research and Reference" by birb, in the [World Info and Formatting](/AID%20WI%20Research%20Sheet.md#world-info-and-formatting) section.

Some of the statements in that guide contradict each other, so some info must be outdated. What I got told in the AID discord server is:
* `JSON` is discouraged because of how wasteful it is, requiring too much boilerplate code.
* All Monky's formats are the most efficient ones in term of character/token saving. They're also simpler, easier to use, more readable and more forgiving to bad wording. So `Futureman` (the latest of Monky's) might be a good starting point for non-native speakers or for use with scripts like `EWIJSON` (see the next section).
* `Zaltys`' format seems to be the most efficient one that also supports categories. And having those is a big deal.

Whichever you choose, it's confirmed by the community members (Zaltys 🐍#5362 and Mr.Accountant 🐧#3984) that you can freely combine any styles you like in a single WI and even in a single entry, as long as you use each format on a separate line.

It's easier to learn from an example, so let's just look into the same John Shepard entry I've shown above, but written in each of those formats:

### Format examples

#### JSON
<details>
<summary>Example</summary>
  
> `Entry`:
>
> `[{"Shepard": {"name": ["Shepard", "John", "John Shepard"], "age": "30y", "gender": "male", "species": ["human", "man"], "APPEAR": {"eyes": {"eye_color": "brown"}, "hair": {"hair_color": "dark brown", "hair-length": ["short", "shaved"], "hair-style": "military haircut"}, "body": {"physique": ["muscular", "hunk"], "height": "tall_189cm", "weight": "average_102.5kg"}}}}]`
</details>

<details>
<summary>Human-readable example</summary>

Since we're trying to save every last character, you shouldn't put the text like this right into the WI. It's here just to show the format itself. It's the same example, just padded with tabs for better illustration. For the actual WI entry, all the extra tabs/spaces/new lines need to be removed.

> `Entry`:
>
> ```json
> [{
> 	"Shepard": {
> 		"name": ["Shepard", "John", "John Shepard"], 
> 		"age": "30y", 
> 		"gender": "male", 
> 		"species": ["human", "man"], 
> 		"APPEAR": {
> 			"eyes": {
> 				"eye_color": "brown"
> 			},
> 			"hair": {
> 				"hair_color": "dark brown", 
> 				"hair_length": ["short", "shaved"], 
> 				"hair_style": "military haircut"
> 			},
> 			"body": {
> 				"physique": ["muscular", "hunk"], 
> 				"height": "tall_189cm", 
> 				"weight": "average_102.5kg"
> 			}
> 		}
> 	}
> }]
> ```
</details>

Nothing to say here, it's basically JSON format as is. It's not recommended to use in WI anyway (see how much chars we waste on all those commas, extra spaces and quotes). It was tested as one of the first ones, and is here just for history... and to show what direction we're going for our entries. It's basically a pile of character keywords, hierarchically grouped into categories.
I'm not going to explain it's syntax: if you understand it, you don't need it, and if you don't — then let's just go next.

#### Zaltys

## Last step: Scripts

## Credits and links

... Massive thanks to <>, who patiently answered all my questions as I was seeking for a solid understanding of the subject.

TODO:
`you` keyword
triang brackets:
* 3 meanings
* it's not **a** citadel (a fortress of some medieval king), it's **THE** Citadel (a massive space station).
