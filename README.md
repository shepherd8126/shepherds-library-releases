# Shepherd's Library - releases

Download the latest installer from [Releases](../../releases/latest).

This repository holds **release assets only**. The source is at
[shepherds-library-windows](https://github.com/shepherd8126/shepherds-library-windows).

## Install

Windows 10 version 1809 or newer, 64-bit. Setup installs per-user with no admin prompt and
checks for the Microsoft Edge WebView2 runtime, which is built into Windows 11.

The installer is not code-signed, so SmartScreen warns the first time you run it:
**More info**, then **Run anyway**.

## Updates

The app checks this feed on launch and every six hours:

```
https://github.com/shepherd8126/shepherds-library-releases/releases/latest/download/latest.json
```

When a newer version exists it offers it in a banner. Pressing **Update now** downloads the
installer, verifies its SHA-256 against the digest published in `latest.json`, and installs
over the running app.

**This repository has to stay public.** The updater fetches `latest.json` with no
authentication; a private repo makes every installed copy silently stop seeing updates.

## The feed

```json
{
  "version": "0.2.0",
  "notes": "Short summary of what changed.",
  "windows": {
    "url": "https://github.com/shepherd8126/shepherds-library-releases/releases/download/v0.2.0/Shepherds-Library-Setup.exe",
    "sha256": "3f2a..."
  }
}
```

`sha256` is the check. A feed that omits it still installs, so an omission is silent: the app
would download an executable and run it with nothing but HTTPS behind it. Do not omit it, and
never replace a published asset in place - cut a patch version instead.

Full procedure: `docs/RELEASING.md` in the source repo.

## Your data

Everything the app remembers lives in `%APPDATA%\Shepherds Library`, never beside the program,
so an update or a reinstall cannot lose it. Your book files are never moved, renamed or
modified.
