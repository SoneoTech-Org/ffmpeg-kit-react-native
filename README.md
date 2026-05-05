# FFmpegKit for React Native (SoneoTech Fork)

## ⚠️ Licensing Notice (Important)

This is a maintained fork of the original ffmpeg-kit-react-native project by arthenica.

### Key Differences from Upstream

- This fork uses **LGPL-only FFmpeg builds**
- **GPL components (x264, x265, xvid, vid.stab, etc.) are NOT included**
- **No GPL-enabled binaries are distributed**
- This repository distributes only LGPL-compliant builds of FFmpeg
- Designed for use in proprietary and commercial applications when used in compliance with LGPL requirements

### Android

- Uses a locally built AAR:
  - `ffmpeg-kit-16kb-6.1.1-lgpl.aar`
- Built with:
  - `--disable-gpl`
  - `--disable-nonfree`
- Built from source using a reproducible build process
- The binary is verified to exclude GPL and nonfree components via automated checks
- Supports modern Android requirements (including 16KB page size)

### iOS

- Uses a prebuilt XCFramework verified to be:
  - `--disable-gpl`
  - `--disable-nonfree`

---

## 📜 Compliance

This project uses FFmpeg under the terms of the GNU Lesser General Public License (LGPL).

You must:

- Provide attribution to FFmpeg
- Provide access to the corresponding FFmpeg source code (including any modifications, if applicable)

Official FFmpeg source:
https://github.com/FFmpeg/FFmpeg

FFmpeg legal information:
https://www.ffmpeg.org/legal.html

Redistribution of this software must comply with the terms of the LGPL.

---

## 🚀 Features

- Includes both **FFmpeg** and **FFprobe**
- Supports:
  - Android and iOS
  - FFmpeg v6.0 (based on upstream release)
  - Android architectures:
    - arm64-v8a
    - armeabi-v7a
    - x86
    - x86_64
  - iOS architectures:
    - arm64
    - x86_64 (simulator)
- Supports Android Storage Access Framework (SAF)
- Includes Typescript definitions
- Optimized for **audio processing and media handling**

---

## 📦 Included Libraries

This build includes only **LGPL-compatible libraries**.

Examples:

- dav1d
- fontconfig
- freetype
- fribidi
- gmp
- gnutls
- kvazaar
- lame
- libass
- libiconv
- libilbc
- libtheora
- libvorbis
- libvpx
- libwebp
- libxml2
- opencore-amr
- opus
- shine
- snappy
- soxr
- speex
- twolame
- vo-amrwbenc
- zimg

---

## ❌ Excluded Libraries (GPL)

The following libraries are **explicitly NOT included**:

- x264
- x265
- xvidcore
- vid.stab

---

## 📦 Installation

```sh
yarn add ffmpeg-kit-react-native
```

---

## ⚙️ Configuration

This fork provides a single, fixed configuration:

- LGPL-only FFmpeg build
- No optional package switching
- No GPL variants

This ensures:

- predictable builds
- legal safety
- consistent behavior across platforms

---

## 📖 Usage

### 1. Execute FFmpeg commands

```ts
import { FFmpegKit, ReturnCode } from 'ffmpeg-kit-react-native';

FFmpegKit.execute('-i file1.mp4 -c:v mpeg4 file2.mp4').then(async (session) => {
  const returnCode = await session.getReturnCode();

  if (ReturnCode.isSuccess(returnCode)) {
    // SUCCESS
  } else if (ReturnCode.isCancel(returnCode)) {
    // CANCEL
  } else {
    // ERROR
  }
});
```

### 2. Access session details

```ts
FFmpegKit.execute('-i file1.mp4 -c:v mpeg4 file2.mp4').then(async (session) => {
  const sessionId = session.getSessionId();
  const command = session.getCommand();
  const commandArguments = session.getArguments();

  const state = await session.getState();
  const returnCode = await session.getReturnCode();

  const startTime = session.getStartTime();
  const endTime = await session.getEndTime();
  const duration = await session.getDuration();

  const output = await session.getOutput();
  const failStackTrace = await session.getFailStackTrace();
  const logs = await session.getLogs();
  const statistics = await session.getStatistics();
});
```

### 3. Execute asynchronously

```ts
FFmpegKit.executeAsync(
  '-i file1.mp4 -c:v mpeg4 file2.mp4',
  (session) => {},
  (log) => {},
  (statistics) => {}
);
```

### 4. Execute FFprobe

```ts
import { FFprobeKit } from 'ffmpeg-kit-react-native';

FFprobeKit.execute('-i file.mp4').then(async (session) => {
  // handle output
});
```

### 5. Get media information

```ts
FFprobeKit.getMediaInformation(fileUrl).then(async (session) => {
  const information = await session.getMediaInformation();
});
```

### 6. Cancel operations

```ts
FFmpegKit.cancel(); // all sessions
FFmpegKit.cancel(sessionId); // specific session
```

### 7. Android SAF support

```ts
import { FFmpegKit, FFmpegKitConfig } from 'ffmpeg-kit-react-native';

FFmpegKitConfig.selectDocumentForRead('*/*').then((uri) => {
  FFmpegKitConfig.getSafParameterForRead(uri).then((safUrl) => {
    FFmpegKit.executeAsync(`-i ${safUrl} output.mp4`);
  });
});
```

### 8. Session history

```ts
FFmpegKit.listSessions().then((sessionList) => {
  sessionList.forEach(async (session) => {
    const id = session.getSessionId();
  });
});
```

### 9. Global callbacks

```ts
import { FFmpegKitConfig } from 'ffmpeg-kit-react-native';

FFmpegKitConfig.enableLogCallback((log) => {
  console.log(log.getMessage());
});

FFmpegKitConfig.enableStatisticsCallback((statistics) => {
  console.log(statistics.getSize());
});
```

### 10. Fonts

```ts
import { FFmpegKitConfig } from 'ffmpeg-kit-react-native';

FFmpegKitConfig.setFontDirectoryList(['/system/fonts', '/System/Library/Fonts']);
```

---

## 🧪 Test Application

See upstream example usage:

https://github.com/arthenica/ffmpeg-kit-test

---

## ⚠️ Notes

- This fork is intended for use in commercial applications under LGPL-compliant conditions
- No GPL components are included
- If you require GPL codecs (e.g. x264), you must build your own version

---

## Disclaimer

This project is not affiliated with or endorsed by the FFmpeg project.

This repository provides a custom build configuration of FFmpeg for React Native usage.

Users are responsible for ensuring compliance with all applicable licenses and regulations when using this software.

This software is provided "as is", without warranty of any kind, express or implied.

---

## 📄 License

This project uses FFmpeg licensed under the GNU Lesser General Public License (LGPL).

FFmpeg source:
https://github.com/FFmpeg/FFmpeg

Legal details:
https://www.ffmpeg.org/legal.html
