## Simple Pong

A single-player Pong game — player vs AI opponent, controlled with the mouse.

### Gameplay

- **Player 1** (left paddle): mouse up/down
- **Computer** (right paddle): AI that tracks the ball with a speed cap, making it beatable
- The ball speeds up slightly after each paddle hit
- First to 10 points wins
- Press fire/click to start and to restart after a game
- ESC to quit

### Techniques

- **Double buffered game loop** with `Screen Swap` / `Wait Vbl` for flicker-free 50 FPS
- **Selective erase** instead of `Cls` — tracks old positions per buffer and only redraws changed areas, keeping the frame budget tight on a 7 MHz 68000
- **Integer-only arithmetic** throughout — no floating point
- **Relative mouse input** via delta tracking (`Y Mouse` frame difference) for full-range paddle control
- **Simple AI**: the computer paddle tracks the ball's Y position but moves at a capped speed (`AISPD=3`), so the player can outmanoeuvre it at higher ball speeds
- **Ball angle variation**: the vertical direction changes based on where the ball hits the paddle (edge vs centre), giving the player control over shot placement
- **7-segment digital score display**: digits rendered with `Bar` commands using a bitfield-encoded segment table (`SDAT` array, bits gfedcba)
- **Sam Raw square wave beeps**: a 2048-byte square wave sample in chip RAM played at different sampling rates (4800-8000 Hz) for authentic Pong-style sound effects
- **All graphics drawn with Bar/Draw/Print** — no sprites or loaded assets needed

### No Assets Required

Everything is drawn procedurally using Amos drawing commands. No `.abk` sprite banks or `.iff` images are needed.
