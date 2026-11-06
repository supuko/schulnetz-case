# SchulNetz Case Opening

Browser extension that hides your SchulNetz grades in CS2 crates. You open a crate, the roulette spins, and then you see your grade.

Not affiliated with SchulNetz or Valve.

## What it does

- Replaces every grade with an "Open" button
- Spins a roulette with tick sounds and lands on your real grade
- Colors the grade by rarity (6 is gold, 5.5 red, 5 pink, 4.5 purple, 4 blue, 3.5 light blue, below that grey)
- Fills the roulette with fake grades that look like yours, so you can't tell the winner by its decimals
- Remembers which crates you already opened
- Keeps the page hidden until the grades are locked, so you don't see them for a second first

## Install

It's not in any store, so you load it manually.

1. Download the repo as a zip and extract it. `manifest.json` has to be directly inside the folder you select.
2. Open `chrome://extensions` (in Edge: `edge://extensions`)
3. Turn on Developer mode
4. Click "Load unpacked" and pick the folder
5. Open your grades in SchulNetz

Works in Chrome, Edge, and Brave.

The official Firefox add-on:
https://addons.mozilla.org/en-US/firefox/addon/schulnetz-case-opening/

## Settings

Click the extension icon to turn crates or sound on and off, see how many crates you opened, or lock all grades again. Reload the SchulNetz page after changing something.

## Testing

There is a fake grades page in the repo, so you don't need to log in to SchulNetz.

Start a local server in the project folder:

```
python -m http.server 8000
```

and open `http://localhost:8000/schulnetz-mock.html`.

You can also open the file directly, but then you have to turn on "Allow access to file URLs" in the extension's details page.

You should see six crates in the Note column.

## My school doesn't work

The extension only runs on a few domains. Add yours to `matches` in `manifest.json`:

```json
"matches": [
  "*://*.schul-netz.com/*",
  "*://*.schulnetz.ch/*",
  "*://your-school.ch/*"
]
```

Then reload the extension.

If the domain is right but no crates show up, the grade detection (`findTargets()` in `content.js`) doesn't match your school's table. It looks for a table column called "Note" or "Noten". If there is none, it takes any table cell that only contains a grade like `5.5` or `4,75`. Open an issue and paste the HTML of your grades table, then I can adjust it.

## Files

- `manifest.json`: extension config and the list of sites
- `content.js`: finds the grades, builds the crates, animation, sound
- `content.css`: styling
- `popup.html`, `popup.js`, `popup.css`: the settings popup
- `schulnetz-mock.html`: fake grades page for testing

## Privacy

The extension only uses the storage permission and makes no network requests. The only thing it saves is which crates you opened, in your browser.

## Limitations

- This only hides the grades visually. They are still in the page source, so anyone who opens the dev tools can see them.
- The result is always your real grade. The animation is just for show.
- I built it without access to every school's SchulNetz layout, so it may need small changes for yours.

## License

MIT, see [LICENSE](LICENSE).
