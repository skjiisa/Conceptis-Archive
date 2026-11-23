# Importing screenshots from iOS

The Shortcut only has to put three images in the right folder on a new branch and open a pull request.
The GitHub Action then compresses the images and writes all the Markdown on that branch (see `.github/workflows/build.yml`).
Squash-merge the PR and delete the branch, so the uncompressed originals never reach `main`'s history.

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

About a minute after the PR is opened, the Action adds a "Compress images and regenerate indexes" commit to it; check the new week's page there before merging.

## Adding a week from a computer

Copy the images into the folder with the names above, then open a pull request the same way:

```sh
git switch -c <YYYY-MM-DD> origin/main
git add <App>/<YYYY-MM-DD>
git commit -m "Add <App> <YYYY-MM-DD>"
git push -u origin <YYYY-MM-DD>
gh pr create --fill
```

Pushing straight to `main` still regenerates the Markdown, but skips compression, since compressing after the fact would leave both copies in history.
