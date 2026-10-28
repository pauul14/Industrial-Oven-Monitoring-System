# Static observations on the recovered listing

These observations come from reading the published code on October 28, 2026. They are not CODESYS compiler diagnostics or runtime test results. Line references below refer to [src/recovered/PLC_PRG.st](../src/recovered/PLC_PRG.st). The archive preserves the listing without logic or syntax repairs.

| Observation | Evidence and implication |
| --- | --- |
| Acknowledgement reset precedes the later clear block | Lines 117–119 set AckAlarm false before lines 138–143 test it again. Under ordinary sequential execution, with no intervening external write, the later branch cannot respond to the value present at scan entry. Missing HMI/Alarm Manager settings prevent verification of alarm-table acknowledgement behavior. |
| Shutdown can clear without acknowledgement | Lines 52–54 clear AlarmShutdown below 280.0. Therefore, the PLC flag does not exclusively require acknowledgement to clear. Alarm-table retention is a separate, unrecovered configuration. |
| At-temperature logic is one-sided | Lines 87–92 contain a ±5.0 comment but only compare against Setpoint - 5.0. There is no upper bound. A temperature far above the target can still satisfy the indicator condition while the run branch is active. |
| Bypass uses the earlier indicator value | Door logic reads LedAtTemp at line 64, before it is refreshed at lines 88–92. A change in temperature or setpoint can leave bypass decisions based on the preceding scan's indicator state. |
| Unlock does not imply safe access | The run bypass can set DoorLocked false at line 65 while SafeToOpen is set false at line 70. An unlocked lamp must not be described as proof of a safe temperature. |
| Power indication can lag forced shutdown | LedPower is copied at line 38 before PowerSwitch is forced false at line 45. The indicator may retain its earlier state until the next scan. |
| Configurable limit is a warning check | Lines 130–132 set AlarmOring. The fixed shutdown comparison remains at line 43. Describing every configurable-limit crossing as a shutdown would overstate the listing. |
| Temperature units conflict | Original screenshot inputs display °F. The report calls 25.0 ambient °C. The source does not label or convert units. No physical unit has been inferred for its thresholds. |
| Simulation is scan dependent | Lines 147–156 change temperature by fixed increments per scan, without elapsed time. No task period was recovered, so heating/cooling rates per second cannot be established. |
| Ambient is not explicitly clamped | The check CurrentTemp > 25.0 precedes subtraction of 0.2. Values just above 25.0 can step slightly below it; the code does not clamp exactly to 25.0. |
| Published syntax needs compiler review | Multiple END_IF tokens lack trailing semicolons, while others include them. These were retained. A successful CODESYS build cannot be claimed from this listing. |

The report's seven test descriptions and screenshots do not resolve these discrepancies. The screenshots show a target of 500.0, whereas the published declaration initializes Setpoint to 250.0; that may reflect operator input or a different capture state, and does not establish that the text and images represent the exact same build.

A future reconstruction should first establish units and configuration, review acknowledgement and interlock behavior, compile in a documented CODESYS version, and validate scan behavior and edge conditions. Any such changes belong in a clearly labeled reconstruction rather than being substituted into the recovered source.
