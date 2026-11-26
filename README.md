# EV9-Dashboard-for-HA
A functional and aesthetic dashboard for managing a Kia EV9.

# Kia EV9 Home Assistant Cockpit Dashboard

An interactive, responsive dark-mode vehicle cockpit for Home Assistant built for mobile phones and widescreen tablets. Designed around quick-glance telemetry, tactile vehicle controls, and deep-dive diagnostic popups without clutter.

---

## 📸 Key Highlights & Features

- **Adaptive Header**:
  - Live zone or auto-truncating City, State pill (`device_tracker.ev9_location`) with tap-to-map modal.
  - Telemetry freshness counter (`Synced Xm ago`) with low 12V auxiliary warning alert.
  - Direct force-refresh cloud button.

- **Hero Vehicle Stage**:
  - Vehicle asset (`/local/ev9/hero.png`) with dynamic underglow reflecting power and thermal states.
  - Contextual status badges: `CHARGING · X.X kW` (or `DC FAST` with time-to-target ETA), `PLUGGED`, and `WARMING` / `COOLING` cabin cues.
  - Exception-only perimeter alert pills (doors, frunk, trunk, glass sunroof, low TPMS PSI, or unlocked state).
  - 0–100% full-spectrum color progress bar with charge-limit marker pip, animated charging travel beam, and tap-for-diagnostics overlay.

- **Vehicle Diagnostics & Health Popup**:
  - Dedicated lock/unlock doors with confirmation safeguards.
  - Target-range projections against configured AC/DC charge limits.
  - Core vitals: Odometer, 12V Aux, Battery SoH, DTC codes, upcoming service interval, and cloud sync age.
  - Perimeter security overview with door and tire status indicators.

- **NACS Charging Suite & Tactile Steppers**:
  - Master charge toggle with live flow rate, target ETA, and deep-dive history graph.
  - Independent, native stepper buttons (`-10%` / `+10%`) flanking AC and DC charging limit readouts.

- **Cabin Climate Control**:
  - One-tap climate toggle with dynamic thermal ripple wave effects.
  - Quick presets (`66° Cool` / `74° Warm`) and discrete `[-]` / `[+]` temperature steppers.
  - Radial target gauge and full HVAC/comfort popup (steering wheel, defrost, mirror/window heaters, battery preconditioning).

- **Charge Insights & Smart Departure Planner**:
  - Real-time/historical session telemetry: Efficiency (`mi/kWh`), Energy (`kWh`), Cost (`USD`), and Range Added (`mi`).
  - Scheduled departure planner with preconditioning lead times and ready-by status.

---

## 🛠️ Prerequisites & Requirements

Install the following via [HACS](https://hacs.xyz/):

1. **[custom:button-card](https://github.com/custom-cards/button-card)**
2. **[browser_mod](https://github.com/thomasloven/hass-browser_mod)** (for diagnostic, location, and control popups)

---

## 📂 Asset Placement

Place your transparent PNG render of the Kia EV9 into your Home Assistant `www` directory:

```text
/config/www/ev9/hero.png  --->  accessible in Lovelace as: /local/ev9/hero.png
```

---

## ⚙️ Entity Mapping Reference

Update or verify the following entity names in your dashboard YAML to match your vehicle integration:

| Component | Entity Name |
| :--- | :--- |
| **Battery State of Charge** | `sensor.ev9_ev_battery_level` |
| **Estimated Range** | `sensor.ev9_ev_range` |
| **Charging Power & Status** | `sensor.ev9_ev_charging_power`, `binary_sensor.ev9_ev_battery_charge`, `binary_sensor.ev9_ev_battery_plug` |
| **Charge Limits** | `number.ev9_ac_charging_limit`, `number.ev9_dc_charging_limit`, `switch.ev9_ev_charging` |
| **Locks & Security** | `lock.ev9_door_lock`, `binary_sensor.ev9_front_left_door`, `binary_sensor.ev9_front_right_door`, etc. |
| **Climate & Thermal** | `switch.ev9_climate`, `climate.ev9_climate_control` |
| **Sensors & Location** | `device_tracker.ev9_location`, `sensor.ev9_car_battery_level` (12V), `sensor.ev9_odometer`, `sensor.ev9_last_updated_at` |
| **Departure Automation** | `input_boolean.ev9_departure_enabled`, `input_datetime.ev9_ready_by`, `input_number.ev9_departure_lead`, `input_number.ev9_departure_temp` |

---

## 📱 Layout Variants

- **Phone Layout (`ev9-phone.yaml`)**: Single-column vertical stack optimized for one-handed thumb interaction and mobile viewport widths.
- **Tablet Layout (`ev9-tablet.yaml`)**: 2-column widescreen layout pairing the vehicle hero stage, quick actions, and climate on the left with a 16:9 24-hour location map, charging controls, session telemetry, and departure planner on the right.