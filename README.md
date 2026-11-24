# tonnycai.com

Personal academic site for Yicheng (Tonny) Cai. Plain static files, no build step.

| Path | What it is |
|---|---|
| `index.html` | The whole site: markup, CSS and JS in one file |
|  `Yicheng(Tonny) Cai-CV.pdf` | Three-page academic CV, linked from section 03 and section 07 |
| `img/t/`, `img/p/` | Photographs: `t` = grid thumbnails (560 px), `p` = viewer images (1600 px). `fNN` = film scan, `dNN` = digital |
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
sips -Z 1600 -s format jpeg -s formatOptions 70 /path/to/new.jpg --out img/p/d31.jpg
sips -Z 560 -s format jpeg -s formatOptions 62 img/p/d31.jpg --out img/t/d31.jpg
```

Name it `dNN` for a digital frame, `fNN` for a film scan, continuing the numbering
already in `img/p/` (currently f01–f56 and d01–d30).

Then add one entry to the `PHOTOS` array near the bottom of `index.html`, where
`kind` is `"film"` or `"digital"` and `w`/`h` are the pixel dimensions of the
`img/p/` file (they reserve layout space so the grid does not jump while loading).
The counts on the All / Film / Digital buttons are written into the markup, so
update those too.

## Type

Only two typefaces, both system fonts, so nothing is fetched at load time:
Times New Roman for headings and the opening paragraph, Arial for everything
else. They are set once as `--display`, `--body` and `--mono` at the top of the
stylesheet.

## DNS

Registered and resolved at Aliyun. The apex has four A records pointing at the
GitHub Pages addresses 185.199.108–111.153, and `www` is a CNAME to
`tonnycai918.github.io`. Two older TXT records (`_cf-custom-hostname`,
`_openai-site-verification`) are left over from a previous site and are unused.
