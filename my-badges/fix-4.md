<img src="https://my-badges.github.io/my-badges/fix-4.png" alt="I did 4 sequential fixes." title="I did 4 sequential fixes." width="128">
<strong>I did 4 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/TheManticoreProject/winacl/commit/8080f98bb0a5bb45451bab3cc6481b83232017cd">8080f98</a>: Fix NtSecurityDescriptor.Unmarshal returning inflated RawBytesSize

Components (Owner, Group, DACL, SACL) are at specific offsets within
the buffer, not laid out sequentially. Summing their sizes produced a
value larger than the actual descriptor. Now tracks the maximum extent
(offset + component size) to return the correct total size.
- <a href="https://github.com/TheManticoreProject/winacl/commit/063a9078c330aeb5db824c3e1c6df7faff71bec0">063a907</a>: Fix GUID FromFormatX incorrectly parsing D and E fields

The D field was parsed from only one byte (parts[3]) instead of two
bytes (parts[3] and parts[4]). The E field loop started at parts[3]
instead of parts[5], overlapping with D and producing an 8-byte value
instead of 6. Now correctly constructs D from 2 bytes and E from 6.
- <a href="https://github.com/TheManticoreProject/winacl/commit/6a2e612975dbe3c3e4a1cef95ee8eb6d1a380cd1">6a2e612</a>: Fix SID.Marshal dropping trailing zero sub-authorities

Marshal() was skipping trailing zero-valued sub-authorities, which
corrupts SIDs that legitimately contain zeros (e.g. domain SIDs with
zero sub-authority components). All sub-authorities are now serialized
regardless of their value.
- <a href="https://github.com/TheManticoreProject/winacl/commit/fbb01ed86cce00b67a1913ac2ebc8ad2bdc5b1ca">fbb01ed</a>: Fix SID.FromString setting wrong SubAuthorityCount for single-subauthority SIDs

When a SID had exactly one sub-authority (e.g. S-1-1-0, S-1-5-18),
SubAuthorityCount was left at 0 instead of being set to 1. The binary
SID format counts the RID as a sub-authority, so Marshal() on such a
SID would produce an incorrect binary representation with no RID bytes.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>