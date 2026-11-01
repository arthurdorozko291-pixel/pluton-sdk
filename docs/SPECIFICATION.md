# Pluton Language & Runtime Specification

## 1. Design Philosophy

Modern systems and AI engineering frequently suffer from multi-language fragmentation: Python wrappers orchestrating C++ bindings, separate shader/rendering pipelines, and external networking daemons. **Pluton** unifies:

1. **Deterministic Execution:** No unpredictable garbage-collection pauses inside 60 FPS loops or tensor gradient steps.
2. **Native Mathematical Primitives:** Vectors and byte streams are built into the core language semantics.
3. **Direct Hardware & Cloud Telemetry:** Built-in GPU memory introspection and native cloud training supervision hooks.

---

## 2. Standard Libraries

### 2.1 `Plutonium` (2D Graphics & Windowing)
- `Plutonium.init(width, height, title)` — Initializes a hardware-accelerated window.
- `Plutonium.is_open() -> bool` — Returns `true` while the window loop is active.
- `Plutonium.clear(hex_color)` — Clears the framebuffer.
- `Plutonium.key_down(key_name) -> bool` — Polls real-time keyboard state.
- `Plutonium.draw_rect(x, y, w, h, color, filled)`
- `Plutonium.draw_round_rect(x, y, w, h, radius, color, filled)`
- `Plutonium.draw_grid(cols, rows, cell_size, color, thickness)`
- `Plutonium.draw_glow_circle(x, y, radius, color, glow_strength)`
- `Plutonium.draw_gradient(x, y, w, h, color_a, color_b, angle)`
- `Plutonium.draw_text(text, x, y, font_size, color)`
- `Plutonium.beep(freq_hz, duration_ms)`
- `Plutonium.get_fps() -> float`
- `Plutonium.update(target_fps)` — Presents the frame and locks frame pacing.
- `Plutonium.close()`

### 2.2 `Plutonium3D` (3D Scene & Lighting Pipeline)
- `Plutonium3D.set_camera(x, y, z, look_x, look_y, look_z, fov)`
- `Plutonium3D.set_light(dir_x, dir_y, dir_z)`
- `Plutonium3D.draw_grid_3d(size, step, color)`
- `Plutonium3D.draw_cube(x, y, z, size, fill_color, rot_x, rot_y, rot_z, wireframe, wire_color)`
- `Plutonium3D.draw_pyramid(x, y, z, size, fill_color, rot_x, rot_y, rot_z, shaded)`

### 2.3 `PlutoNET` & `Laser` (Binary Networking)
- `tcp.connect(host, port) -> Socket`
- `Socket.send(bytes)` / `Socket.recv(num_bytes)`
- `ByteStream.new()` — Allocates a binary packet builder.
- `ByteStream.write_int(v)` / `ByteStream.write_long(hi, lo)` / `ByteStream.write_string(s)`
- `ByteStream.create_packet(packet_id, payload_bytes, version)`
- `ByteStream.read_header(raw_7_bytes) -> Header`

### 2.4 `hardware` (Accelerator Introspection)
- `hardware.is_available() -> bool`
- `hardware.gpu(index) -> GpuDevice` (`name: string`, `vram: int`)
