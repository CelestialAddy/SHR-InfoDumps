# RadSound4Format
NOTE: This documentation does not explain how to decode any type of literal audio data.

## Description
RadSound is an audio storage (container/encoding) and integration/playback system created by Radical Entertainment as part of their general shared technologies for use in video games. 

RadSound 4 is the version used in *The Simpsons: Hit & Run*; this document will focus on the file format and application within that game solely.

## Container
The layout of a RadSound4 ".rsd" file is as follows.
All header values are little-endian.
("LEN" refers to the length of the file, in bytes.)
("d" = decimal, "h" = hexadecimal)

| Offset (d/h) | Length (d/h) | Information |
| ------------ | ------------ | ----------- |
| 0/0 | 8/8 | Encoding format identity string, in ASCII. See "Formats" - if only 7 characters long, a " " is appended. |
| 8/8 | 4/4 | Number of channels as a 32-bit integer; typically 1 (mono) or 2 (stereo). |
| 12/C | 4/4 | Bits-per-sample/bitrate as a 32-bit integer; typically 16. |
| 16/10 | 4/4 | Sample rate per-second as a 32-bit integer; typically 24000. |
| 20/14 | 108/6C | Padding block 1 - repeated 0x2A (ASCII *). |
| 128/80 | 1920/780 | Padding block 2 - repeated 0x2D (ASCII -). |
| 2048/800 | (LEN - 2048(d) bytes/header size) | Encoded audio data. |

## Formats
There are a few RadSound4 audio data encoding formats relevant to the game.

| Identity string | Information |
| --------------- | ------------ |
| `RSD4PCM ` (0x5253443450434D20) | Raw signed little-endian PCM audio data. No format-inherent compression. |
| `RSD4PCMB` (0x5253443450434D42) | Raw signed big-endian PCM audio data. No format-inherent compression. |
| `RSD4RADP` (0x5253443452414450) | A "Radical" variant of Adaptive Differencial Pulse Code Modulation. Applies format-inherent compression. |
| `RSD4GADP` (0x5253443447414450) | A "GameCube" variant of Adaptive Differencial Pulse Code Modulation. Applies format-inherent compression. |
| `RSD4VAG ` (0x5253443456414720) | PlayStation 2 SPU-optimised audio. Applies format-inherent compression. |
| `RSD4XADP` (0x5253443458414450) | Unknown, apparently possibly supported (see [**DTDocs**](https://docs.donutteam.com/docs/lucasrmsbuilder/xml-format)). |

## Audio types and data requirements in TS:H&R
Incorrect sound data specification can lead to crashes and active memory corruption.

| Type | GameCube | PlayStation 2 | Windows | Xbox | Channels | Bitrate | Sample Rate |
| ---- | -------- | ------------- | ------- | ---- | -------- | ------- | ----------- |
| Ambience | `RSD4RADP` | `RSD4VAG ` | `RSD4PCM ` | `RSD4PCM ` | 2 | 16 | 24000 |
| Vehicle Sounds | `RSD4PCMB` | `RSD4VAG ` | `RSD4PCM ` | `RSD4PCM ` | 1 | 16 | 24000 |
| Character Dialogue | `RSD4GADP` | `RSD4VAG ` | `RSD4RADP` | `RSD4PCM ` | 1 | 16 | 24000 |
| Music | `RSD4RADP` | `RSD4VAG ` | `RSD4PCM ` | `RSD4PCM ` | 2 | 16 | 24000 |
| Non Interactive Scenes | `RSD4PCMB` | `RSD4VAG ` | `RSD4PCM ` | `RSD4PCM ` | 1 | 16 | 24000 |
| Sound Effects | `RSD4PCMB` | `RSD4VAG ` | `RSD4PCM ` | `RSD4PCM ` | 1 | 16 | 24000 |

## Programs
[**ffmpeg ->**](https://ffmpeg.org/) A cross-platform command-line utility capable of decoding, playing, and exporting most if not all RSD4 encoding formats mentioned above to any supported audio export format.  
[**Lucas' RSD Converter ->**](https://modbakery.donutteam.com/releases/view/14) A Windows graphical-user-interface tool capable of decoding, playing, and exporting all RSD encoding formats mentioned above to **Wave**/".wav" files except for **RSD4GADP**, **RSD4VAG**, and possibly **RSD4XADP**; can encode/convert *to* **RSD4PCM** and **RSD4PCMB** via **Wave**/".wav" files.  
[**Audacity ->**](https://www.audacityteam.org/) A cross-platform graphical-user-interface tool capable of importing raw audio data to work with (thus **RSD4PCM**/**RSD4PCMB** audio) and export however supported with the right settings - see below.

## Settings to import RSD4PCM/B audio in Audacity via "Import Raw Data"
```
Encoding:
        "Signed 16-bit PCM"
Byte order:
        "Little-endian" (if file is RSD4PCM; see table above)
        "Big-endian" (if file is RSD4PCMB; see table above)
Channels:
        "1 Channel (Mono)" (if not storing ambience/music)
        "2 Channels (Stereo)" (if storing ambience/music)
Start offset:
        2048 bytes
Amount to import:
        100 %
Sample rate:
        24000 Hz
```

---
