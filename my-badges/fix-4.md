<img src="https://my-badges.github.io/my-badges/fix-4.png" alt="I did 4 sequential fixes." title="I did 4 sequential fixes." width="128">
<strong>I did 4 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/TheManticoreProject/winacl/commit/963a0a916e009dc289962d834ddbbda43865a4dc">963a0a9</a>: Fix SID.FromString accepting identifier authority > 48 bits (#66)

The SID binary format (MS-DTYP 2.4.2.1) stores IdentifierAuthority in
6 bytes. FromString parsed the component with ParseUint(_, 10, 64)
and assigned the result without a range check; values greater than
2^48-1 silently overflowed when marshalled, producing a SID that did
not round-trip.

Reject values that cannot fit in the 6-byte field at parse time
instead.
- <a href="https://github.com/TheManticoreProject/winacl/commit/85268f676350d64352d51f461a9bf6a260a5e66b">85268f6</a>: Fix sddl.CutSDDL silently dropping lowercase-marker components (#64)

CutSDDL recognised 'O'/'G'/'D'/'S' markers case-insensitively but then
stored the original-case marker as the map key, while the components
map was created with only uppercase keys. Input with lowercase markers
(o:, g:, d:, s:) ended up writing to keys that were never read, so
every return value was empty with no error.

Normalise the stored key to uppercase so lowercase and uppercase markers
land in the same bucket, matching SDDL's case-insensitive grammar and
the existing private cutSDDL implementation in securitydescriptor.
- <a href="https://github.com/TheManticoreProject/winacl/commit/028340e393170a56d5263f10c2d3ab68e6aebf42">028340e</a>: Fix FromSDDLString silently dropping ACEs on unbalanced parens (#62)

cutAces only appended ACE content inside the `depth == 0` branch of
the ')' case, so an input ending with depth != 0 (unclosed '(') or a
stray ')' would silently discard the accumulated content. The signature
had no error channel, so FromSDDLString could not distinguish "no ACEs"
from "ACEs lost due to malformed input."

Return an error from cutAces on unbalanced parentheses, propagate it
through cutSDDL, and surface it from FromSDDLString.
- <a href="https://github.com/TheManticoreProject/winacl/commit/eb780445dfd0f2e161d421fbc1bdf15222055057">eb78044</a>: Fix SID.Marshal omitting RID when value is zero (#60)

The marshaller skipped writing the RelativeIdentifier when it was
zero, producing binaries 4 bytes shorter than the SID format requires
(8 + 4*SubAuthorityCount). This corrupts well-known SIDs such as
S-1-1-0 (Everyone), S-1-0-0 (Nobody), and S-1-3-0 (Creator Owner),
and breaks round-trip of genuine Windows binaries.

Write the RID whenever the model indicates one exists
(SubAuthorityCount > len(SubAuthorities)), regardless of its value.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>