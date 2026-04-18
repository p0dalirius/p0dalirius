<img src="https://my-badges.github.io/my-badges/fix-2.png" alt="I did 2 sequential fixes." title="I did 2 sequential fixes." width="128">
<strong>I did 2 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/5250ng/5250ng/commit/56088052126e777eeed3497fbdf29970663aadc8">5608805</a>: Fix SessionConfig::fromJson accepting out-of-range numeric values (#77)

Validate port, screen dimensions, and code page against their
accepted ranges up front before mutating any SessionConfig field.
When JSON carries a value outside the valid range, fromJson returns
false without emitting changed() and without half-populating the
object. Adds CodePage::isKnownId() to validate against the
supportedCodePages set.
- <a href="https://github.com/5250ng/5250ng/commit/1473d8ea6aa84b2f81f8ffba81fc54ad24d9fd6c">1473d8e</a>: Fix GDS record length silently truncated for oversized payloads (#75)

Refuse to emit a GDS record when the computed length would overflow
the 16-bit on-the-wire field. TN5250Client::sendData and sendGDS now
compute the length in qint64, compare against 0xFFFF, and log an
error plus early-return when the record would be truncated. This
keeps the 5250 stream in frame and surfaces the protocol violation
instead of corrupting the server's parser state.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>