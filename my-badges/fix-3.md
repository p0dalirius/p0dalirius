<img src="https://my-badges.github.io/my-badges/fix-3.png" alt="I did 3 sequential fixes." title="I did 3 sequential fixes." width="128">
<strong>I did 3 sequential fixes.</strong>
<br><br>

Commits:

- <a href="https://github.com/5250ng/5250ng/commit/30cc0edad19167a132ac128c0b854e551932d45c">30cc0ed</a>: Fix MCP HTTP parser reset() discarding pipelined/trailing bytes (#124)

McpHttpParser::reset() called m_buffer.clear() unconditionally, so any
bytes that arrived in the same TCP read past the just-parsed request
body — most commonly a pipelined second request — were silently dropped
when McpServer::onClientData() reset the parser after dispatch. The
header doc on reset() already promises 'Reset for the next request.';
the implementation contradicted it.

Make reset() drop only the consumed prefix (bodyStart + contentLength),
keeping any leftover for the next parsing cycle. Update onClientData()
to drain additional requests already in the buffer by calling feed()
in a loop after each reset(), so a pipelined batch is dispatched in
order without needing fresh readyRead activity.

Add testResetPreservesLeftoverForPipelinedRequest to exercise the
two-request-in-one-feed path.
- <a href="https://github.com/5250ng/5250ng/commit/d3bbe6321b9bd7c064c8eb5737e3b09d913380b9">d3bbe63</a>: Fix DEVNAME value in NEW_ENVIRON SB not RFC 1572 ESC-escaped (#120)

m_deviceName.toUtf8() was appended directly to the NEW_ENVIRON SB
payload, bypassing the IBMRSeed::escapeNewEnviron() call applied to
every other user-controlled value in the same function. Bytes 0x00,
0x01, 0x02, 0x03 or 0xFF inside the device name aliased RFC 1572
in-band markers and corrupted the SB framing.

Apply escapeNewEnviron to the DEVNAME value the same way it is already
applied to the IBMRSEED client seed and the IBMSUBSPW encrypted
password later in the same function.
- <a href="https://github.com/5250ng/5250ng/commit/d5e767ee44ae7b5c35c5f11fcf323c8612d1bdc8">d5e767e</a>: Fix IAC IAC inside Telnet subnegotiation routing to app data (#118)

When the Telnet parser is inside an SB...SE block, an escaped 0xFF
(IAC IAC) byte was unconditionally appended to the application data
stream instead of the subnegotiation buffer. RFC 4777 IBMRSEED server
seeds are random 8-byte values, so a 0xFF byte in the seed silently
truncated the seed and injected a stray 0xFF into the EBCDIC stream.

Route the escaped byte based on m_inSubnegotiation. Add a unit test
test_telnet_subnegotiation that exercises both inside-SB and outside-SB
paths via a friend declaration.


Created by <a href="https://github.com/my-badges/my-badges">My Badges</a>