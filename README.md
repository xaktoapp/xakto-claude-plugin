# Xakto for Claude Code

[Xakto](https://xakto.app) is a Chrome extension for inspecting and editing a live
page, the way you would in Figma. This plugin connects it to Claude Code: edit
the page in Xakto, then tell Claude **Apply my Xakto edits** and it writes them
into your code.

It adds:

- **Xakto's tools**, through its relay, `xakto-mcp`: Claude reads your edits,
  the selected element, the page's design system, the Check's findings, your
  notes and a screenshot, finds elements by description, and tries changes on
  the page you can undo.
- **A skill, Apply my Xakto edits**: Claude reads your edits, writes them in
  the source, and marks them written, so Xakto lists them under In the code.

## What you need

- Xakto in Chrome. On Free, Claude collects your edits three times a month;
  every other tool is Pro.
- Node 20 or later, which runs the relay.

## Install

In Claude Code:

```
/plugin marketplace add xaktoapp/xakto-claude-plugin
/plugin install xakto@xakto
```

It asks for your pairing key: in Chrome, open Xakto's menu › Coding agent and
press **Copy key**. Then start a new session.

Already set Xakto up with `npx -y xakto-mcp setup`? Then Claude Code has
Xakto's tools twice. Keep the plugin and remove the old entry:

```
claude mcp remove xakto --scope user
```

Xakto in more than one browser or Chrome profile? Each makes its own key. In
the others, under **Different key**, paste this key and press **Use key**:
Claude then follows the browser you use Xakto in.

## Use it

- Edit a page in Xakto, open **Changes**, and choose **Copy to agent**. Paste
  it here and press Enter.
- Or ask for a change to the page. Claude asks whether you want it in the
  browser, in the code, or both.

Things to ask Claude:

- "Apply my Xakto edits."
- "What's selected in Xakto? Give the card in my code the same spacing and
  colours."
- "Check this page in Xakto and fix the contrast findings in my code."
- "Read the page's design system from Xakto and write it to DESIGN.md."

## What it runs

The plugin runs Xakto's relay, `xakto-mcp` from npm, at one fixed version,
with Node. The relay listens on your own computer only (127.0.0.1, port
47821) and answers Xakto in your browser once it proves the same pairing key.
The relay itself sends nothing anywhere else. When Claude asks for a page
element as a React component, the relay writes it to a temporary folder,
`xakto-clones`, and gives Claude its path.

More in the [Coding agents docs](https://xakto.app/docs-agents.html). Xakto's
[Privacy Policy](https://xakto.app/privacy) and [Terms](https://xakto.app/terms)
apply. The plugin is proprietary: see [LICENSE](LICENSE).
