# Nerd Voice — Updates

This repository is the update channel for the **Nerd Voice** desktop app.
It contains no source code — only release installers and a signed manifest.

## How it works

`manifest.json` on the `main` branch describes the current release:

```json
{
  "version": "1.3.0",
  "url": "https://github.com/javeshkhan0/nerd-voice-updates/releases/download/v1.3.0/NerdVoice_Setup.exe",
  "sha256": "<installer hash>",
  "size": 49733771,
  "notes": "What changed in this release",
  "signature": "<Ed25519 signature>"
}
```

The app checks this file, verifies the Ed25519 signature against a public key
built into the app, downloads the installer, and refuses to run it unless its
SHA-256 matches the signed value.

Because the signing key is never published, nobody else can publish an update
that the app will accept — even with write access to this repository.

## Publishing a release

From the private source repo:

```
python scripts/sign_release.py <VERSION> dist_final/NerdVoice_Setup.exe --notes "..."
gh release create v<VERSION> dist_final/NerdVoice_Setup.exe --repo javeshkhan0/nerd-voice-updates
```

Then commit the generated `manifest.json` here.

## Installing manually

Grab `NerdVoice_Setup.exe` from the [latest release](../../releases/latest).
