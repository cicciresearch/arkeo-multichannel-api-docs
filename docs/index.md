# ARKEO Multichannel API

Welcome to the **ARKEO Multichannel API documentation**.

This API allows programmatic control of the ARKEO multichannel measurement platform, including device channels, sensors, environments, and automation logic.

The documentation is organized to help you:

- understand the API structure
- discover available commands
- integrate a client step by step

---

## Getting started

If you are new to the API, follow this recommended path:

<div class="grid cards" markdown>

-   :material-swap-horizontal: **Protocol**
    
    ---
    
    Learn how commands and responses are exchanged, including message framing and transport rules.
    
    [:octicons-arrow-right-24: Protocol overview]

-   :material-console-line: **Commands**
    
    ---
    
    Explore all available commands, grouped by functional domain.
    
    [:octicons-arrow-right-24: Commands overview](commands/index.md)

-   :material-code-json: **JSON Objects**
    
    ---
    
    Understand how channels, sensors, and settings are represented in JSON.
    
    [:octicons-arrow-right-24: JSON objects]

</div>
---

## API structure at a glance

The API is organized around **domains**, each with a clear responsibility and response structure:

| Domain | Purpose |
|------|--------|
| Device | Measurement channels and electrical control |
| Sensors | Physical and virtual sensors |
| Environments | Logical grouping of sensors |
| Day–Night | Automation and cycling logic |

Each domain is documented separately and can be used independently.

---

## Who this documentation is for

This documentation is intended for:

- client developers (Python, LabVIEW, C++, etc.)
- system integrators
- advanced users automating measurements

It focuses on **clarity, consistency, and explicit behavior** rather than tutorials or examples tied to a specific language.

---

## Looking for something specific?

- Want to control measurements? → **Device commands**
- Need sensor values? → **Sensor commands**
- Working with automation? → **Day–Night**
- Integrating metadata? → **JSON objects**

Use the navigation menu on the left to jump directly to the relevant section.

---

!!! note
    This documentation describes the API behavior, not a specific client implementation.
