# Videos

Drop short, looping, **muted** project clips here.

## Conventions

- Format: `mp4`, H.264, no audio (audio gets stripped on autoplay anyway).
- Size: ~360–480 px on the long side. The tiles are 180 px square on the page, so anything larger is wasted bytes.
- Length: 5–10 seconds, looping cleanly.
- Filename: kebab-case slug matching the entry (e.g. `peds-ai.mp4`, `umi-deployment.mp4`).
- Companion poster: drop a still frame as `image/<slug>-poster.jpg`. This is what shows before the video buffers, on slow connections, and in browsers that block autoplay.

## Quick re-encode recipe (ffmpeg)

```bash
ffmpeg -i raw.mov -an -vf "scale=480:-2" -c:v libx264 -crf 23 -preset slow -movflags +faststart videos/<slug>.mp4
ffmpeg -i raw.mov -ss 00:00:01 -frames:v 1 -vf "scale=480:-2" image/<slug>-poster.jpg
```

## Adding the entry to `index.html`

Inside the `Research` or `Projects` section's `<ul class="entry-list">`, add:

```html
<li class="entry">
  <div class="entry-media">
    <a href="https://your-project-page.com">
      <video class="entry-video" autoplay muted loop playsinline
             poster="image/<slug>-poster.jpg">
        <source src="videos/<slug>.mp4" type="video/mp4">
      </video>
    </a>
  </div>
  <div class="entry-body">
    <a class="entry-title" href="https://your-project-page.com">Project title</a>
    <div class="entry-authors">Authors, with <strong>Ryan Zhang</strong> bolded</div>
    <div class="entry-venue"><em>Venue or status</em>, year</div>
    <div class="entry-links">
      <a href="#">project page</a> ·
      <a href="#">arXiv</a> ·
      <a href="#">code</a>
    </div>
    <p class="entry-tldr">One-sentence summary.</p>
  </div>
</li>
```
