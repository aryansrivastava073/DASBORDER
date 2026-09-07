# DAS Border Sensing Simulator — deploy notes

Static site, no build step, no server code. Version 2.1.

## Folder contents

```
index.html                 the whole application
vendor/three.min.js        three.js r128, vendored so the page has no network dependency
vendor/three-LICENSE.txt   MIT licence for the above, keep it alongside
favicon.svg                browser icon
preview.png                Open Graph card used when the link is shared
DEPLOY.md                  this file
```

Keep the folder structure as it is. `index.html` loads `vendor/three.min.js`
by relative path, so moving or renaming the `vendor` folder breaks the page —
though it now fails with a readable message rather than a blank screen.

## Deploying

**Vercel Drop.** Go to vercel.com/drop, drag this whole folder in, press Deploy.
Nothing else to configure.

**Vercel via GitHub.** Push the folder to a repo and import it. Framework
Preset: Other. Leave Build Command empty and Output Directory blank.

**Vercel CLI.**
```bash
npm i -g vercel
cd site
vercel
vercel --prod
```

**Anywhere else.** GitHub Pages, Netlify, Cloudflare Pages and any plain web
server all work, because this is only static files.

## Running it locally

Opening `index.html` directly with a `file://` URL works in most browsers, but
some block local file loads. If the page reports that the 3D library did not
load, serve the folder over HTTP instead:

```bash
cd site
python3 -m http.server 8000
# then open http://localhost:8000
```

## Updating the Open Graph card

`preview.png` is what appears when the link is pasted into Slack, WhatsApp,
LinkedIn or a chat. It is 1200 x 630. Replace it with a real screenshot if you
prefer, keeping the same filename and roughly the same dimensions.

## What to check after deploying

1. The page reaches the 3D view rather than stopping on the boot screen.
2. `Sound` produces audio (browsers need the click, which the button provides).
3. `Copy link`, then open that link in a new tab: the scenario should be restored
   and the help panel should not reappear.
4. `PNG`, `Trace CSV` and `Log CSV` all download.
5. Paste the deployed URL into a chat and confirm the preview card renders.

## Keyboard reference

```
arrow keys   rotate the camera
+  -         zoom
1  2  3      oblique / overhead / along-cable presets
R            reset the camera
space        start and pause
H            open and close help
Esc          close help
```

## A note on the numbers

Every signal in this application is synthesised from a physical model. Nothing
here was recorded in the field, and the classification accuracy figures quoted
elsewhere in the project come from a separate training pipeline, not from this
page. The interface says so in the header, in the help panel, in the exported
CSV headers, on the exported PNG and on the printed page. Please leave those
markings in place.
