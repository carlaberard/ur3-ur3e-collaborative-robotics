# Communication protocol

## Architecture

The UR3 and UR3e execute URScript programs and both connect as TCP **clients** to a **PC-hosted relay**. The course exercise assigns the UR3 a logical **server role** in the workflow, but URScript does not implement the TCP listening server here.

The relay/middleware implementation is not provided in the project files and therefore cannot be reproduced from these files alone.

## Handshake sequence

| Step | Sender | Message | Receiver/action |
| --- | --- | --- | --- |
| 1 | UR3e | `client ready` | UR3 may move to operate pose |
| 2 | UR3 | `server moved` | UR3e may pick and place block |
| 3 | UR3e | `block placed` | UR3 may perform tool-rotation operation |
| 4 | UR3 | `operated` | UR3e may return to home |

The two programs use `socket_open("PC_IP", 8080, socket_name="sock")` and message waits with a 20-second timeout. The `PC_IP` value is intentionally a placeholder, not a working address.

## Notes

- Each robot must use a configured and reachable network address for the PC relay.
- Timing and correct message forwarding depend on the **missing middleware** implementation.
- The original scripts halt on failed connections or unexpected incoming strings; they do not verify every `socket_send_string` result or attempt reconnection.
- The UR3 rotation is a tool motion intended to **simulate** operating on the placed block, not physically manipulate it.
