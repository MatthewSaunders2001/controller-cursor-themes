# The work behind the smooth controller setup

This is the build diary for turning a PS4 controller into a Windows desktop remote and making a set of mouse-themed cursors. It records the little adjustments because the finished experience can look deceptively simple. Dates below reflect the November 2026 working sessions. A configured control is not the same as a physical test; the status notes say which is which.

## The feel we were aiming for

- Move the pointer with the left stick; X and Circle act as left and right click.
- Scroll with the right stick, but use it to navigate Task View when R3 opens the window overview.
- Hold L1 and use the right stick to snap windows; keep ordinary scrolling when L1 is released.
- In Task View, start with a visible pointer and X as click. After moving the selection border, switch to X as Enter and hide the pointer. Moving the mouse should bring click mode back.
- Keep a separate Brave profile instead of mixing browser shortcuts into the desktop layout.
- Give Windows a distinctive mouse cursor theme without losing the meaning of text, link, waiting, and resize cursors.

## The iterations

| Step | What we changed or learned | Why it mattered |
| --- | --- | --- |
| 1. Controller foundation | Installed and started DS4Windows with the required virtual-controller driver, then confirmed the wireless PS4 controller was detected. | A mapping file alone does nothing unless the controller and virtual output are live. |
| 2. First desktop controls | Mapped left stick to pointer, X to left click, Circle to right click, right stick to the mouse wheel, and R3 to Task View. | This created the first usable couch-to-PC loop. |
| 3. Window movement | Mapped L1 with arrow controls to Windows snapping, later moved the L1 snap action to the right stick after feedback. | The physical layout needed to match how the controller felt in hand. |
| 4. Button clean-up | Tried and revised Triangle, Square, Options, touchpad, and browser-button actions. The current desktop layout uses Triangle for Escape, Square for Backspace, Options for Enter, and R1/R2 for browser-tab movement. | Some early assignments conflicted or were simply uncomfortable. The Brave browser layout remains a separate profile. |
| 5. Keyboard reality check | Tried the Windows on-screen keyboard, then targeted the sunset-themed Touch Keyboard. L2 can launch its process, but that has not reliably made the keyboard visible. | A running process was initially mistaken for a working keyboard. This remains open. |
| 6. Pointer precision | Slowed pointer movement, adjusted stick dead zones and response curves, and saved earlier profiles before further tuning. | Matthew reported twitchy movement and difficulty landing on nearby controls. The changes were judged by feel, not just by XML values. |
| 7. Cursor concepts | Created Starlight, Cosmic, Pixel, and Cyber sets, each with cursor roles for normal pointing, links, text, waiting, resizing, and more. Activated Starlight. | A cursor theme has to communicate its job at tiny screen sizes, not merely look good enlarged. |
| 8. Starlight poses | Revised the link hand, text cursor, waiting pose, and horizontal-resize pose after the first full theme looked too similar across roles. | The distinct poses are the difference between a collection of icons and a useful cursor system. |
| 9. Right-stick snapping | Tuned sideways thresholds when an upward tilt also fired left or right. An experimental extra Down Arrow action overlapped scrolling and snapping, so it was removed from the working setup. | Diagonal stick input can create two Windows shortcuts when the user intended one. |
| 10. Corner experiments | Tried one-shot directions to stop a held stick cycling through positions, then returned to the steadier direction mapping when corners still felt one step behind. | Windows snap commands are relative to the window's current position; timing and order matter. |
| 11. Anti-snapback | Enabled the right-stick anti-snapback filter after heavy flicks sometimes registered the opposite direction on rebound. | Matthew reported snapping felt much better afterward. Bottom corners can still minimise a window if Down reaches Windows before Left or Right. Moving sideways first, then down, is the reliable technique. |
| 12. Task View detection | Identified Task View as an Explorer window with the title `Task View`, then added an automatic DS4Windows profile for it. | Right-stick navigation and ordinary scrolling needed to switch by context. Matthew confirmed both worked. |
| 13. Task View selection | Mapped right-stick directions to arrow keys and X to Enter in the navigation profile. | This selects the highlighted window, but it removed the instinctive mouse-click option on entry. |
| 14. Mouse-first Task View | Added a Task View Mouse profile where X clicks, plus a local helper that changes to navigation mode after an arrow input and back to mouse mode after pointer movement. | Matthew can use either the pointer or the selection border without deciding in advance. The helper restores the pointer on exit and has a watchdog for an unexpected stop. |
| 15. Cursor hide fault | The first hide attempt failed on an obsolete Windows cursor ID and immediately reloaded the saved cursor scheme. Removing that ID made hide and restore register successfully in the local status log. | Even a tiny visual detail needs a recovery path; an invisible pointer left behind would be a terrible surprise. |

### The actual tuning checkpoints

The saved Desktop Mouse snapshots show how small the input changes were. The first snapshot used left/right stick dead zones of **12/10**, mouse sensitivity **25**, and linear response. The later smoothing snapshot used **18/18**, sensitivity **16**, and enhanced-precision response. Snap tuning then set the right stick's axial dead zones to **52 horizontal / 26 vertical**. The current local profile retains those values and adds right-stick anti-snapback. These are local profile settings, not universal recommendations for every controller.

## Current evidence and remaining checks

- **Confirmed by Matthew:** the controller can navigate Task View and return to normal scrolling; the anti-snapback adjustment made snapping feel much better; the remaining corner issue is manageable with a sideways-then-down movement; the new Task View navigation updates work.
- **Confirmed in local logs:** Task View opens in mouse mode, arrow input requests the navigation profile, mouse movement requests the mouse profile, and the saved cursor scheme is restored on exit. DS4Windows also logged the profile switches.
- **Visual test found two remaining faults:** although Windows accepted the pointer-hide call, Matthew still sees the mouse in Task View after right-stick navigation. Navigation can reach the desktop thumbnails at the bottom but cannot reliably go back up with the right stick. These are being investigated; the success log alone is not proof of a working visual result.
- **Still needs a full button check:** X should click a thumbnail before right-stick navigation, then select the highlighted window after navigation.
- **Still open:** the L2 sunset Touch Keyboard does not reliably appear. Corner snapping still depends on movement order. The Task View helper is running locally but is not yet set to start automatically after reboot.

## Where the work lives

The repository contains the public controller profiles and four cursor sets. The active DS4Windows profiles, Task View mode helper, status log, backups, and current Starlight cursor scheme are local working files. The helper and newer live settings have not been packaged as a portable public release yet; this diary records the work without publishing personal machine paths or device identifiers.

The point of this log is simple: when the controller feels effortless, that is the result of all these small choices, tests, reversals, and honest “still broken” notes. Smooth took work. 🎮🐭
