# The M-AILABS Speech Dataset

The following is the text that accompanied the M-AILABS Speech DataSet:

The M-AILABS Speech Dataset is the first large dataset that we are providing free-of-charge, freely usable as training data for 
*speech recognition* and *speech synthesis*.

Most of the data is based on [LibriVox](https://librivox.org/) and [Project Gutenberg](https://www.gutenberg.org/).
The training data consist of nearly thousand hours of audio and the text-files in prepared format.

A transcription is provided for each clip. Clips vary in length from 1 to 20 seconds and have a total
length of approximately shown in the list (and in the respective `info.txt`-files) below.

The texts were published between 1884 and 1964, and are in the public domain. The audio was recorded by the 
LibriVox project and is also in the public domain - *except for Ukrainian*.

Ukrainian audio was kindly provided either by [Nash Format](https://nashformat.ua/) or [Gwara Media](http://gwaramedia.com.ua/)
for machine learning purposes only (please check the data `info.txt` files for details).

Before downloading, please read the license agreement at the bottom of this posting first!

## Intro

People have asked us "Why", i.e. "why are you giving away this much highly valuable data".</p>

The quick answer is: because our mission is *to enable (European) companies to take advantage of AI & ML without having to give up control or know-how.*

The full answer would be significantly longer, but let's say we just want to advance the use of AI & ML in Europe.

## Directory Structure

Each language is represented by its international ISO-Code for language + country (e.g. `de_DE` for `de` =German, `DE` =Germany) plus an addition `by_book` directory.

Below that, you will find directories named:

- female
- male
- mixed

The training data is split into `female` , `male` and `mixed` voices. In case of mixed, the training data contains `male` and `female` data mixed.


For each voice, there is the name and some `info.txt` containing information about the training data. Each training-data directory contains two files:

- `metadata.csv`
- `metadata_mls.json`


The full directory structure looks like this:

[Screenshot](./images/dir_structure.png?raw=true)

## Format

**All audio-files are in wav-format, mono and 16000 Hz.**

The complete training data is in the MLS (M-AILABS)-  *and* LJSpeech-Format. Each `book` contains its own `metadata.csv`  and `metadata_mls.json`.


Those of you who know the LJSpeech data format will immediately recognize the .csv-file. The `_mls.json` file contains the same information as the `.csv` -file except that that information is in JSON-format.

Each line in a `metadata.csv` consist of a filename (without extension) and two texts, separated by a " `|` "-symbol. The text includes upper- and lower-case characters, special-characters (such as punctuation)
and more. If you need clean-text, please clean it before using it. For Speech Synthesis, sometimes you need all special characters.

The first text contains the fully original data, including  *non-normalized * numbers, etc. The second version of the text contains the  *normalized version*, meaning numbers have been converted to words and some cleanup of &#8220;foreign&#8221; characters (transliterations) have been applied.

Both files are in UTF-8-Format. Do not try reading it in ASCII, it won't work.


        grune_haus_01_f000002|Ja, es ist ein grünes Haus, in dem ich 1989 wohne...|... eintausendneunhundert...
        grune_haus_01_f000003|Es ist nicht etwa grün angestrichen wie ein Gartenzaun...
        grune_haus_01_f000004|die Menschen verstehen noch immer nicht die Farben so...
        grune_haus_01_f000005|Dann wachsen die Haselsträucher und die Kletterrosen so...
        grune_haus_01_f000006|und wenn der Wind kommt, weht er Laub und Blütenblätter...
        grune_haus_01_f000007|In diesem grünen Hause wohne ich mit meinen drei Kindern...
        grune_haus_01_f000008|die noch nicht in die Schule geht und ein großer Wildfang...
        grune_haus_01_f000009|Denkt nur, neulich wollte sie durchaus die Blumen von meinem...
        ...

The `.wav` -files can be found in the directory `wavs` in the same directory as where the `metadata.csv` resides.

**Note: each `.wav` -file has 0.5 seconds of silence at the beginning and at the end of it. If you don't need it, you can just remove it using [sox](http://sox.sourceforge.net/) or [ffmpeg](https://ffmpeg.org/)**

## Usage

If you have any training model that supports LJSpeech data format for preprocessing, you can just run that preprocessing tool on `metadata.csv` and life will be fine. Otherwise, you will need to do your own preprocessing.

n the original format that we provide, the files are separated as shown in the directory structure above.

But, since all `.wav` -files within a given language have  *guaranteed unique names* , you can copy them all into a single `wavs` -directory and generate the `metadata.csv` for that by using the following shell-command (Linux + macOS):

        cat <mmetadata.csv_1> <metadata.csv_2> ... >> new_metadata.csv

## Some Hints on Using the Data
It is important to know that languages evolve over time and introduce words from other languages. For example, the word "Exposé" exists in the German language and was "imported" from French. But the character "é" is not a base character of the German alphabet. It exists only for special purposes like the one shown here.

You have two options (the second being the better option):

- Leave it as is and add the character "é" to your German character-set
- Replace it by "e", which is done in the *transliterated* version of the text (second column)
    
In the first case, this can result in "not-so-good" learning as that character doesn't show up too often and your DNN might not learn well. Then again, you *may* want to separate between "e" and "é".

In the second case, this word will be learned the same as "Expose", which may not be what you want.

This is valid for all texts, including in other languages. We decided, after some discussion, to *not * remove data but instead leave it up to you to decide which information to use and which not to use. Thus, we are providing you  *both version of the text: a version including those characters and a version where those characters are transliterated * (e.g., the Turkish "ç", if it shows up in German text, is transliterated to "tsch").

For speech recognition, we usually generate multiple version of the same data in a flat-directory structure. Each additional version has noise added to it such as Cafe-backgrounds, City, Crowded Markets, Data Centers, Mega-City-Noise, Train, People Talking and more. If we add all our noise to, e.g., German, we generate usually around 2,800 hours of training data out of the existing, clean 237hrs. We recommend you experiment with similar approaches.

Since the data is used for Speech Recognition (STT) as well as Speech Synthesis, we are providing clean-audio versions here.

**Warning: in some very, very rare cases, there may be a `wav` -file missing though the filename shows up in the `metadata.csv` file. In these cases, you can just ignore the entry. We have found about six(!) cases where this happens (en_UK:2, en_US:3, es_ES:1). Bear with us, there were hundreds of thousands of files to handle...**

## Character Sets

Following character sets have been used in the data in the *transliterated, cleaned version*:

- ASCII:     `ABCDEFGHIJKLMNOPQRSTUVWYXZabcdefghijklmnopqrstuvwxyz0123456789!\',-.:;? `
- English:   ASCII
- German:    ASCII + `äöüßÄÖÜ`
- Italian:   ASCII + `àéèìíîòóùúÀÉÈÌÍÎÒÓÙÚ`
- Spanish:   ASCII + `¡¿ñáéíóúÁÉÍÓÚÑ`
- French:    ASCII + `àâæçéèêëîïôœùûüÿŸÜÛÙŒÔÏÎËÊÈÉÇÆÂÀ`
- Ukrainian: ASCII + [Image](./images/Screen-Shot-2019-01-03-at-13.46.06-.png?raw=true)
- Russian:   ASCII + [Image](./images/Screen-Shot-2019-01-03-at-13.46.14-.png?raw=true)
- Polish:    ASCII + [Image](./images/Screen-Shot-2019-01-03-at-13.46.22-.png?raw=true)

## Statistics & Download Links

<table>
    <tbody>
        <tr>
            <th>Language</th>
            <th>Country</th>
            <th>Tag</th>
            <th>Length</th>
            <th>Size</th>
            <th>DL Size</th>
            <th>Sample</th>
            <th>DL Link</th>
        </tr>
        <tr>
            <td>German</td>
            <td>Germany</td>
            <td>de_DE</td>
            <td>237h 22m</td>
            <td>27 GiB</td>
            <td>20 GiB</td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/samples/de_DE/f.wav">F</a>
                 / 
                <a href="https://data.solak.de/data/Training/stt_tts/samples/de_DE/m.wav">M</a>
            </td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/de_DE.tgz">DOWNLOAD</a>
            </td>
        </tr>
        <tr>
            <td>English</td>
            <td>Queen&#8217;s</td>
            <td>en_UK</td>
            <td>45h 34m</td>
            <td>4.9 GiB</td>
            <td>3.5 GiB</td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/samples/en_UK/f.wav">F</a>
                 / M
            </td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/en_UK.tgz">DOWNLOAD</a>
            </td>
        </tr>
        <tr>
            <td>English</td>
            <td>US</td>
            <td>en_US</td>
            <td>102h 07m</td>
            <td>11 GiB</td>
            <td>7.5 GiB</td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/samples/en_US/f.wav">F</a>
                 / 
                <a href="https://data.solak.de/data/Training/stt_tts/samples/en_US/m.wav">M</a>
            </td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/en_US.tgz">DOWNLOAD</a>
            </td>
        </tr>
        <tr>
            <td>Spanish*</td>
            <td>Spain</td>
            <td>es_ES</td>
            <td>108h 34m</td>
            <td>12 GiB</td>
            <td>8.3 GiB</td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/samples/es_ES/f.wav">F</a>
                 / 
                <a href="https://data.solak.de/data/Training/stt_tts/samples/es_ES/m.wav">M</a>
            </td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/es_ES.tgz">DOWNLOAD</a>
            </td>
        </tr>
        <tr>
            <td>Italian</td>
            <td>Italy</td>
            <td>it_IT</td>
            <td>127h 40m</td>
            <td>14 GiB</td>
            <td>9.5 GiB</td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/samples/it_IT/f.wav">F</a>
                 / 
                <a href="https://data.solak.de/data/Training/stt_tts/samples/it_IT/m.wav">M</a>
            </td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/it_IT.tgz">DOWNLOAD</a>
            </td>
        </tr>
        <tr>
            <td>Ukrainian</td>
            <td>Ukraine</td>
            <td>uk_UK</td>
            <td>87h 08m</td>
            <td>9.3 GiB</td>
            <td>6.7 GiB</td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/samples/uk_UK/f.wav">F</a>
                 / 
                <a href="https://data.solak.dedata/Training/stt_tts/samples/uk_UK/m.wav">M</a>
            </td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/uk_UK.tgz">DOWNLOAD</a>
            </td>
        </tr>
        <tr>
            <td>Russian</td>
            <td>Russia</td>
            <td>ru_RU</td>
            <td>46h 47m</td>
            <td>5.1 GiB</td>
            <td>3.6 GiB</td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/samples/ru_RU/f.wav">F</a>
                 / 
                <a href="https://data.solak.de/data/Training/stt_tts/samples/ru_RU/m.wav">M</a>
            </td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/ru_RU.tgz">DOWNLOAD</a>
            </td>
        </tr>
        <tr>
            <td>French</td>
            <td>France</td>
            <td>fr_FR</td>
            <td>190h 30m</td>
            <td>21 GiB</td>
            <td>15 GiB</td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/samples/fr_FR/f.wav">F</a>
                 / 
                <a href="https://data.solak.de/data/Training/stt_tts/samples/fr_FR/m.wav">M</a>
            </td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/fr_FR.tgz">DOWNLOAD</a>
            </td>
        </tr>
        <tr>
            <td>Polish*</td>
            <td>Poland</td>
            <td>pl_PL</td>
            <td>53h 50m</td>
            <td>5.8 GiB</td>
            <td>4.2 GiB</td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/samples/pl_PL/f.wav">F</a>
                 / 
                <a href="https://data.solak.de/data/Training/stt_tts/samples/pl_PL/m.wav">M</a>
            </td>
            <td>
                <a href="https://data.solak.de/data/Training/stt_tts/pl_PL.tgz">DOWNLOAD</a>
            </td>
        </tr>
        <tr>
            <td>TOTALS (downloadable)</td>
            <td></td>
            <td></td>
            <td>999h 32m</td>
            <td>~110 GiB</td>
            <td>~78 GiB</td>
            <td></td>
            <td></td>
        </tr>
    </tbody>
</table>

*: *I was made aware that the speaker "karen" is Mexican and the speaker "victor" is Argentinian. On one hand, I apologize for the mishap. On the other, this adds a few hours of Latin American Spanish to the collection. Please be aware of this difference.*


## License
Copyright (c) 2017-2019 by the original creators @ M-AILABS with the following license:

Redistribution and use in any form, including any commercial use, with or without modification are permitted provided that the following conditions are met:

- Redistributions of source data must retain the above copyright notice, this list of conditions and the following disclaimer.
- Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this downloaded data, source-code or binary-code without specific prior written permission.

THIS DATA IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE and/or DATA, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

## Closing Words
We hope that you will create the most interesting, fascinating and rich speech recognition and speech synthesis solutions. Please do contact us if you have developed and/or marketed something based on this data. We would be happy to hear it.</p>

If you have any questions, please feel free to contact me here or on Fediverse. 

As of October 2018, this data is provided courtesy of [Imdat Celeste](https://tau-ceti.space/@ics).

Any license restrictions you may find in downloaded data is removed herewith, only valid license (which is even more free than before) is shown above.

This repository is only a placeholder for the actual Dataset.
