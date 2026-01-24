# API Commands

The ARKEO Multichannel API is organized into **command domains**.  
Each domain groups commands that operate on the same logical subsystem and share a common response structure.

Select a section below to explore the available commands.

---

<div class="grid cards" markdown>

-   :material-chip:{ .lg .middle } **Device Commands**
    
    ---
    
    Commands that control **measurement channels**
    
    **Response root:** `channels`
    
    [:octicons-arrow-right-24: Open device commands](device.md)

-   :material-thermometer:{ .lg .middle } **Sensor Commands**
    
    ---
    
    Commands related to **physical sensors**, their configuration, and live values.
    
    **Response root:** `sensors`
    
    [:octicons-arrow-right-24: Open sensor commands](sensors.md)

-   :material-layers-triple:{ .lg .middle } **Environment Commands**
    
    ---
    
    Commands for managing **sensor environments**
    
    **Response root:** `environments`
    
    [:octicons-arrow-right-24: Open environment commands](environments.md)

-   :material-weather-night:{ .lg .middle } **Day–Night Commands**
    
    ---
    
    Commands controlling **day–night cycling**, automation logic, and thresholds.
    
    **Response root:** `day_night`
    
    [:octicons-arrow-right-24: Open day–night commands](day-night.md)

</div>

---

## Command domain overview

Each command belongs to exactly one domain and returns a domain-specific payload.

| Domain | Description | Response key |
|------|-------------|--------------|
| Device | Measurement channels and SMU control | `channels` |
| Sensors | Physical sensors and readings | `sensors` |
| Environments | Sensor grouping and associations | `environments` |
| Day–Night | Global cycling and automation logic | `day_night` |

Clients should rely on the **domain-specific response key** when parsing results.

---

!!! note "Design rule"
    Commands never mix multiple domains in a single response.
