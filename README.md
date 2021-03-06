# The transcriber process

This process will correlate the official transcription for the file with the text recognised from the [Speech to Text Cognitive Service](https://docs.microsoft.com/en-us/azure/cognitive-services/custom-speech-service/customspeech-how-to-topics/cognitive-services-custom-speech-use-endpoint) and generate a transcription file to be fed into the [Custom Speech](https://azure.microsoft.com/en-us/services/cognitive-services/custom-speech-service/) API. This will enable training on individual speakers with distinct accents and also apply accoustic models to filter out unwanted noise.

We will correlate recognised text with the official transcription using NLP semantic search, fuzzy matching and regular expressions as a last resort. Once trained on a single transcription file, we will use the custom model from the Custom Speech service for more accuracy which in turn will generate higher accuracy transcription files.

* To install run ```pip install -r requirements.txt``` .
* As we use [Spacy for industrial strength NLP](https://spacy.io/) the following model will need to be downloaded. Run ```python -m spacy download en_core_web_lg```


## The following parameters need to be populated. 

```WORD_SLIDE = 20```
* Slide words to the left and right for better matching but uses more CPU

```WORD_PAD = 20```
* Pad number of words onto left and right for better matching but uses more CPU

```SUBSTRING_PAD = 3```
* When we are doing substring searches as a last resort - do not change 3 is ideal

```TRANSCRIBED_FILE = '/Users/shanepeckham/sources/video/File/11_WTA_ROM_STEPvGARC_2018/11_WTA_ROM_STEPvGARC_2018.txt'```
* This is your transcribed file for the video. Format is text only. No need for speaker names or timings, only the continuous transcription text.

```AUDIO_PROCESSED_FILE = '/Users/shanepeckham/sources/video/File/11_WTA_ROM_STEPvGARC_2018/11_WTA_ROM_STEPvGARC_OFFSET.txt'```
* This is the file that is automatically generated by the Speech to Text process

```GENERATED_TRANSCRIPT_FILE = '/Users/shanepeckham/sources/video/Results2/11_WTA_ROM_STEPvGARC_TRANSCRIPT_OUTPUT.txt'```
* This is the automated transcript that will be generated

```PASS2_THRESHOLD = 80```
* This is the second pass threshold using broader semantic search and fuzzy matching - the higher the value the more precise but the more restrictive the match criteria.The recommended value is 80%. Format - enter 80 for 80%


```PASS3_THRESHOLD = 72```
* This is the third pass threshold using expression and pattern matching - the higher the value the more precise but
the more restrictive the match criteria. The recommended value is 72%. Format - enter 72 for 72%
