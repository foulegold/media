# Audio Generation and Voice Cloning Best Practices for Safe, Clear Results

Synthetic audio has moved from novelty to everyday production tool. A training video can be narrated in eleven languages by the same voice, a podcast intro can get a custom score in minutes, and a game prototype can ship with hundreds of generated footsteps, doors, and ambiences. Workspaces such as [Gen.new](https://gen.new/) place text, music, image, and video generation side by side, so a single project can move from script to narration to soundtrack without leaving one collaborative environment. That convenience brings a responsibility. Generated audio can mislead listeners, infringe on someone's voice or music, or simply sound bad enough to undermine the content it supports. This guide covers the practices that keep voiceovers, sound design, and music clear, consistent, and legally defensible.

## Three Kinds of Generated Audio and Their Different Risks

Generated audio falls into three working categories. Each has its own quality criteria and its own legal exposure, and treating them as one category leads to mistakes. A rule that is sensible for music, such as checking for melodic similarity to existing songs, means little for a door slam. A rule that matters for voices, such as written consent, rarely applies to rain ambience.

| Category | Typical uses | Main quality criterion | Main compliance risk |
| --- | --- | --- | --- |
| Voiceover and voice cloning | Narration, dubbing, e-learning, IVR menus, audiobooks | Intelligibility and correct pronunciation | Impersonation, missing consent, deceptive use |
| Sound design | Foley, ambiences, UI sounds, transitions, game effects | Fit with picture and absence of artifacts | Low; occasional trademarked sound signatures |
| Music | Background beds, intros, jingles, full tracks | Structure, mix balance, loudness | Similarity to copyrighted works, licensing terms, distribution rules |

Voice work carries the heaviest burden because a voice identifies a person. A synthetic voice that resembles a real individual can be used to defraud, defame, or misrepresent, and several jurisdictions now treat voice as a protected attribute of identity.

## Consent and Rights Come Before the First Generation

### Voice cloning requires documented permission

Cloning a voice means training or conditioning a model on recordings of a specific person. The only safe basis for doing so is explicit, written consent from that person, or from the legal holder of their likeness rights if they are deceased. A verbal "sure, go ahead" during a recording session is not sufficient documentation if a dispute arises two years later.

A usable consent agreement specifies the scope of use. It names the languages the voice may speak, the types of content permitted, whether the clone may be used for advertising or political messaging, the duration of the license, and how the person can revoke permission. It also states what happens to the voice model and source recordings after the license ends. Professional voice actors increasingly negotiate these terms through unions; in the United States, SAG-AFTRA agreements now include specific provisions on digital replicas, including consent and compensation for each use.

Several laws make consent a legal requirement rather than a courtesy. Tennessee's ELVIS Act, in force since July 2024, extends right-of-publicity protection to voice and covers simulations of it. California has enacted laws restricting unauthorized digital replicas of performers. In 2024 the US Federal Communications Commission ruled that AI-generated voices in robocalls count as "artificial" voices under the Telephone Consumer Protection Act, which makes unsolicited synthetic-voice calls without prior consent illegal. In the European Union, a voice is personal data under the GDPR when it can identify a person, so processing recordings for cloning needs a lawful basis and respects deletion rights.

Never clone a voice from public recordings such as interviews, YouTube videos, or podcast episodes without permission, even for parody or internal testing. Reputable platforms prohibit it in their terms and some require a live verification step, where the speaker reads a randomly generated phrase to prove they are present and agreeing.

### Stock and designed voices avoid the problem

When a project does not need a specific person's voice, a platform's library voice or a fully synthetic designed voice removes the consent question. Designed voices are generated from parameters such as age, accent, pitch, and timbre rather than from one individual. They still come with license terms, so check whether commercial use, broadcast, or resale in other products is included.

### Music licensing depends on the platform's terms

Generated music is not automatically free to use. Copyright treatment of AI output varies: the US Copyright Office has stated that purely machine-generated material without meaningful human authorship is not eligible for copyright registration. That cuts both ways. A user may be unable to stop others from copying an unedited generated track, while the platform's terms of service still govern how the user may distribute it. Read whether free-tier output can be monetized, whether attribution is required, and whether tracks can be uploaded to streaming services or registered with Content ID systems. Registering a generated track with Content ID often causes false claims against other users who generated similar material, and some distributors reject such registrations.

## Technical Standards for Clear Audio

### Source recordings for voice cloning

A clone reproduces the flaws of its training audio. Room reverb, a humming refrigerator, or mouth clicks in the source material show up in every generated line. Record source audio as uncompressed WAV at 48 kHz and 24-bit depth. Keep the noise floor below about -60 dBFS, which in practice means a treated room or a closet lined with clothing, and a microphone 15 to 20 centimetres from the mouth with a pop filter.

Quantity matters less than consistency. Instant cloning systems often work from one to three minutes of speech; higher-fidelity professional clones typically need 30 minutes to several hours. In both cases, the speaker should hold one consistent delivery style. Mixing a calm narration read with energetic promotional lines produces a clone that wavers between the two unpredictably. If a project needs both styles, record and train two separate voice profiles.

Do not apply heavy processing before training. Compression, noise reduction, and EQ baked into source files become part of the voice. Light high-pass filtering around 80 Hz to remove rumble is acceptable; aggressive denoising that creates watery artifacts is not.

### Script preparation prevents most pronunciation errors

Text-to-speech engines guess pronunciation from spelling and context, and they guess wrong on names, acronyms, numbers, and homographs. "Read" in past and present tense, "lead" the metal and "lead" the verb, and "St." as Street or Saint are routine failures. Prepare scripts before generation rather than fixing lines afterward.

Write numbers the way they should be spoken: "twenty twenty-six" rather than "2026" if the year should not be read as "two thousand twenty-six." Spell acronyms with periods or spaces when they should be read letter by letter, and as words when they are pronounced as words. Where the engine supports SSML, use phoneme tags with IPA or the engine's own phonetic alphabet for brand names and proper nouns, and break tags to control pauses. Build a pronunciation dictionary for each recurring project so that a company name sounds identical in episode one and episode forty.

Punctuation acts as direction. A comma produces a short pause, a full stop a longer one, and an em dash often a slight change in pitch. Long sentences with stacked clauses sound rushed in synthetic speech; split them.

### Loudness and peak targets by destination

Generated audio arrives at inconsistent levels. A voiceover may peak at -3 dBFS while a generated music bed sits at -20 LUFS integrated. Normalize every deliverable to its destination's standard. Loudness is measured in LUFS (or LKFS, the equivalent term in US broadcast) and peaks in dBTP, true peak, which accounts for inter-sample overs that standard peak meters miss.

| Destination | Integrated loudness target | True peak ceiling |
| --- | --- | --- |
| European broadcast (EBU R128) | -23 LUFS | -1 dBTP |
| US broadcast (ATSC A/85) | -24 LKFS | -2 dBTP |
| Spotify and YouTube (playback normalization) | about -14 LUFS | -1 dBTP |
| Apple Music | about -16 LUFS | -1 dBTP |
| Podcasts, stereo | -16 LUFS | -1 dBTP |
| Podcasts, mono | -19 LUFS | -1 dBTP |
| E-learning and corporate video | -16 to -18 LUFS | -1 dBTP |

Streaming platforms turn loud tracks down, so mastering a background bed at -8 LUFS gains nothing and adds distortion. For narration over music, keep the music bed 15 to 20 dB below the voice during speech, and use sidechain ducking so the bed rises in pauses rather than staying flat throughout.

### Listening for generation artifacts

Generated speech has characteristic faults. Listen on headphones at moderate volume for metallic or phasey sibilants, breaths that cut off mid-inhale, words that are swallowed at the end of a sentence, sudden pitch jumps between adjacent sentences, and repeated syllables. Generated music shows other faults: melodies that lose their key center after a minute, drum patterns that drift off grid, vocals with garbled pseudo-words, and endings that fade abruptly or loop. Sound effects often contain tails that are cut short or low-frequency content far below what the scene needs.

Check every file on two systems: closed-back headphones for detail and a phone speaker for intelligibility. A large share of listeners hear content through phone speakers, which remove almost everything below 200 Hz. A voice that relies on low warmth to sound clear will become thin and harder to follow.

## Keeping Output Consistent Across a Project

Consistency is the hardest quality to maintain with generative tools, because each generation is a fresh sample. Two lines generated a day apart with identical text can differ in pace and emphasis. Over a 30-module course or a 12-episode series, that drift becomes obvious.

Lock the settings. Most voice engines expose parameters such as stability, similarity, style exaggeration, and speaking rate. Higher stability produces more uniform, sometimes flatter delivery; lower stability adds expressiveness and variance. Choose values during a test phase, record them in a project document, and do not change them mid-project. Where a seed value is available, store it with each approved generation so it can be reproduced.

Generate in context, not line by line. Producing a full paragraph at once gives the model the surrounding sentences to shape intonation, which sounds more natural than stitching single sentences together. When a single line needs a fix, regenerate the surrounding sentence as well so the join is not audible.

Keep a version log. Record the script version, voice ID, model version, settings, and date for every exported file. Platforms update their models, and a voice that sounded one way in March may sound slightly different after an engine update in June. The log tells you whether a mismatch comes from your settings or from the platform, and it tells you which files may need regeneration together.

For music, consistency means a defined palette. Write a reference prompt that specifies tempo in BPM, key, instrumentation, and mood, and reuse it as the base for every cue. A brand that uses a 92 BPM lo-fi bed in D minor with Rhodes piano should not get a 128 BPM synthwave track in episode seven because a prompt was phrased differently. Request stems when the tool offers them, so that drums, bass, and melody can be balanced and edited separately.

## Sound Design With Generative Tools

Generated sound effects work best when the prompt describes the physical event rather than the emotion. "Heavy wooden door closing slowly in a stone hallway, latch click, short reverb" gets closer than "ominous door sound." Specify material, size, distance, and space. For ambiences, ask for a length longer than the scene needs, then trim, because generated loops often have audible seams at their start and end. Crossfade loop points over 50 to 200 milliseconds.

Layer generated material with care. A single generated explosion often sounds thin; three layers covering low impact, mid crunch, and high debris sound fuller. Check that layers do not phase-cancel by listening in mono. For interface sounds, keep files short, under 300 milliseconds for clicks and confirmations, and trim silence at the head so the sound fires exactly with the on-screen action.

Sound design carries less legal risk than voice or music, with one exception: some sounds function as trademarks. Well-known audio logos, startup chimes, and broadcaster stings are protected brand assets. Do not prompt a generator to recreate them, and reject outputs that closely resemble them.

## Music Generation Practices

Prompt for structure. Many music generators accept section markers such as intro, verse, chorus, bridge, and outro, along with durations. A 30-second advertisement cue needs a different shape from a three-minute background track: an immediate hook and a clean ending on the downbeat, rather than a slow build.

Avoid naming living artists in prompts. Requests such as "a song in the style of" a specific singer increase the chance of output that imitates a recognizable voice or signature melody, and several platforms block such prompts. Describe the attributes instead: tempo, era, instruments, vocal register, production texture.

Screen output for similarity before publishing. Listen for melodies or lyrics that feel familiar, and run finished tracks through an audio recognition service if one is available. A generated track that triggers a match against a commercial recording is unusable for distribution regardless of how it was made.

Lyrics deserve separate review. Generated lyrics can contain nonsense phrases, unintended meanings in other languages, or lines lifted from existing songs. Write or edit lyrics as text first, then generate vocals from the approved text.

## Disclosure, Labeling, and Watermarking

Listeners increasingly expect to know when a voice is synthetic, and regulators increasingly require it. The EU AI Act's transparency obligations, applicable from August 2026, require that deployers of systems generating deepfake audio disclose that the content was artificially generated or manipulated, with limited exceptions for evidently artistic or satirical works. Providers of generative systems must mark output in a machine-readable way. Advertising regulators in several countries treat an undisclosed synthetic voice imitating a real person as deceptive.

Disclosure works on two levels. The human-readable level is a credit line, a spoken or on-screen note, or a description field stating that narration was generated with AI. The machine-readable level is metadata and watermarking. Content Credentials based on the C2PA standard attach signed provenance information to a file, recording which tool created it and what edits followed. Audio watermarking systems embed an inaudible signal that survives compression and can later identify the content as synthetic. Do not strip this metadata during export or transcoding; some audio editors discard it by default when saving to MP3.

Some uses call for disclosure regardless of law. Synthetic voices in customer-service lines, political messaging, news-style content, and anything addressed to children should always be labeled clearly. A cloned voice of a deceased person, even with estate permission, warrants an explicit note to the audience.

## Practical Walkthrough: A 90-Second Product Explainer

Consider a small software company producing a 90-second explainer video in English and Spanish. The narration uses a cloned voice of its head of customer support, with a generated music bed and a handful of interface sounds. The process below covers it from consent to delivery.

1. Obtain consent. The employee signs a voice license that covers English and Spanish narration for product marketing and support videos for 24 months, excludes political and third-party advertising, and states that the voice model will be deleted within 30 days of revocation or departure from the company. Employment alone does not imply consent.
2. Record the source. The employee reads 20 minutes of varied product-related text in a calm explanatory tone, captured as 48 kHz, 24-bit WAV in a quiet office with acoustic panels. Only a high-pass filter at 80 Hz is applied before upload.
3. Prepare the script. The writer replaces "v4.2" with "version four point two," adds an IPA phoneme entry for the product name, and splits two 40-word sentences into four shorter ones. The Spanish script is translated by a native speaker, not machine-translated and left unchecked, because word length grows by roughly 15 to 25 percent and the timing needs adjusting.
4. Generate and log. Narration is generated paragraph by paragraph with stability and speaking rate fixed after three test reads. Each approved take is logged with voice ID, model version, settings, and script version.
5. Create the music bed. A prompt specifies 100 BPM, light acoustic guitar and soft percussion, optimistic and unobtrusive, 95 seconds, clean ending. Stems are exported so the guitar can be lowered under dense narration.
6. Design interface sounds. Three short click and confirmation sounds are generated, trimmed to under 250 milliseconds, and aligned to the animation frames.
7. Mix and master. Music is ducked 18 dB under speech with sidechain compression. The final mix is normalized to -16 LUFS integrated with a -1 dBTP ceiling for web delivery, then checked on headphones and on a phone speaker.
8. Disclose and archive. The video description states that narration is AI-generated using the voice of a named employee with permission. C2PA metadata is preserved in the export. Source recordings, consent form, and generation log are stored together for audit.

The Spanish version reveals one edge case: the cloned voice carries a slight English accent in Spanish. The company decides that is acceptable for its audience and notes it in the log, rather than switching to a different voice mid-campaign, which would break consistency between language versions.

## Common Failure Modes and Edge Cases

A clone used across languages may pronounce loanwords and names in the wrong language's phonology. Cross-lingual models often default to the source language's accent. Test a sample in each target language with native listeners before committing.

Emotional range is limited. A clone trained on calm narration will struggle to deliver shouting, crying, or whispering convincingly. Forcing it with style settings produces distortion. Record dedicated source material for each register a project needs, or use a human performer for emotional peaks.

Concatenated fixes can create audible seams where room tone or pitch changes between takes. Add a consistent low-level room tone under the full narration to mask joins, and regenerate whole paragraphs when edits accumulate.

Revocation is a real scenario. When a voice owner withdraws consent, published content may still exist. The license should state whether existing published material remains in use or must be withdrawn, and the team needs to know which files used the voice, which the generation log provides.

Platform changes can break reproducibility. If a provider retires a model version, exact regeneration of earlier lines may become impossible. Archive final masters and, where possible, keep the approved raw generations rather than relying on regenerating them later.

Before any generated audio is published, a short review catches most of these problems:

- Consent documentation exists for every cloned voice and covers this specific use.
- Pronunciation of names, numbers, and acronyms has been checked by a listener who did not write the script.
- Loudness and true peak meet the destination standard.
- The mix has been checked on headphones and on a phone speaker.
- Music has been screened for similarity to existing recordings.
- Disclosure text is present and provenance metadata survived export.
- The generation log and source files are archived together.

## FAQs

### Is it legal to clone my own voice?

Yes. Cloning your own voice is generally lawful, and most platforms allow it after a verification step. The main considerations are the platform's terms on who owns the voice model and how others may use it if you share access. Keep control of the account that holds the model, since anyone with access can generate speech in your voice.

### Can I use AI-generated music in a monetized YouTube video?

Usually yes, provided the generating platform's license allows commercial use at your subscription tier. Check whether the free tier excludes monetization, and avoid registering the track with Content ID, which can trigger disputes with other users who generated similar audio. Keep a record of the generation date and account in case of a claim.

### How much audio is needed to create a good voice clone?

Instant clones can work from one to three minutes of clean speech, but they capture timbre more than delivery habits. Professional-grade clones typically use 30 minutes or more. Recording quality and consistent delivery matter more than total length; ten clean minutes outperform an hour recorded in an echoing room.

### Do I have to tell my audience that a voice is AI-generated?

In a growing number of contexts, yes. The EU AI Act requires disclosure for synthetic audio that resembles real people, and US rules restrict synthetic voices in robocalls without consent. Beyond legal requirements, disclosure is good practice for any content where listeners might reasonably assume a human is speaking, such as news, customer service, or testimonials.

### Why does my generated voiceover sound different from one session to the next?

Generation is probabilistic, and small differences in text context, settings, or model version change delivery. Fix your voice settings, generate whole paragraphs rather than single lines, store seed values where available, and log the model version. If the platform updated its engine, regenerate related lines together so they match each other.

### What loudness should I use for a podcast with AI narration?

Target -16 LUFS integrated for stereo podcasts or -19 LUFS for mono, with true peaks no higher than -1 dBTP. Apply the target to the final mix, including music and effects, rather than to the voice track alone.

## Conclusion

Generated audio is now good enough that its weaknesses are rarely technical alone. A voiceover fails because nobody secured consent, because a product name was mispronounced in forty files, or because episode nine sounds like a different narrator from episode one. Music fails because its license excluded the channel it was published on. The practices in this guide address those failure points directly: documented permission before cloning, clean source recordings, prepared scripts, fixed settings and version logs, destination-specific loudness, and clear disclosure backed by provenance metadata. Teams that treat generated audio with the same production discipline as recorded audio get output that is clear, consistent, and defensible when questions arise.
