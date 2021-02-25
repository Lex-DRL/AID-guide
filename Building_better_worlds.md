# Building better worlds <sub>*(in AI Dungeon)*</sub>
An introductory guide for game masters / somewhat experienced players who want to enhance `AI Dungeon`'s output and make it generate a more believable story, with a detailed/developed world.

This doc is just a compilation of the info already available on the subject atm of writing. See the [Credits](#credits-and-links) section for details.

<details>
<summary>Disclaimer</summary>
  
> I am not a native english speaker, so I'm apologizing for my grammar/spelling upfront.
>
> I did my best to make this guide as short and yet as structured and informative as possible, but I was making it alongside with learning the subject myself. So there might be some mistakes, missing specifics or too much of specifics here and there. Although, I believe it points you to the right direction in general.
>
> Feel free to commit/pull request any corrections you see fit.
>
> — [Lex (DRL) Darlog](https://github.com/Lex-DRL)
</details>

<details>
<summary><b>Table of contents</b></summary>

- [Introduction](#introduction)
  * [But I'm not a programmer!](#but-im-not-a-programmer)
  * [How AI remembers your WI](#how-ai-remembers-your-wi)
- [First steps: optimising just a plain english](#first-steps-optimising-just-a-plain-english)
</details>

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

The first might be not as obvious as you think. For instance, the well-known `has`/`is` difference: you can say that a `character has green eyes` or that the `character's eyes are green`. It seems the same to you, but for the AI, the former would be much harder to understand (the connection is weaker) than the latter. More on that below, here it's just as an example.

And let's talk about the the second problem, being informative...

### How AI remembers your WI

To correctly understand what statement is informative **for the AI**, we need to discuss how the AI represents your input in general. Again, I try to stay away from specifics for programmers, but we need to grasp at least the concept.

AI doesn't remember **words** you input. Neither it stores some IDs of those words. Nor it understands the meaning of those. Instead, as the very first step, AI parses (disassembles) your text into so-called **tokens**. Tokens are in essence just a common combinations of characters. So, for example, the word `APPEARANCE` is represented by 3 consequent tokens: `AP`, `PE`, `AR`, `ANCE`. Those tokens are the actual information the AI works with.

Here's an example of few common words [tested for tokens by the community](/AID%20WI%20Research%20Sheet.md#tokenization---understanding-limitations-and-special-characters):
<details>
<summary>Screenshot</summary>
  
![CATEGORY tokens](/imgs/cat-tokens.png "CATEGORY tokens")
</details>

So, back to the track. You can make an entry which have many **characters** but not so much **tokens**, and vice versa. Or you can make a descriptive entry in english which, when represented by tokens, doesn't make much sense for the AI. We want to use at least tokens as possible while keeping them as informative as possible.

Another important thing about AI memory is it's size. With each input you give, only about 2.8k charcters are fed to the NN. It's not so much even on it's own, but it's even less considering that this limit is shared between your `Remember` section, any relevant WI that AI found for the given input, the input itself and, well, the history of previous text. The specifics on how this memory shared can be found [here](/AID%20WI%20Research%20Sheet.md#remember-worldinfo-authorsnotes-worlds-and-how-the-game-handles-them). But for now — let's mark two things:
* The **overall** limit for `Remember` + `WI` + `Author's notes` (premium feature, but can be used on free account with scripts) + your `Input` + most recent part of story = 2772 chars. 
* We want to use those chars as effectively as possible, trying not to waste any of them.

## First steps: optimising just a plain english
Here's a (somewhat) full list of tips I've found so far. These tips don't require "hacking" the WI in any way. As with all other tips, I intend to extend this list with other hints as I find them.

#### Mention the subject in entry
When you mention a thing in `Keys` section, also mention it in the `Entry` itself. From now on, I'm gonna give examples in Mass Effect universe *(since that's the scenario I want to make and the one I've learned the subject for)*.
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
As stated above, `has` is much weaker than `is`. To a degree that the AI can loose the connection entirely. Ideally, you should move to a special WI formatting altogether (more on that later), but if you don't, at least use `is`.
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

#### Avoid using words with broad meaning
As a non-native english speaker, I have a small vocabulary myself. But whenever you can, put the words that carry as many sense as possible, but that sense shouldn't be broad. Ideally, your text should look like hokku, where each word carries a whole ocean of info. Remember those ridiculously clickbaity screaming tabloid headlines that yellow journalism likes to use? Like that. Each word there carries a whole image. Check yourself:
```
Titanic Survivors Found Onboard
Vampires Attack US Troops
Alien Bible Found, They Worship Oprah
```

A list of words proven to be descriptive is at the same [Personality Keywords section](/AID%20WI%20Research%20Sheet.md#personality-keywords) I quoted above.

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
The list is really long and it's get updated so I won't duplicate the info here and I'll just give a [link to the table of common categories](/AID%20WI%20Research%20Sheet.md#categories-table).

Some of the most noteable are: `SUMMARY`, `MIND`, `APPEAR`, `WORN`, `DESC`, `LIMIT/LACK`. You can read about them at the link above.
Note that all of them are in `UPPERCASE`. That's not by accident. It's still a matter of preference whether you use `UPPERCASE`, `lowercase` or `ProperCase` (aka `CamelCase`). Again, read about differences at the link above. But if you just want the "recommended" approach for beginners, it's definitely `UPPERCASE`.
<details>
<summary>Example</summary>
  
(assuming you still use a raw prose and not a specific WI format)

> `Entry`:
>
> Shepard:<br>
> SUMMARY: human male, 30y, military, Alliance forces, first human Spectre.<br>
> APPEAR: 189cm tall, 102.5kg, muscular, short military haircut, dark hair-color, brown eyes-color.
</details>

Note: the above example shows the use of special phrases like `30y` (no space). They're not just allowed but recommended to use: common phrases are treated as a single token and easy to understand for the AI.

Also note: the dash (`-`) character [is treated by the AI specially](/AID%20WI%20Research%20Sheet.md#on-certain-characters). So for some sub-categories it's better to use names like `hair-color` instead of `hair color` or just `color`.

#### Don't use emojis and special characters
Unicode emojis are supported but they cost 2 tokens. Use with caution, only if you really want to use those or an emoji as actually shorter than a regular word.
Special characters like `<>`, `[]`, `{}` and other symbols used in programming are treated... well, like in programming. The AI is trained on an immense dataset gathered by scraping internet, so it learned the meaning for those chars from where it've seen them the most: in the source code.

This is a good thing, and the WI formattings utilize that. But unless you're using one of them or testing your own format, you should avoid them in general.

Non-ASCII unicode characters like `ù` should be avoided in any case.

## Next step: World Info formats
Now we're stepping into somewhat hacky area.

As stated above (and you might already know), modern AI learns from the experience. So there inevitably will be some patterns that the AI recognizes better. That's the whole idea of so-called **WI formatting/formats**. You can't program AID directly to built the world you want, but you can format your WI entries in a specific (somewhat program-alike) style, which AI would understand much, much better. So therefore it would generate a mich more meaningful output.

That's what AID community discovered from practice, confirmed with a plenty of tests/evidences and came to the conclusion that it's much superior way to describe a world than a regular prose. So yes, you can type just a plain natural language into WI entries, and AID can automagically understand it. But you should describe your world in a more machine-readable format. The AI won't generate a machine-like text if you do so, quite the opposite: since it understands the world better, it produces more believable results. So, if you want it's output to "translate to human language" better, you should translate your input (WI, not the actual game input) to "machine-friendly language" first.

That's where the main WI formats emerged from. The few most used ones are called `JSON Formatting` (named after the actual JSON file format), `Zaltys Formatting` (named after the discord community member, Zaltys 🐍#5362, who invented it) and a few formats designed by Monky: `Caveman` which evolved to `Neanderthal` which in turn evolved to `Futureman`.

### A couple of notes relevant for all formats
* All of them use forementioned [categories](#use-known-categories), the up-to-date [table of which can be found here](/AID%20WI%20Research%20Sheet.md#categories-table).
* Also, as stated above, sub-category name like `hair-color` is better than `hair color`.
* Grouping with `<>` [is better](/AID%20WI%20Research%20Sheet.md#birb-research) than `()`.
* New line is a very strong (good) way to separate groups/traits. Though, each new line takes 2 characters.

### Author's note
The A/N feature is a premium one, it's intended to enforce "meta": to make the overall narration to have a specific style or go a certain way. But the community research has shown that it can be used even in free accounts since it's no different from simply appending a formatted message like this to every third input:

`[Author's note: This novel is esoteric and descriptive. Author: Terry Pratchett. Writing style:  Metafiction, in the style of Deadpool. Genre: Witty, talkative.]`

`[Author's note: We now switch focus on Mary.]`

Or even a shortened one, saving on characters (also utilizes JSON formatting):

`A/N: [{"writing style":["descriptive", "elegant", "gritty"], "wording":["archaic", "Cockney accent"], "current state":"indoors"}]`

Doing so manually would be tedious, but with addition of scripts feature (which became available for free, too) it can be automated.

Read more details about it here: [Authors Notes specifics](/AID%20WI%20Research%20Sheet.md#authors-notes-specifics).

### The best format atm
The in-depth comparison of those formats is also in the colossal "AI Dungeon World Info Research and Reference" by birb, in the [World Info and Formatting](/AID%20WI%20Research%20Sheet.md#world-info-and-formatting) section.

Some of the statements in that guide contradict each other, so some info must be outdated. What I got told in the AID discord is:
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
> `[{"Shepard": {"name": ["Shepard", "John", "John Shepard"], "age": "30y", "gender": "male", "species": ["human", "man"], "APPEAR": {"eyes": {"eye-color": "brown"}, "hair": {"hair-color": "dark brown", "hair-length": ["short", "shaved"], "hair-style": "military haircut"}, "body": {"physique": ["muscular", "hunk"], "height": "tall-189cm", "weight": "average-102.5kg"}}}}]`
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
> 				"eye-color": "brown"
> 			},
> 			"hair": {
> 				"hair-color": "dark brown", 
> 				"hair-length": ["short", "shaved"], 
> 				"hair-style": "military haircut"
> 			},
> 			"body": {
> 				"physique": ["muscular", "hunk"], 
> 				"height": "tall-189cm", 
> 				"weight": "average-102.5kg"
> 			}
> 		}
> 	}
> }]
> ```
</details>

Nothing to say here, it's basically JSON format as is. It's not recommended to use in WI anyway (see how much chars we waste on all those commas, extra spaces and quotes). It was tested as one of the first ones, and is here just for history... and to show what direction we're going for our entries. It's basically a pile of character keywords, hierarchically grouped into categories.
I'm not going to explain it's syntex: if you understand it, you don't need it, and if you don't — then let's just go next.

## Credits and links
TODO:
`you` keyword
triang brackets:
* 3 meanings
* it's not **a** citadel (a fortress of some medieval king), it's **THE** Citadel (a massive space station).
