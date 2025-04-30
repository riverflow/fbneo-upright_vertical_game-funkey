Patch Description: fbneo-rotate90.patch
Title:
Add software-based 90-degree rotation for vertical games in libretro core (RG NANO, funkey-S)

Description:
This patch adds software-side 90-degree counter-clockwise rotation support to the FinalBurn Neo libretro core.
When a game is flagged with BDF_ORIENTATION_VERTICAL, the framebuffer is manually rotated and passed to the frontend via video_cb().

Key Changes:

Adds a new function RotateBuffer90_16bit() to libretro.cpp

In retro_run(), detects vertical games and rotates pBurnDraw into a static buffer

Sends the rotated buffer to the frontend, resulting in correct portrait orientation on devices like RG Nano

Test Environment:

Device: Anbernic RG Nano

Frontend: picoarch (SDL 1.2-based RetroArch fork)

Game tested: gunbird.zip (Psikyo vertical shooter)

Pixel format: 16bpp (RGB565 / XRGB1555)

Limitations:

Only supports 16-bit framebuffer formats

No effect on non-vertical (horizontal) games

Uses a statically-allocated rotate_buffer (up to 384×384 resolution supported)

