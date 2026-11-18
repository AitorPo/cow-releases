# CoW: Code On Wow

Chat with Claude Code or Codex from inside World of Warcraft (Retail) through a popup window.

A small desktop app reads your prompts from a strip of pixels the addon draws on screen, runs the selected agent in a project folder you allowed, and hands the answer back through small helper addons it installs next to CoW. Nothing is typed into the game. This repository only hosts the downloads.

## Download

Get the installer for your system from the [Releases page](https://github.com/AitorPo/cow-releases/releases/latest):

- **macOS:** `CoW_<version>_aarch64.dmg` for Apple Silicon (M1 and newer). Open the dmg and drag CoW to Applications. There is no Intel Mac build for now.
- **Windows:** `CoW_<version>_x64-setup.exe` for 64-bit Windows. Run it and follow the setup steps.

### macOS from Terminal (no warning)

Files fetched by `curl` have no quarantine flag, so the app opens normally. The command picks the right build for your CPU, installs `/Applications/CoW.app` and starts it.

```bash
curl -fsSL https://raw.githubusercontent.com/AitorPo/cow-releases/main/scripts/install-macos.sh | bash
```

### If you download in the browser

The builds are not signed yet, so the system warns on first launch:

- **macOS:** "CoW cannot be opened because the developer cannot be verified". Right-click CoW in Applications, choose Open, then Open again. Or open System Settings, Privacy & Security, and click Open Anyway. If macOS says the app is damaged, run `xattr -d com.apple.quarantine /Applications/CoW.app` in Terminal and open it again.
- **Windows:** SmartScreen says "Windows protected your PC". Click More info, then Run anyway.

Each release lists a `SHA256SUMS` file to verify the downloads.

The installers include `CoW-Engine-<version>.zip` (CoW's version), CoW's guide engine for WoW Forever: a headless build of [Polestar](https://github.com/fitzforge/polestar) by the Polestar authors, modified by Code On Wow. It also includes [QuestieDB](https://github.com/Questie/QuestieDB) by the Questie authors, unchanged; both are built from their latest releases for every CoW release. The zip is in the app's resources (macOS: `CoW.app/Contents/Resources/engine/`; Windows: the `engine` folder next to `CoW.exe`) and the app installs it on WoW Forever from there; it is not a separate download. Its `LICENSE` files are inside the zip and in the installed `CoW_Engine` folder, and the patches ship in `CoW_Engine/CoW/patches/`; the build scripts are available on request from Code On Wow (open an issue at https://github.com/AitorPo/cow-releases/issues).

## Setup

1. Install and log in to at least one agent: Claude Code (`npm install -g @anthropic-ai/claude-code`) and/or Codex (`npm install -g @openai/codex`).
2. Start the CoW app. It finds your WoW folder and installs the addon. After the first install, fully quit and start WoW once. Type `/reload` in game after an app update.
3. macOS: grant Screen Recording access when asked (CoW reads the pixel strip the addon draws). Keep game sound enabled: the addon hears the app through silent sound files.
4. In the app, open Projects and add the folders the agent may work in. In game, `/cow cd <folder>` points a chat at any existing folder and adds it to that list without asking again. Agents stay read-only there unless "Allow edits" is on in Settings. Network shares and network mounts are refused. The Allow & retry button only works for the permission the app just offered in that chat.
5. In game: `/reload`, then `/cow`.

CoW runs from the menu bar (macOS) or the system tray (Windows). Closing its window keeps it running there; use the tray menu to quit.
