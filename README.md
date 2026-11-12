# Second Look · 第二眼

A second opinion on your photos, for people who do not know how to grade or crop.
给照片一个第二意见：帮新手调色和裁剪的网页。

- **Front end only / 纯前端**: `index.html` plus one sample photo, no backend, no model.
- **Nothing is uploaded / 不上传**: photos are processed in the browser with Canvas.
- **Rule based / 基于规则**: every suggestion comes from a fixed rule and has its own switch.
- 中文 / English, day / night.

## How it works

A histogram sits on top of three tabs.

1. **Diagnose**: what was measured, one line on why, and a switch for each fix. Nothing changes until you ask: press Fix all, or flip the switches one at a time.
2. **Color**: nine looks rendered on your own photo, then the full set of sliders. The sliders show the total of the fixes, the look and your own changes, so picking a look shows what it is made of.
3. **Crop**: shapes, straighten, six composition guides, suggested crops as pictures, and a live score for the current framing. Tap the photo to mark the subject.

| Fix | Rule |
|---|---|
| Brighten / Darken | median luminance outside the mid-tone range (darkening is always optional: bright scenes are usually meant to be bright) |
| Clear haze | stretch the histogram ends to black and white |
| Recover highlights, Lift shadows | share of pixels near pure white or black |
| Color cast | the brightest, least colorful area should be white; corrected at 70% |
| Richer / Calmer color | mean saturation too low or too high |
| Straighten | Sobel edges and a Hough transform find a near-horizontal line; only one that crosses most of the frame is recommended |
| Crop | the subject is the region that differs most from its surroundings; crops never cut it and keep it where it was framed |

Thresholds and looks are hand-written, not tuned on a photo set. Treat them as a starting point.

## Sample photo

The page opens on Moraine Lake in Banff National Park: [Moraine Lake 17092005.jpg](https://commons.wikimedia.org/wiki/File:Moraine_Lake_17092005.jpg) by Gorgo, from Wikimedia Commons, released into the public domain by its author. The page darkens, flattens and cools it on purpose, so that there is something to fix; the original 2048×1536 file is `sample.jpg`, unmodified. Opened straight from disk the browser will not let the page read it, so the page starts empty and waits for your photos.

## Limits

- HEIC opens only in Safari; convert to JPEG elsewhere.
- On phones, photos above about 16 megapixels are scaled down on save (a browser limit). On a computer they are saved at full size.
- Rules cannot tell which way a person is facing, so crops never push the subject to one side.

## Run

Open `index.html`, or host it as a static file. This repository deploys to Vercel on every push to `main`.
