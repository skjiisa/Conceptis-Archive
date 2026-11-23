# Importing screenshots from iOS

The Shortcut only has to put three images in the right folder and push.
The GitHub Action writes all the Markdown afterwards (see `.github/workflows/build.yml`).

## What a week needs

```
<App>/<YYYY-MM-DD>/info.png       the puzzle's info screen
<App>/<YYYY-MM-DD>/puzzle.png     the unsolved grid
<App>/<YYYY-MM-DD>/complete.png   the finished picture
```

`<App>` is the app's name as it appears in the repo (`Link-a-Pix`, `Pic-a-Pix`, ...).
The date is the Friday the weekly bonus came out.
If a week needs a written note, add `notes.md` to its folder and it will be shown under the images.

## Building the Shortcut

The Working Copy actions are under "Working Copy" in the Shortcuts action list; their exact names vary a little between versions.
In each one, set the repository to this archive.

1. **Working Copy: Pull Repository.**
   The Action commits the generated Markdown after every push, so the phone's copy is always one commit behind until it pulls.
2. **Select Photos**, with Select Multiple on.
   Tap the screenshots in the order Info, Puzzle, Complete.
   If they come out of the action in a different order on your iOS version, add **Filter Files** after it, sorted by Creation Date, oldest first. That works as long as you take the screenshots in play order.
3. **Choose from Menu** with one item per app (`Link-a-Pix`, `Pic-a-Pix`, ...). In each branch, **Text** with the app name, then set the variable `App` to it after the menu.
4. **Work out the default date** (the Friday on or before the screenshot was taken):
   1. **Get Item from List**: first item of the Selected Photos.
   2. **Get Details of Images**: Date Taken.
   3. **Format Date**: Custom, format `EEE` (gives `Mon`, `Tue`, ...).
   4. **Dictionary**: `Fri: 0`, `Sat: 1`, `Sun: 2`, `Mon: 3`, `Tue: 4`, `Wed: 5`, `Thu: 6`.
      These keys assume an English device language; adjust them if the formatted day comes out differently.
   5. **Get Value for** the formatted day in the dictionary.
   6. **Adjust Date**: subtract that many days from Date Taken.
5. **Ask for Input**, type Date, default answer the adjusted date. Change it when backfilling an older week.
6. **Format Date**: Custom, format `yyyy-MM-dd`. Set the variable `Week` to it.
7. **List** with `info`, `puzzle`, `complete`, and **Repeat with Each** over the Selected Photos.
   Inside the loop:
   1. **Get Item from List**: item at Repeat Index from the `info`/`puzzle`/`complete` list.
   2. **Working Copy: Write** the Repeat Item to `App/Week/<that name>.png`, overwriting if the file exists.
8. **Working Copy: Commit Repository** with the message `Add App Week` (all changed files).
9. **Working Copy: Push Repository.**

To check it worked, open `<App>/README.md` on GitHub a minute after pushing; the new week should be at the top.

## Adding a week from a computer

Copy the images into the folder with the names above, then:

```sh
python3 scripts/build.py   # optional: the Action does this after you push
git add <App>/<YYYY-MM-DD>
git commit -m "Add <App> <YYYY-MM-DD>"
git push
```
