<img src="https://my-badges.github.io/my-badges/fix-3.png" alt="I did 3 sequential fixes." title="I did 3 sequential fixes." width="128">
<strong>I did 3 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/p0dalirius/ZuluSCSI-firmware/commit/52a23422071b83e40a88a72f6147fc5ad733f0ed">52a2342</a>: Fix VPD/SPD buffer truncation losing AS/400 EC data (#834)

Bump MAX_SPD_SIZE 128 -> 192 and MAX_VPD_DATA_SIZE 128 -> 255 in
src/custom_vendor_inquiry.cpp. The previous values silently truncated
profile-driven AS/400 captures whose sizes exceed 128 bytes:

  Std INQUIRY (DGVS09U & XCPR036):  164 B captured, 128 B emitted.
                                    Hardware EC level at offsets
                                    126-131 truncated to "H6" + zeros.
                                    `additional_length` byte at offset
                                    4 still advertises 159 -- a SCSI
                                    protocol violation.

  XCPR036 page 0xC3:                250 B captured, 128 B emitted
                                    (49% of page lost, including the
                                    trailing Seagate diagnostic tables).

  XCPR036 page 0xD1, 0xD2:          244 B each captured, 128 B emitted
                                    (48% of each page lost, including
                                    half the IBM EC-tracking fields).

The new sizes are the maximum representable in the existing `uint8_t
length` field (255) with comfortable headroom for std INQUIRY (192).
No struct-layout changes, no API changes. RAM cost +2.5 KB across
all targets, comfortably within budget on every default env.

Closes #834.
- <a href="https://github.com/p0dalirius/ZuluSCSI-firmware/commit/d3cfe7067556ceafa1eb9b2334543bfebd250a8e">d3cfe70</a>: Fix AS/400 Skip Read/Write parameter handling to match IBM spec (#4)

Two related changes to scsiDiskSkip and the Skip Read execution
path, validated against IBM ESS SCSI Command Reference SC26-7297-01
pages 66-67:

1. scsiDiskSkip:
   - Reject transfer_length > 256 per spec ("The maximum transfer
     length is 256 blocks. If a larger number is specified, then
     Check Condition status is returned. The sense data is set to
     Illegal Request - Invalid Field in CDB").
   - Mask Length=0 already maps to 256 (existing behavior, kept).

2. start_dataInTransfer Skip Read branch:
   The loop exits early when skip_next returns 0, which happens
   once the mask is exhausted. Previously the code shipped the
   (possibly partially-filled) buffer to the host regardless,
   leaving stale bytes from the prior transfer in any unfilled
   sectors. Raise CHECK CONDITION / MEDIUM ERROR / UNRECOVERED
   READ ERROR if sectors_remaining > 0 after the loop, so a
   malformed skip mask cannot silently corrupt host reads.

Closes #4
- <a href="https://github.com/p0dalirius/ZuluSCSI-firmware/commit/77b203f118ce74453a5e1364dcd2f545aa765634">77b203f</a>: Fix AS400_DiskPartNumber not patched into standard INQUIRY (#808)

AS400_DiskPartNumber previously updated only VPD page 0x01. The 7-char
IBM disk part number 09L4044 is also hardcoded in AS400VendorInquiry
at offsets 114-120, and loadAS400Defaults() copied the blob into the
per-target SPD without patching it. A host that read both the standard
INQUIRY and VPD page 0x01 saw inconsistent part numbers.

Extend injectPartNumber() to accept a negative ebcdicOffset meaning
'this buffer has no EBCDIC slot, skip the EBCDIC write', then call it
from loadAS400Defaults() against the default SPD at ASCII offset 114.
The VPD-page 0x01 path is unchanged. The injection is a no-op when the
user has not configured AS400_DiskPartNumber, so the SPD retains its
baseline 09L4044 literal when no override is set.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>