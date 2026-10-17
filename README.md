# Dconfig

**Edit your server's plugin configs in a browser, and see how they will look in game before you save.**

Dconfig is a Paper plugin plus a web panel. You change any plugin's `.yml` files from a web page instead of an SSH window. MOTDs, chat formats, messages, tab lists and scoreboards are drawn the way players will see them, from your unsaved draft. Every change is backed up first, and you can give staff their own limited access.

This repository is where **bugs, feature requests and questions** about Dconfig are tracked. If something is broken or missing, [open an issue](../../issues/new/choose).

---

## Download

- **Website:** https://dconfig.in (the panel, and the plugin jar with its version and SHA-256)
- **CurseForge** and **Modrinth:** search for "Dconfig"

Current version: **1.0.0**. It needs **Paper 26.2** and **Java 25**. It is not tested on Spigot, Folia or other forks.

## What it does

- **Three editors for every file.** Tree turns the comments in a file into help text and gives each setting a proper control. Form does the same for plugins that ship a `dconfig.yml`. Raw YAML is the file itself, with plain-English error checking and one-click fixes. Save is disabled while there are errors.
- **Live previews** of MiniMessage text, `&` codes and gradients: MOTD, chat, messages, tab lists and scoreboards.
- **Colour studio:** colour wheel, gradient builder, readability check.
- **Safe saving:** the file is checked, a backup is written, then the file is replaced in one step. If someone changed it meanwhile, you are asked instead of losing their change. Earlier versions can be restored.
- **Teams and roles:** owner, manager and viewer, each limited to the plugins you choose. Passwords and tokens are masked.
- **In-game editor:** `/dconfig` opens dialog screens for plugins that ship a `dconfig.yml` schema (Java Edition).
- **No port forwarding:** the plugin connects out to the panel.

## Set up

1. Put `Dconfig.jar` in your `plugins` folder and start the server once.
2. Open https://dconfig.in, sign in, press **Link a server** and copy the key. It is shown once.
3. In `plugins/Dconfig/web.yml`, paste the key, set `url:` to the address the panel shows, and list the plugins to share:

   ```yaml
   url: "wss://dconfig.in/ws/plugin"
   key: "dcw_..."
   plugins:
     - Dcore
     - Dtab
   ```

4. Run `/dconfig web reload`.
5. The panel shows a short code. Compare it with `/dconfig web identity` and confirm it once.

`/dconfig web help` prints these steps in game or in the console.

## Commands and permission

| Command | What it does |
|---|---|
| `/dconfig` (aliases `/dcfg`, `/configui`) | Opens the in-game editor |
| `/dconfig <plugin>` | Opens one plugin's settings |
| `/dconfig reload` | Reloads Dconfig's own settings |
| `/dconfig web help` | Panel address and setup steps |
| `/dconfig web status` | Connection state and the last problem, if any |
| `/dconfig web reload` | Re-reads `web.yml` and reconnects |
| `/dconfig web identity` | This server's fingerprint, to compare with the panel |

Permission: `dconfig.admin` (default: operators).

## What leaves your server

Dconfig does nothing on the network until you paste a key into `web.yml`. After that it keeps one outgoing WebSocket open to the address in that file. There is no telemetry, no update check, no download and no code loaded from anywhere.

- Your configs are **end-to-end encrypted** between the plugin and your browser. The panel's relay only forwards ciphertext, so it cannot read your files.
- The panel is told the server key, the plugin's public identity key, the Dconfig and game versions, and who is signed in with which role. Like any web service it also sees connection details such as your server's IP address.
- Only `.yml` files inside the plugin folders you list in `web.yml` can be opened, never data folders, and never Dconfig's own key or identity file.
- To turn it off, empty the `key:` line in `web.yml`.

## Reporting a problem

Please use the **Bug report** form. A good report lets me reproduce the problem without guessing. It needs:

1. **Dconfig version:** the output of `/version Dconfig`.
2. **Server:** the output of `/version`, and your Java version.
3. **What you did, what you expected, what happened.** Numbered steps are best.
4. **For connection problems:** the output of `/dconfig web status`, and the lines from the server log that mention Dconfig.
5. **For panel problems:** your browser and its version, and a screenshot if it is visual.
6. **For a file that saved wrongly:** the plugin and file name, and the lines that changed (a "before" and "after" is enough, not the whole file).

> **Never post your key.** Do not paste `plugins/Dconfig/web.yml`, `identity.key`, or any line starting with `key:` or `dcw_`. Remove passwords, tokens and database URLs from logs and configs too. The fingerprint code from `/dconfig web identity` is safe to share.

Before you open a new one, search the existing issues: your problem may already be reported. Add details there instead of opening a duplicate.

### Feature requests

Use the **Feature request** form. Describe the problem you are trying to solve first, then your idea. Requests that say what you were doing and why it was hard are much easier to act on than "add X".

### Security problems

Do **not** open a public issue for a security problem (for example, a way to read another server's files, or to bypass roles). Use **Security → Report a vulnerability** on this repository's page to tell me privately.

### What to expect

I read every issue. There is no guaranteed reply time. Issues are labelled `bug`, `enhancement`, `question` or `needs info`; an issue with `needs info` that gets no answer for 30 days may be closed, and you can reopen it with the details.

## Supported versions

Only the **latest release** is supported. If you are on an older one, update first and check whether the problem is still there.

## Made with AI help

Dconfig was designed and directed by its author, with a large part of the code written with the help of an AI assistant (Claude by Anthropic), then tested and reviewed on a live server.

<!-- Add your license here once you have chosen it. -->
