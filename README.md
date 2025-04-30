<h2>📌 Patch Description: <code>fbneo-rotate90.patch</code></h2>

<h3>Title:</h3>
<p><code>Add software-based 90-degree rotation for vertical games in libretro core</code></p>

<h3>Description:</h3>
<p>
  This patch adds software-side 90-degree <strong>counter-clockwise rotation</strong> support to the FinalBurn Neo libretro core.
  When a game is flagged with <code>BDF_ORIENTATION_VERTICAL</code>, the framebuffer is manually rotated and passed to the frontend via <code>video_cb()</code>.
</p>

<h3>Key Changes:</h3>
<ul>
  <li>Introduces a new function <code>RotateBuffer90_16bit()</code> in <code>libretro.cpp</code></li>
  <li>Within <code>retro_run()</code>, vertical games are detected and the framebuffer is rotated into a static buffer</li>
  <li>The rotated buffer is submitted via <code>video_cb()</code> for correct portrait display</li>
</ul>

<h3>Test Environment:</h3>
<ul>
  <li><strong>Device:</strong> Anbernic RG Nano</li>
  <li><strong>Frontend:</strong> <code>picoarch</code> (SDL 1.2-based RetroArch fork)</li>
  <li><strong>Tested Game:</strong> <code>gunbird.zip</code> (Psikyo vertical shooter)</li>
  <li><strong>Pixel Format:</strong> 16bpp (RGB565 / XRGB1555)</li>
</ul>

<h3>Limitations:</h3>
<ul>
  <li>Only supports 16-bit framebuffer formats</li>
  <li>Horizontal games are unaffected</li>
  <li>Uses a statically allocated <code>rotate_buffer</code> (up to 384×384 resolution)</li>
</ul>
