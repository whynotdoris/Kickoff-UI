# Contributing to Kickoff UI

Thanks for wanting to help! Here's how to get involved.

## Found a problem or have an idea?

Open an issue and tell us:

- What you were trying to do
- What happened (screenshots help a lot)
- What you expected instead

Ideas for new tokens are welcome too. The most useful ones come from real moments where you reached for a token and it wasn't there, so describe that moment.

## Making a change

1. Fork the repo and create a branch.
2. Edit the token data in `plugin/code.js`. That file is the single source of truth.
3. Run `node scripts/build.js` to regenerate `tokens/` and `css/`.
4. Test the plugin in Figma (see "Running the plugin locally" in the README). Try it on a fresh file and on a file that already has an older version.
5. Open a pull request explaining what changed and why.

## Guidelines

- **Follow the naming pattern.** Semantic colors are `property / color family / variant`, all lowercase. No numbered names like "primary 2". If something is a stronger version, call it `strong`.
- **Keep contrast passing.** Text tokens need 4.5:1 on the surfaces they're meant for, in both light and dark mode. Icons and input borders need 3:1.
- **Every semantic token gets a description** saying when to use it.
- **Don't break existing names** without a good reason. People's designs are linked to them. If a rename is needed, add it to the rename list in the plugin so existing files update cleanly.
- **Use plain language** in descriptions and docs. Write like you're explaining it to a designer friend.
