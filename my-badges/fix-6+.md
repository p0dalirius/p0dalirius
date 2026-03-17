<img src="https://my-badges.github.io/my-badges/fix-6+.png" alt="I did 7 sequential fixes." title="I did 7 sequential fixes." width="128">
<strong>I did 7 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/5250ng/5250ng/commit/f4c088ef0c548a38d7ef4b8aa8b1a674d425f1f7">f4c088e</a>: Fix potential WHILE loop index underflow in executor

The WHILE implementation decremented the parent frame index to
re-execute the WHILE node after each body iteration. If the index
was already 0 (e.g. due to a GOTO modifying execution state), this
would underflow to -1 causing incorrect execution. Add a guard.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
- <a href="https://github.com/5250ng/5250ng/commit/e6bee73fa457a6d911e825ba103d4c304ea04649">e6bee73</a>: Fix lone trailing $ in interpolateVariables() resolving to "0"

A trailing $ with no following identifier characters produced varName
"$" which resolved to "0" via the default. Now a lone $ is emitted
as a literal dollar sign instead.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
- <a href="https://github.com/5250ng/5250ng/commit/5c3ce6f0af9c28eb02ff70c8ff58a1d2ed0ac45c">5c3ce6f</a>: Fix lexer silently accepting unterminated string literals

readStringLiteral() returned STRING_LITERAL even when the closing
quote was missing, causing scripts with typos like TYPE "hello to
silently parse as if the string were properly closed. Now returns
UNKNOWN token type so the parser reports an error.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
- <a href="https://github.com/5250ng/5250ng/commit/bbc411cb78cccf2a989464d45a2a975acb0b9709">bbc411c</a>: Fix unguarded m_scriptStopAction access in executionFinished lambda

The executionFinished lambda accessed m_scriptStopAction via raw
'this' pointer while other objects in the same lambda used QPointer
guards. If MainWindow is destroyed before the lambda fires, this
is a use-after-free. Guard it with QPointer like the other members.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
- <a href="https://github.com/5250ng/5250ng/commit/b29f9d044cf399e06d8a19014b46639d34971d9e">b29f9d0</a>: Fix missing row bounds check in readScreenText()

readScreenText() validated col via the loop condition but never
checked row against buf->rows(). Out-of-bounds or negative row
values would access invalid memory in buf->character().

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
- <a href="https://github.com/5250ng/5250ng/commit/d072c7d56b6c0ccff4302894a96965cb8283d30f">d072c7d</a>: Fix missing scriptExecutor cleanup when closing a tab

When a session tab is closed, macroRecorder was stopped and
disconnected but scriptExecutor was not. A running script would
continue firing timer callbacks against destroyed widgets,
causing use-after-free crashes.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>
- <a href="https://github.com/5250ng/5250ng/commit/56d8074cbf4914709ba6875e9fb0c6c43063fad0">56d8074</a>: Fix null pointer dereference in checkExpectCondition()

screenBuffer() can return nullptr if the screen widget is destroyed
mid-execution (e.g. tab closed while script runs). The CursorAtPos
and CursorAtRow cases called screenBuffer()->cursorPosition() without
a null check, causing a crash.

Co-Authored-By: Claude Opus 4.6 (1M context) <noreply@anthropic.com>


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>