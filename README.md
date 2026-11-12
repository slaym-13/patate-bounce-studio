# Patate Bounce Studio

A single-file browser tool for making the short-form videos where sprites bounce
inside a rainbow ring, merge when they match, and climb to a top level. Bring your
own PNGs and your own sound effects, tune the physics, record the clip.

**[Open it](https://slaym-13.github.io/patate-bounce-studio/)** — no install, no build step, no dependencies.

## How it works

Patates fall in through the chute at the top and bounce around a circular ring.
When two of the same number touch they merge into the next number up, 25% bigger.
Everything spawns as a **1**; the top level is yours to set, from 3 up to 14.

## Making your own

| Step | Where |
| --- | --- |
| Give each level a PNG | **The patates** → `PNG` on that row |
| Give each level a sound | **The patates** → `Sound` on that row |
| Set the caption and the corner badge | **Text** |
| Choose how many levels | **Merging** → Levels |
| Record | **Record** under the stage |

Images are centre-cropped and masked to a circle by default; untick
**Crop PNGs to a circle** to keep the original shape and transparency.

### Sound rules

The audio is deliberately opinionated, because these videos live or die on it.

- **One voice.** Any patate sound cuts off whichever one is still playing.
- **Reveals are protected.** The first time a level is ever reached, its clip
  plays out in full and nothing interrupts it.
- **Big sounds hold the floor.** A lower level trying to talk over a higher one
  still playing is muted instead — 60% of the time by default, adjustable.
- **Per-level odds.** Each row has an `odds` slider. Low levels bounce and merge
  constantly, so they start lower on a curve and the top level starts at 100%.
- Level **1** fires on every wall bounce; levels **2 and up** fire when formed.
- Empty sound slots fall back to a built-in chime that rises with the level.

Nothing you upload leaves the page. Files are read with `FileReader` and decoded
in the browser; there is no server and no network call.

### Physics worth knowing

`Trampoline` makes the ring hand back a minimum inward speed on every contact, so
patates never wind down and settle at the bottom where they could not merge. Wall
contact below an impact threshold counts as a graze: it is repositioned silently
rather than firing a bounce, which is what stops a resting sprite from
machine-gunning the sound once per physics substep.

## Recording

**Record** captures the canvas plus the live audio mix via `MediaRecorder`, and
stops on its own after 90 seconds. Chrome and Firefox produce WebM, Safari MP4.
Right-click the resulting clip and choose *Save video as…*. If your platform
insists on MP4, a screen recorder aimed at the stage is the simpler path.

## Running it

Open `index.html` in a browser. That is the whole thing — one file, no build.

To host it on GitHub Pages: **Settings → Pages → Deploy from a branch → `main` / root**.

## Browser support

Needs the Web Audio API, `canvas.captureStream` and `MediaRecorder`. Current
Chrome, Edge, Firefox and Safari are all fine. Sound only starts after you click,
which is a browser rule, not a bug — press **Start** first.
