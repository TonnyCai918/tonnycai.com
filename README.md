# tonnycai.com

Personal academic site for Yicheng (Tonny) Cai. Plain static files, no build step.

| Path | What it is |
|---|---|
| `index.html` | The whole site: markup, CSS and JS in one file |
| `cv.pdf` | Three-page academic CV, linked from section 03 |
| `img/t/`, `img/p/` | Photographs: `t` = grid thumbnails (560 px), `p` = viewer images (1600 px) |
| `img/c/` | Bottle collection: `cNN_t.jpg` thumbnail, `cNN.jpg` full |
| `CNAME` | Tells GitHub Pages to serve this repo at tonnycai.com |
| `.nojekyll` | Skips Jekyll processing, so nothing is rewritten |

## Updating it

Edit the files, then:

```
git add -A && git commit -m "..." && git push
```

GitHub Pages rebuilds within a minute or two. Pushing uses the deploy key at
`~/.ssh/tonnycai_deploy`; the repo's `core.sshCommand` already points at it.

## Adding photographs

Each image needs two sizes. From the repo root, with the original at `/path/to/new.jpg`:

```
sips -Z 1600 -s format jpeg -s formatOptions 70 /path/to/new.jpg --out img/p/p63.jpg
sips -Z 560 -s format jpeg -s formatOptions 62 img/p/p63.jpg --out img/t/p63.jpg
```

Then add one entry to the `PHOTOS` array near the bottom of `index.html`, where
`kind` is `"film"` or `"digital"` and `w`/`h` are the pixel dimensions of the
`img/p/` file (they reserve layout space so the grid does not jump while loading).

## DNS

Registered and resolved at Aliyun. The apex has four A records pointing at the
GitHub Pages addresses 185.199.108–111.153, and `www` is a CNAME to
`tonnycai918.github.io`. Two older TXT records (`_cf-custom-hostname`,
`_openai-site-verification`) are left over from a previous site and are unused.
