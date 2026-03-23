<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/5250ng/5250ng/commit/850d069fe62349c202a6254884a17980f2c53c03">850d069</a>: Fixed #28
- <a href="https://github.com/5250ng/5250ng/commit/1f0279ae6e7f90475ca3ec1fff0b2294b8781fb3">1f0279a</a>: Fix hex color format in built-in theme JSON files (#RRGGBBAA → #AARRGGBB)

All 8-digit hex color values in the hand-written theme JSON files
used #RRGGBBAA format (alpha last), but Qt's QColor(string) parser
expects #AARRGGBB format (alpha first). This caused the alpha and
red channels to be swapped.

Most visibly, fieldIndicatorColor values like "#0080ff40" (intended
as blue at 25% alpha) were parsed with alpha=0x00, making the
"Show input fields" overlay completely transparent/invisible.

Selection background colors were also affected — e.g. "#ffff0040"
was parsed as fully opaque instead of 25% alpha.

Converted all 22 affected color values across 13 theme files.
Skipped cellGridColor entries which were already in correct format.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>