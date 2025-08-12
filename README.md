# Voice Cloning Scripts for Mirako CLI

This repository contains voice recording scripts designed for use with [Mirako CLI](https://github.com/mirako-ai/mirako-cli) - a command-line tool for creating AI avatars with custom voice cloning capabilities.

## Overview

These scripts provide carefully curated text content for recording high-quality voice samples needed to create custom voice profiles using Mirako's voice cloning technology. Each script is optimized for capturing the phonetic diversity and emotional range necessary for generating realistic AI voice clones.

## Prerequisites

Before using these scripts, ensure you have:

1. **Mirako CLI installed** - Follow the [installation guide](https://github.com/mirako-ai/mirako-cli#installation)
2. **Valid API token** - Obtain from [Mirako Developer Console](https://developer.mirako.ai/)
3. **Audio recording setup** - Quality microphone and quiet recording environment
4. **Audio editing software** - For cleaning and processing recordings (optional but recommended)

## Quick Start

### 1. Install Mirako CLI

Follow the installation instructions in the [Mirako CLI repository](https://github.com/mirako-ai/mirako-cli).

### 2. Configure Authentication

```bash
# Interactive setup
mirako auth login

# Or set environment variable
export MIRAKO_API_TOKEN="your-api-token-here"
```

### 3. Record Voice Samples

1. **Create organized folder structure** (see [Folder Organization](#folder-organization))
2. **Choose your script** from the available options
3. **Record each script** in a quiet environment
4. **Clean audio** using denoising tools (recommended)
5. **Organize files** according to the naming convention

## Available Scripts

This repository includes the following voice recording scripts:

- **cantonese_40.txt** - 40 Cantonese sentences for basic phonetic coverage
- **cantonese_mixed_100.txt** - 100 mixed Cantonese and English phrases and sentences
- **cantonese_word_100.txt** - 100 individual Cantonese words
- **english_generic_100.txt** - 100 English sentences covering general topics
- **english_smalltalk_140.txt** - 140 English small talk and conversational phrases
- **mandarin_150_v2.txt** - 150 Mandarin Chinese sentences for comprehensive coverage

## Recording Guidelines

### Audio Quality Standards

- **Format**: WAV (16-bit, 44.1kHz minimum)
- **Bit depth**: 16-bit or 24-bit
- **Sample rate**: 44.1kHz or 48kHz
- **Channels**: Mono
- **Duration**: 2-10 seconds per sample
- **Total samples**: 50-150 samples recommended per language

### Recording Environment

- **Quiet space** with minimal background noise
- **Consistent distance** from microphone (6-12 inches)
- **Pop filter** or foam cover to reduce plosives
- **Consistent volume** throughout recording
- **Same microphone** for all samples

### Performance Tips

- **Natural delivery** - speak as you normally would
- **Consistent pace** - avoid rushing or dragging
- **Clear articulation** - but maintain natural speech patterns
- **Accuracy** - Make sure you speak the text exactly as in the annotation file.
- **Language consistency** - complete one language before switching

## Using Mirako CLI for Voice Cloning

### 1. Prepare Your Samples

Ensure all audio files are:
- Properly named and organized
- Cleaned and denoised
- In the correct format (WAV)

### 2. Create Annotation File

The `annotation.list` file uses a pipe-delimited format to map audio files to their corresponding text and language. Each line follows this structure:

```
audio_filename|language_code|text_content
```

**Example entries:**
```
audio_samples_100.wav|yue|我嗰個smart home system真係好方便。
audio_samples_101.wav|yue|嗰個cafe嘅brunch menu好吸引。
audio_samples_102.wav|en|London bridge is falling down.
audio_samples_103.wav|en|Hi there! Welcome to mirako.
audio_samples_104.wav|zh|寻求将能源转化为智能的最优解。
audio_samples_105.wav|zh|但是它本身是不支持访问网络、数据库等外部资源，也不支持执行任何代码。
```

**Format specifications:**
- **audio_filename**: Name of the audio file (without path)
- **language_code**: Language identifier (`yue` for Cantonese, `en` for English, `zh` for Mandarin)
- **text_content**: The exact text spoken in the audio file
- **Delimiter**: Pipe character `|` separates the three components
- **Empty lines**: Allowed and will be ignored during processing

### 3. Organize your audio samples

Create the following directory structure for optimal voice sample management:

```
some-voice-sample-project/
├── audio-samples/
│   ├── cantonese_50_101.wav
│   ├── cantonese_50_102.wav
│   └── english_generic_101.wav
└── annotation.list              # The annotation file 
```

### 4. Clone Your Voice

Here's an example to perform voice cloning process using the Mirako CLI:

```bash
mirako voice clone \
  --name "My Multilingual Voice" \
  --annotations annotations.list \
  --audio-dir audio_samples/
```


#### Denoise pre-processing option (Experimental)

You can also use the `--clean_data` flag to let the voice clone service to perform de-noise operations on the audio files. This is useful if you have a worse quality audio samples (e.g. noisy, high reverb environment) and you don't have the tools to clean them up. However, this may not always yield the best results, so use it with caution. The best practice is to record in a quiet environment with low noise and reverberation.


```bash
mirako voice clone \
  --name "My Multilingual Voice" \
  --annotations annotations/voice_profile.yml \
  --audio-dir recordings/final/ \
  --clean_data

```

### 4. Use Your Custom Voice

```bash
# List your voice profiles
mirako voice list

# Use in text-to-speech
mirako speech tts \
  --text "Hello, this is my custom voice!" \
  --voice [your-voice-profile-id] \
  --output hello_custom.wav

# Use in interactive session
mirako interactive start \
  --avatar [avatar-id] \
  --voice [your-voice-profile-id]
```

## Troubleshooting

### Common Issues

**Audio Quality Problems**
- Use denoising tools before processing
- Ensure consistent recording environment
- Record multiple takes for selection

**Voice Cloning Failures**
- Verify audio format compatibility
- Check annotation file syntax
- Ensure sufficient sample variety per language

**API Authentication**
- Verify API token validity
- Check network connectivity
- Ensure proper configuration

## Best Practices

1. **Sample Diversity**: Include varied content types across all languages
2. **Quality over Quantity**: Better to have 50 high-quality samples than 200 poor ones
3. **Consistent Setup**: Use same microphone, position, and environment
4. **Language Separation**: Organize recordings by language for easier processing
5. **Regular Testing**: Test voice quality throughout the recording process


## Additional Resources

- **Mirako CLI Documentation**: [GitHub Repository](https://github.com/mirako-ai/mirako-cli)
- **API Documentation**: [docs.mirako.ai](https://docs.mirako.ai/)
- **Web Console**: [mirako.ai](https://mirako.ai/)
- **Voice Cloning Guide**: Available in Mirako documentation

## Support

For issues with:
- **These scripts**: Open an issue in this repository
- **Mirako CLI**: Visit [mirako-ai/mirako-cli](https://github.com/mirako-ai/mirako-cli)
- **General support**: Contact Mirako Discord channel or shoot us an email.

## License

This script repository is provided under the MIT License. See LICENSE file for details.

The Mirako CLI is a separate product maintained by Mirko AI, also under MIT License.
