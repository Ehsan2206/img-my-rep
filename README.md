# FarsiDub Android

This public repository has been repurposed for FarsiDub 0.2.1 on the user's request. The original placeholder README has been replaced.

- Source build bundle: `farsidub/source.tar.xz.b64` (base64-encoded XZ tar, excluding large HPLT translation weights).
- Build workflow: `.github/workflows/build-farsidub.yml`.
- Build: **Actions > Build FarsiDub 0.2.1 APK > Run workflow** (or push).
- Output: Actions artifact `FarsiDub-0.2.1-arm64-debug-apk`.

The workflow obtains the sherpa-onnx runtime, Whisper tiny English speech recognition, Persian Piper Amir voice, and Silero VAD assets from the upstream URLs in `prepare-assets.sh`. Google ML Kit translation downloads its language model when first used.

**Important:** The large preconverted HPLT MT models were intentionally not included in this public repository. HPLT translation requires those exact models. The build should not be advertised as supporting standalone HPLT translation without them. Debug builds are not production-signed and have not been tested on a physical phone.

## Local build
```bash
mkdir FarsiDub && cd FarsiDub
base64 -d ../farsidub/source.tar.xz.b64 | tar -xJ
bash prepare-assets.sh
chmod +x gradlew
./gradlew :app:assembleDebug --no-daemon
```
