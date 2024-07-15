Attempting to restore Prompt engineering within xttsv2 model

Key Points/Theories

Tortoise TTS supported prompt engineering to manipulate the sound/intonation of the generated speech by adding text in brackets, e.g. "[joy]It's nice to see you!". This allowed evoking specific emotions in parts of the speech. XTTS v2 lost this capability and just speaks the prompt text literally.

The prompt engineering in Tortoise worked by using an alignment mechanism backed by wav2vec2 to identify where the bracketed text should influence the speech. If wav2vec2 mistranscribed the text, the alignment could fail leading to poor results. 

The autoregressive model dimensionality is different in XTTS v2 compared to Tortoise. XTTS uses a max prompt tokens of 70 vs 2 in Tortoise.


The CLVP model in Tortoise v2 was small and may have restricted the generation of intonation. A bigger CLVP model was planned to help account for intonation better when scoring text-speech alignment. 

Tortoise aimed to build a word-alignment mechanism to identify where each word is spoken in the output, enabling extracting specific phrases with certain prompt engineering,

The Univnet vocoder used in Tortoise was treated as a nearly lossless conversion from mel spectrogram to audio. Injecting tonality at the vocoder level was not considered the right approach.


XTTS v2 diverged from Tortoise by losing the expressive prompt engineering capabilities while making architectural changes to the autoregressive model. The limited CLVP model and lack of word-level alignment were acknowledged limitations in Tortoise that aimed to be improved in the future.

Code Summary
the mrq repo (https://git.ecker.tech/mrq/tortoise-tts) had some xtts modification. COuld lead to something?
The code changes in api.py and autoregressive.py update the Tortoise TTS model to support XTTS v2:

Different autoregressive model dimensionality is used for XTTS
the code changes alone don't reveal the full context of the differences and tradeoffs between Tortoise and XTTS, which the GitHub discussion provides insight into. Preserving the prompt engineering capabilities while evolving the architecture seems to be the ideal path forward.
