# Dinag Sengupta — portfolio

One static page (`index.html`). Layout modelled on nwiesner.com/work/type-7.

## Add work
Drop images into `img/<project>/` with these names (JPG):

| file      | where it shows                         | shape        |
|-----------|----------------------------------------|--------------|
| hero.jpg  | full-screen opener, home slider, thumbs | landscape    |
| 01–03.jpg | first 3-up row                          | 4:5 portrait |
| 04.jpg    | full-bleed (trailer: poster for player) | 16:9         |
| 05.jpg    | wide, small side margins                | 3:2          |
| 06–08.jpg | second 3-up row                         | 2:3 portrait |
| 09–10.jpg | side-by-side, full height               | 2:3 portrait |

Folders: `food-cinematography`, `horror`, `trailer`, `concert-photography`.
Any missing file shows a tinted placeholder.

## Edit text / trailer
Everything is in the `PROJECTS` and `ABOUT` blocks at the top of the script in `index.html`.
Paste a YouTube or Vimeo link into the trailer's `video: ""` field (or a local `.mp4` path).

## Run locally
python3 -m http.server 4317   then open http://localhost:4317

## Deploy
Upload the folder to Vercel, Netlify or GitHub Pages. No build step.

## Media
Everything the site shows lives in this repo. Nothing depends on Vercel Blob or any paid storage.
- `video/<id>.mp4`: small copy (540p vertical / 720p horizontal, with sound). Autoplays and loops.
- `video/hd/<id>.mp4`: sharper copy (720p vertical / 1080p horizontal). Opens on click or "Full screen".
- `img/<project>/posters/<id>.jpg`: still shown before a video loads.
- `img/<project>/<name>.jpg`: photos (1800px long side).
- `img/<project>/hero.jpg` and `01.jpg`: covers used on the home page, the Work list and the next-project link.

Page layouts are set in the `media` block of each project in `ALL_PROJECTS` (index.html).
`hidden: true` keeps a project (currently Trailer) off the site until it has content.

Originals stay in Google Drive / `~/Downloads/portfolio`. Never commit them: GitHub rejects files over 100 MB.

### Adding a video
  ffmpeg -i in.mp4 -vf "scale=540:-2,fps=30" -c:v libx264 -crf 27 -pix_fmt yuv420p -c:a aac -b:a 96k -movflags +faststart video/<id>.mp4
  ffmpeg -i in.mp4 -vf "scale=720:-2,fps=30" -c:v libx264 -crf 23 -pix_fmt yuv420p -c:a aac -b:a 160k -movflags +faststart video/hd/<id>.mp4
  ffmpeg -ss 5 -i in.mp4 -frames:v 1 -vf scale=720:-2 img/<project>/posters/<id>.jpg
(For horizontal video use 1280:-2 and 1920:-2.) Then add { name, kind, id } to a row, commit and push. Vercel redeploys on its own.

## Type
- Display: PP Editorial Condensed (Pangram Pangram, licensed). Put `PPEditorialCondensed-Regular.woff2` (or .woff/.otf) in `fonts/`. Newsreader shows until then.
- Body: Helvetica Neue (built into Mac/iPhone; Arial on Windows/Android).
- Scale: major third (x1.25) from a 14px body, as CSS variables `--fs--1` (11.2px) through `--fs-6` (53.4px) in `:root`.
