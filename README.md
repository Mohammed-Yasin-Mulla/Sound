# SystemAudioDump

**⚠️ IMPORTANT: This tool captures SYSTEM AUDIO only (apps, browser, media players, etc.) and does NOT record from external sources like microphones, external audio interfaces, or USB devices.**

A macOS command-line tool that captures system audio and outputs it as raw PCM data to stdout.

## Features

- Captures all system audio (excluding the current process)
- Converts audio to 24kHz, 16-bit PCM format
- Real-time streaming to stdout
- Automatic permission handling

## Requirements

- macOS 13.0+ (for ScreenCaptureKit support)
- Xcode with Swift 5.7+
- Screen Recording permissions

## Building

```bash
swift build -c release
```

## Usage

Run the executable:
```bash
./.build/release/SystemAudioDump
```

The tool will:
1. Check for screen recording permissions (required for system audio capture)
2. Prompt you to grant permissions if needed
3. Start capturing system audio and output raw PCM data to stdout

### Redirecting Audio Output

Pipe the output to a file or another program:
```bash
# Save to raw PCM file
./.build/release/SystemAudioDump > audio.pcm

# Play through ffplay
./.build/release/SystemAudioDump | ffplay -f s16le -ar 24000 -ac 2 -
```

## Permissions

When first run, macOS will prompt for Screen Recording permission. This is required because system audio capture uses the same privacy framework as screen recording.

Go to: **System Preferences > Security & Privacy > Privacy > Screen Recording** and enable access for your terminal or the application.

## Output Format

- Sample Rate: 24kHz
- Bit Depth: 16-bit signed integers
- Channels: Stereo (2 channels)
- Format: Interleaved PCM, little-endian

## Stopping

Press `Ctrl+C` to stop the capture and exit gracefully. 