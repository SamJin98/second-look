# Second Look · 第二眼

A second opinion on your photos, for people who do not know how to grade or crop.
给照片一个第二意见：帮新手调色和裁剪的网页。

- **Front end only / 纯前端**: one `index.html`, no backend, no model.
- **Nothing is uploaded / 不上传**: photos are processed in the browser with Canvas.
- **Rule based / 基于规则**: every fix comes from a fixed rule and has its own switch.
- 中文 / English, day / night.

## How it works

1. **Fix**: obvious faults are corrected as soon as a photo loads. Each is a switch, so turning one off shows what it did.
2. **Style**: nine looks rendered on your own photo; tap one.
3. **Crop**: suggested crops as pictures; tap one, or drag the box. Tap the photo to mark the subject.

| Fix | Rule |
|---|---|
| Brighten / Darken | median luminance outside the mid-tone range (darkening is off unless highlights are blown) |
| Clear haze | stretch the histogram ends to black and white |
| Recover highlights, Lift shadows | share of pixels near pure white or black |
| Color cast | the brightest, least colorful area should be white; corrected at 70% |
| Richer / Calmer color | mean saturation too low or too high |
| Straighten | Sobel edges and a Hough transform find a long near-horizontal line |
| Crop | the subject is the region that differs most from its surroundings; crops never cut it and keep it where it was framed |

Thresholds and looks are hand-written, not tuned on a photo set. Treat them as a starting point.

## Limits

- HEIC opens only in Safari; convert to JPEG elsewhere.
- Photos above about 16 megapixels are scaled down on save.
- Rules cannot tell which way a person is facing, so crops never push the subject to one side.

## Run

Open `index.html`, or host it as a static file. This repository deploys to Vercel on every push to `main`.
