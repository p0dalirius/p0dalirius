<img src="https://my-badges.github.io/my-badges/fix-4.png" alt="I did 4 sequential fixes." title="I did 4 sequential fixes." width="128">
<strong>I did 4 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/p0dalirius/ZuluSCSI-firmware/commit/94963c329afa5370a52dd3857cc8e91c895a958f">94963c3</a>: Fix tagged queue messages 0x20/0x21/0x22 unconditionally rejected (#836)

process_MessageOut() in lib/SCSI2SD/src/firmware/scsi.c rejected every
SCSI tagged-queue message (SIMPLE_QUEUE_TAG 0x20, HEAD_OF_QUEUE_TAG
0x21, ORDERED_QUEUE_TAG 0x22) by sending MESSAGE_REJECT (0x07), even
though the captured AS/400 disk profiles in tree advertise CmdQue=1 in
their standard INQUIRY. Initiators that issue tagged commands by class
default -- notably the AS/400 9406-class IOA -- entered a tag/abort
retry loop and after exhausting retries posted a device-class error
(SRC 4326 3110 on a 9406-810 driving an emulated IBM 53P3239).

The minimum spec-compliant fix is small. SCSI-2 §6.6.17 / §7.5.3 (and
SPC-3 §6.5) only require the target to send a queue tag back to the
initiator at RESELECTION immediately after a DISCONNECT -- not at
command completion, and not for non-disconnecting targets. The SCSI2SD
codebase is non-disconnecting today (scsiDisconnect() / scsiReconnect()
are commented out further down in this file), so the only spec-defined
trigger for a tag echo is unreachable. Accepting the tag in MESSAGE_OUT
and continuing normally to STATUS / COMMAND_COMPLETE -- without
rejecting the message and without echoing the tag at completion --
satisfies the protocol for compliant initiators.

Changes:

  * Add MSG_SIMPLE_QUEUE_TAG / MSG_HEAD_OF_QUEUE_TAG /
    MSG_ORDERED_QUEUE_TAG to the SCSI_MESSAGE enum so the message
    handler can name them in source.
  * In process_MessageOut(), accept these three messages instead of
    rejecting. Read and discard the tag byte. The 0x23 (Ignore Wide
    Residue) and unknown 0x24-0x2F branches are unchanged.
  * The tag value is intentionally not stored; the only consumer would
    be a reselection echo, which is unreachable today. A header-block
    comment in scsi.c points future maintainers at the right place to
    add storage if/when this firmware gains DISCONNECT/RESELECT
    support.

Untagged hosts are unaffected -- the 0x20-0x2F branch only fires when
the initiator issues one of the tagged-queue messages.

Closes #836.
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