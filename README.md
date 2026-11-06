# Controller desktop layouts and mouse cursors

Two experimental DS4Windows profiles and four mouse-inspired Windows cursor sets: Starlight, Cosmic, Pixel and Cyber.

The small adjustments, failed experiments, physical tests, and remaining issues are recorded in [the build diary](BUILD_DIARY.md).

## Controller profiles

Import a profile in DS4Windows. Desktop Mouse maps the left stick to the mouse and right stick to scrolling; L1 plus right stick is intended for Windows window snapping. Brave Controller is a separate browser-oriented layout. These are personal experimental mappings, not a guaranteed compatible setup for every controller or Windows version.

The Desktop Mouse profile references special actions that are not included: opening the Windows touch keyboard has not been verified to work, and an experimental down-arrow action can overlap scrolling. L1 plus right-stick snapping can trigger diagonal directions and needs further tuning.

## Cursor sets

The `cursors` directory contains four sets of Windows `.cur` files. Select cursor files through Windows Mouse Properties > Pointers. Starlight has distinct experimental hand, text, wait and horizontal-resize poses in `*-pose.cur` files. Other roles use the same mouse art with small badges; the other three designs are not yet fully illustrated state-by-state themes.

The graphics were generated with OpenAI image generation and prepared for use as Windows cursor files. Some hotspots and appearances may need adjustment for individual displays.
