---
name: mokxi-circuits
description: Build working Arduino, ESP32 and Raspberry Pi Pico circuits with code in the Mokxi simulator through the Mokxi MCP server. Use when someone asks for an electronics project, a circuit, a sketch for a board, or "a Mokxi link".
---

# Build circuits with Mokxi

Mokxi (mokxi.com) is a browser simulator for Arduino, ESP32, Raspberry Pi Pico, STM32 and more, with 500+ real parts. Through the Mokxi MCP server (`https://mokxi.com/mcp`) you can design a project, check it the way the Mokxi editor does, and hand back a link that opens and runs it.

## Setup

Connect the Mokxi MCP server first:
- Claude: Settings, Connectors, Add custom connector, URL `https://mokxi.com/mcp`, then sign in to Mokxi.
- Claude Code: `claude mcp add --transport http mokxi https://mokxi.com/mcp`

Signing in to Mokxi is required. Free accounts can create 10 projects a day, and Mokxi Pro has no daily limit.

## Workflow

1. **Pick the board.** Call `list_boards` and choose the board the person asked for. If they didn't ask for one, pick the simplest board that fits (Arduino Uno for beginners, ESP32 for Wi-Fi or Bluetooth).
2. **Find the parts.** For each part, call `search_parts`, then `get_part` to read its real pin names. Never guess pin names.
3. **Learn the format.** Call `get_project_format` once per conversation, and follow it exactly for the diagram and the files.
4. **Write the project.** Wire every part with the pin names from `get_part`, and add the resistors a real circuit needs (for example 220 ohm for an LED). Write the sketch for that board's core, using the same pins as the wiring.
5. **Check it.** Call `validate_project`. If it reports problems, fix them and validate again. Repeat until it passes.
6. **Hand it back.** Call `create_project` and give the person the link, with one or two lines on what to press (Run) and what they'll see.

## Rules

- Only use boards and parts the tools return. If a part doesn't exist in Mokxi, say so and suggest the closest one it has.
- Keep the first version small and working, then offer upgrades.
- Mokxi simulates circuits. It does not control real hardware. For anything with mains voltage, say it isn't safe to wire to a microcontroller, and use low-voltage parts in the simulation.
- Explain the circuit in plain words for beginners: what each part does, and which pin it uses.

## Example requests

- "Build an Arduino traffic light with three LEDs and give me the Mokxi link."
- "Make an ESP32 that reads a DHT22 and shows the temperature on an SSD1306 OLED."
- "I have a Pico and a servo. Make it sweep back and forth."
