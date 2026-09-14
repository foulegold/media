# Why AI Companion Image Generators Ignore Your Prompt (And How to Fix It)

The complaint repeats across almost every AI companion platform: the picture looks good, but it is not the picture that was ordered. A documented test at [https://virtualcandy-ai.com/blog/darlink-ai-review/](https://virtualcandy-ai.com/blog/darlink-ai-review/) shows the pattern in one run. The reviewers asked DarLink AI for an existing character in a full-body airport scene, wearing a corset, with a scared expression, in landscape format. The platform charged 2 tokens and returned a polished portrait-style bedroom image. The character's face and body type were recognisable. The location, expression, clothing, framing and orientation were not. That outcome is not a DarLink quirk. The same failure appears on Candy AI, Secrets AI, Kupid AI and most other companion apps that bolt an image model onto a chat product, and the causes are structural rather than random.

## How a companion image generator actually reads your request

A companion app does not send your words directly to an image model. Two or three separate inputs compete for control of the final picture. First, the identity of the character: a reference embedding, a set of saved appearance parameters, or a fine-tuned weight that keeps the face, hair, skin tone and body type stable across generations. Second, your scene request, whether typed freely or assembled from dropdown menus for pose, outfit, location and expression. Third, a hidden platform prompt that enforces the house style, typically a glossy, well-lit, centred portrait with a shallow depth of field.

Those inputs are merged into one instruction before generation. Identity conditioning almost always carries the highest weight, because a companion app that changes the character's face every time would be unusable. The house style comes next. Your scene request is last in the priority order, and it is the only one of the three that the user can see.

Training data compounds the problem. Companion platforms fine-tune on portrait imagery: headshots, three-quarter shots, bedroom and studio settings. When the model receives an unusual combination, such as a full-body figure inside an airport terminal, it falls back to the compositions it has seen most often. A bedroom appears because a bedroom is the statistical default, not because the model rejected the airport.

A parameter-based editor adds a further layer. Selecting "airport" from a location menu inserts a short text fragment. Selecting "scared" inserts another. Selecting "full body" and "landscape" inserts two more. Stack five fragments on top of the identity block and the style block, and each individual instruction receives a small share of the model's attention. The instructions that survive are the ones reinforced by training data; the ones that get dropped are the ones that conflict with it.

## The five failures that account for most wasted generations

The table below maps the requests that go wrong most often to what the model returns instead and the mechanism behind the substitution.

| Requested element | What usually appears instead | Underlying cause |
| --- | --- | --- |
| Specific location (airport, kitchen, rooftop, street) | Bedroom, studio backdrop or undefined interior | Portrait-heavy training data; background receives least attention |
| Full-body or wide framing | Head-and-shoulders or waist-up portrait | House style prompt biases toward close framing |
| Strong emotion (scared, angry, crying) | Neutral or smiling face | Identity embedding was built from a calm reference face |
| Named clothing item (corset, trench coat, uniform) | Generic lingerie, dress or default outfit | Outfit token conflicts with the character's saved default outfit |
| Landscape or square orientation | Portrait aspect ratio | Aspect ratio is hard-coded or overridden by the style preset |

### Wrong location

Background is the element with the lowest priority in every companion generator tested by reviewers. A location word competes with the identity block, the style block and any outfit or pose instruction, and it loses. The result is the DarLink outcome: an airport request answered with a bedroom. Locations with distinctive visual anchors survive better than abstract ones. "Airport" is abstract; "standing next to a departures board with suitcases" gives the model concrete objects to place.

### Framing drift

Full-body requests fail because the identity embedding was captured from a face. The model reproduces that face at the scale it learned, which means a large face in the frame and therefore a tight crop. Asking for "full body" without also specifying what fills the remaining space leaves the model free to zoom back in. Adding floor, shoes and a visible horizon line forces the wider composition.

### Expression defaults

A companion character is saved with a reference expression, usually neutral or a light smile. Every generation starts from that face. A request for "scared" must overwrite the saved expression, and a single adjective rarely has enough weight to do it. Physical descriptions work where emotional labels fail: "eyes wide, mouth slightly open, eyebrows raised" describes the geometry of fear rather than naming it.

### Clothing substitution

Characters carry a default outfit from their profile. A new outfit word competes with that default, and the default wins if the new word is unusual or if the outfit dropdown and the free-text field disagree. Corsets, uniforms and period costumes are the most frequent casualties because they appear rarely in the training set relative to dresses and underwear.

### Orientation ignored

Many companion apps expose a landscape toggle that does nothing, or that is overridden by a style preset locked to 3:4 or 9:16. The DarLink test requested landscape output and received portrait. If the platform's gallery shows only vertical images, assume the toggle is cosmetic and plan compositions accordingly.

## Why the character looks right while everything else goes wrong

Users often read this pattern as the model "ignoring" them. The more accurate description is that the model obeyed the highest-weighted instruction and discarded the rest. In the DarLink run, the reviewers confirmed the character's appearance stayed consistent: the saved parameters for age 25, hazel eyes and a skinny body type carried through. That consistency is the platform's primary engineering goal, and it comes at the direct expense of scene accuracy.

The trade-off is visible in the platform's own review data. DarLink scored 4.2 for media quality but drew an explicit note that instruction accuracy was weak in the test run. Reddit discussion of the same platform repeats the complaint about image prompt accuracy. Convincing visual quality and poor instruction adherence are not contradictory; they are two outputs of the same design choice.

Understanding this changes the strategy. Fighting the identity weight is futile. Working around it, by giving the scene elements enough concrete detail to survive the merge, is not.

## What a missed prompt costs in tokens

Every companion platform meters image generation, and every failed generation is charged at the same rate as a successful one. DarLink publishes the figures: 2 tokens per image, 20 per video. The monthly allowance is 100 Coins on Essential, 300 on Advanced and 500 on Ultimate. In theory that is 50, 150 and 250 images per month. In practice, the number of usable images depends on how many attempts each scene requires.

| Plan or pack | Tokens | Theoretical images at 2 tokens | Usable scenes at 3 attempts each | Usable scenes at 1 attempt each |
| --- | --- | --- | --- | --- |
| Essential (100 Coins/month) | 100 | 50 | 16 | 50 |
| Advanced (300 Coins/month) | 300 | 150 | 50 | 150 |
| Ultimate (500 Coins/month) | 500 | 250 | 83 | 250 |
| 100-token pack ($9.99) | 100 | 50 | 16 | 50 |
| 550-token pack ($49.99) | 550 | 275 | 91 | 275 |

The middle column is the realistic figure for a user who writes complex prompts. Three attempts per scene turns a 50-image entry allowance into 16 finished pictures. At the 100-token pack price of $9.99, each usable scene costs roughly 60 cents rather than 20. Users who send one video request per failed image scenario do worse still: one 20-token video equals ten images, so a single wrong video wipes out the equivalent of ten portrait generations.

Token accounting also has edge cases worth checking before relying on the arithmetic. Some platforms charge for generations that fail validation. Some expire unused monthly Coins at renewal. Some, including DarLink, use two different names, Coins and Tokens, on different screens without explaining whether they are the same unit. None of this changes the core rule: fewer attempts per scene is the only lever the user controls.

## How to simplify a request so the model keeps it

The most reliable improvement is to reduce what the model must change in a single generation. The following rules cut the average attempt count on most companion platforms.

- Change one element per generation. Location first, then framing, then outfit, then expression. Each step starts from the previous successful image where the platform supports image-to-image.
- Replace emotional adjectives with physical descriptions. "Eyebrows raised, mouth open, leaning back" survives the merge; "scared" often does not.
- Anchor locations with objects. "Departures board, rolling suitcase, tiled floor" beats "airport" because each noun gives the model something to render.
- Drop every instruction that the profile already covers. Restating hair colour, age or body type spends attention on things the identity block already enforces.
- Use the dropdown menus or the free-text field, not both for the same attribute. Conflicting inputs resolve toward the default.
- Do not request a change in orientation unless the platform's gallery proves the toggle works.
- State the framing in terms of what is visible: "shoes on the floor, head near the top of the frame" rather than "full body".

Negative phrasing deserves a separate warning. "Not smiling" contains the word "smiling" and often produces a smile. "Without a bed" often produces a bed. Most companion generators either lack a negative-prompt field or weight it weakly, so describe what should be present and leave out what should not.

Order also matters inside a free-text prompt. The first ten to fifteen words receive the most attention. Put the element that failed last time at the front. If the location keeps defaulting to a bedroom, the prompt should open with the location, not with the outfit.

## Rebuilding the airport scene step by step

The DarLink test bundled five changes into one 2-token request and lost four of them. The same scene, built in stages, illustrates how the staged approach reduces waste. Each step assumes the platform keeps the character identity fixed and allows the previous output to seed the next generation.

1. Generate the location alone. Prompt: "standing in an airport terminal, departures board behind her, tiled floor, daylight through large windows." Keep the default outfit and neutral expression. Cost: 2 tokens. Verify the background before proceeding; if a bedroom appears, rewrite the location with more objects and retry once.
2. Widen the framing. Prompt: same location plus "full figure visible, shoes on the floor, head near the top of the frame, camera at waist height." Cost: 2 tokens. Check that the feet are in frame.
3. Add the outfit. Prompt: previous text plus "wearing a black corset with visible lacing over a white blouse." The blouse gives the corset context and reduces the chance of substitution with generic underwear. Cost: 2 tokens.
4. Add the expression last. Prompt: previous text plus "eyes wide, eyebrows raised, mouth slightly open, looking off to the left." Cost: 2 tokens.
5. Skip the landscape toggle unless a prior test confirmed it works. If it does, apply it at step 2, where the composition is being set, not at the end.

Total cost with no retries: 8 tokens for a scene that matches the request. The single-shot attempt cost 2 tokens and matched almost nothing; a user who repeated that single-shot attempt five times would have spent 10 tokens with no guarantee of improvement, because each retry re-rolls all five elements at once. Staging costs slightly more per finished scene than a lucky single shot but far less than the typical three-to-five-attempt cycle.

## Edge cases where simplification still fails

Some requests exceed what current companion generators can deliver regardless of prompt structure. Recognising them in advance prevents repeated charges.

Readable text is the clearest example. Signs, name tags, phone screens and book titles come out as glyph-like shapes. Requesting "a sign that says Gate 12" produces a sign with garbled characters, and no amount of rewording fixes it on models that lack a text-rendering pathway.

Group images with two or more saved characters push the identity problem to its limit. Each character's embedding competes with the other's, and faces blend. DarLink supports group chat with up to three additional characters, but image generation with multiple identities remains unreliable across the category.

Extreme expressions run into the same wall as strong emotions, only harder. Crying, screaming or laughing with the head thrown back distort the face enough that the identity weight pulls it back toward the reference. Moderate physical descriptions, such as "eyes closed, slight grimace," land more often than dramatic ones.

Night and low-light scenes tend to brighten. The house style prompt usually includes lighting instructions, and those override "dark room" or "moonlight." Specifying a light source, "lit only by a phone screen" or "single candle on the table," gives the model a reason for the darkness and improves the hit rate.

Specific brands, real locations and named landmarks are filtered or poorly represented. A request for a recognisable airport lounge or a branded suitcase returns a generic equivalent at best. Describing the visual features instead of the name is the only workable approach.

## Testing a platform before committing tokens

A short diagnostic run reveals how a given generator handles instructions before a subscription decision. Spend six tokens, three images, and vary one element at a time: one image with an unusual location, one with full-body framing, one with a strong expression. The results show which instructions the platform respects and which it drops. On DarLink, the free account allows enough access to complete this check, and the review confirms the character builder retains saved appearance settings, so identity consistency can be assumed and the test can focus on scene control.

Record the outcomes. A platform that honours locations but ignores framing calls for a different prompt strategy than one that honours framing but ignores expressions. Reddit threads and review sites provide a starting point, but individual runs vary, and a six-token test is cheaper than a month of guesswork.

## FAQs

### Why does the character look correct but the background is wrong?

The character's identity carries the highest weight in the generation pipeline, and the platform's style preset carries the second highest. The background is the lowest-priority input and gets dropped first when instructions conflict. Anchoring the location with concrete objects raises its chance of surviving.

### Does writing a longer, more detailed prompt improve accuracy?

Usually the opposite. Each additional instruction takes attention from the others, and the model keeps the ones reinforced by training data. Shorter prompts that change one element at a time produce more predictable results and fewer paid retries.

### Is a failed generation charged at the same rate as a successful one?

On DarLink, and on most companion platforms, yes. An image that misses the location, expression and framing still costs 2 tokens. That is why reducing attempts per scene matters more than any single prompt trick.

### Why does "not smiling" produce a smile?

Most companion generators lack an effective negative-prompt field. The word "smiling" is read as a positive instruction regardless of the "not" preceding it. Describe the desired mouth position directly instead.

### Can the landscape toggle be trusted?

Only if the platform's gallery or output history shows horizontal images. In the documented DarLink test, a landscape request returned a portrait. Treat orientation controls as unverified until a test confirms them.

### How many images can 100 tokens realistically produce?

At 2 tokens each, 100 tokens cover 50 generations. If each finished scene needs three attempts, that is around 16 usable images. Staged prompting, one change per generation, typically lands closer to 25 to 30 usable scenes from the same 100 tokens.

## Conclusion

Companion image generators do not ignore prompts at random. They rank inputs, and the user's scene request sits at the bottom of that ranking beneath character identity and house style. The documented DarLink run, five instructions in, one honoured, is the predictable output of that architecture, not an isolated defect. Every missed element is charged, so a 50-image allowance shrinks to a fraction of that under multi-attempt prompting. The remedy is procedural: change one element per generation, describe physical details rather than emotional labels, anchor locations with objects, avoid negative phrasing and skip controls that a test has not verified. Eight tokens spent in four deliberate steps beat ten tokens spent re-rolling the same overloaded request, and the difference compounds across a month of use.
