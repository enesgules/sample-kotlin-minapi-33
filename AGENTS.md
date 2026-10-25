# AGENTS

For testing the app, always use the `lim` CLI which provides remote Gradle builds and
remote Android Emulators.

Install `lim`:
```bash
npm install -g lim
```

Ensure `LIM_API_KEY` exists either as environment variable or in `.env` files.

## Development flow

Build the debug APK on a remote Gradle sandbox and upload it to Limrun asset storage:

```bash
lim gradle build . --upload sample-kotlin-minapi-33/app-debug.apk
```

Get an emulator from Limrun with the APK installed, then launch the app:

```bash
lim android create --install-asset sample-kotlin-minapi-33/app-debug.apk
lim android launch-app com.limrun.samplekotlin33 --detach
```
`lim android create` returns a signed stream URL that you can open in the browser, or tell
the user to open, to stream the Android screen. When `adb` is installed, it also starts an
`adb` tunnel. The `lim android` commands work without `adb`.

To install a local APK file on a running emulator instead:
```bash
lim android install-app <path to apk file>
```

For quick tests, you can use `lim android` commands like tapping, screenshots, element tree etc.

While testing, you can trigger recording of the Android screen:
```bash
lim android record start
```

Once the test is completed, you can have it written to a file you can show to user or upload:
```bash
lim android record stop -o recording.mp4
```

See what's available with `lim android --help`
