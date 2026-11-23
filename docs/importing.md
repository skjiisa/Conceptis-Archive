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

## Getting the Shortcut

An iCloud link to the Shortcut will be shared here later.

After a push, the GitHub Action takes about a minute to update the Markdown; the new week then appears at the top of `<App>/README.md`.

## Adding a week from a computer

Copy the images into the folder with the names above, then:

```sh
python3 scripts/build.py   # optional: the Action does this after you push
git add <App>/<YYYY-MM-DD>
git commit -m "Add <App> <YYYY-MM-DD>"
git push
```
