# Audio Converter

Windows desktop application for converting between audio formats. Built in C++ using plain Win32 (no MFC), compiled with Visual C++ 6.0.

## Supported Conversions

| Input | Output |
|-------|--------|
| MP3   | WAV    |
| MP2   | WAV    |
| WMA   | WAV    |
| CDA   | WAV    |
| WAV   | MP3    |
| MP3   | MP3    |
| MP2   | MP3    |
| WMA   | MP3    |
| CDA   | MP3    |

## Requirements

- Windows XP or later
- `fmod.dll` — audio decoding and playback (FMOD 3.x)
- `lame_enc.dll` — MP3 encoding (LAME)

Both DLLs must be placed in the same directory as the executable.

## Building

Open `Converter_Audio.dsw` in **Visual C++ 6.0** and build from the IDE.

Alternatively, export a makefile from the IDE and run NMAKE:

```
NMAKE /f "Converter_Audio.mak" CFG="Converter_Audio - Win32 Release"
NMAKE /f "Converter_Audio.mak" CFG="Converter_Audio - Win32 Debug"
```

Binaries are output to `Release\` or `Debug\` respectively.

## Usage

1. Run `Converter_Audio.exe`.
2. Select the conversion type in the main window.
3. Click **Next**.
4. Choose the input file (or select the CD drive and track).
5. Choose the output file.
6. Click **Convert**.

MP3 conversions that do not start from a WAV file are handled in two internal steps: the source is first decoded to a temporary `temp.wav` in the executable's directory, then encoded to MP3 at 192 kbps. The temporary file is deleted once the conversion finishes.

Each conversion writes a text log file to the executable's directory with process details (`status_converter_to_wav.txt`, `status_cda_to_wav.txt`, `status_converter_to_mp3.txt`).

## External Dependencies

| Library        | Purpose                                                  |
|----------------|----------------------------------------------------------|
| FMOD 3.x       | Decoding MP3/MP2/WMA and reading CDA tracks              |
| LAME           | MP3 encoding (loaded dynamically at runtime)             |
| hyperlink.lib  | Hyperlink control in the About dialog                    |
| HtmlHelp       | Help system                                              |
| winmm / comctl32 | Win32 multimedia and common controls                   |
