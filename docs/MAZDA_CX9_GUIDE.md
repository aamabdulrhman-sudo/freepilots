# Mazda CX-9 (2021) & Sunnypilot Optimization Guide ًںڑ—

This guide is specifically tailored for owners of the **2021 Mazda CX-9** using **Comma Four / Comma 3X** with **Sunnypilot** and **FreePilots**.

---

## 1. Why Mazda CX-9 (2021) is Unique in openpilot

The 2021 Mazda CX-9 uses Mazda's specialized Electronic Power Steering (EPS) architecture. Compared to Honda or Toyota, Mazda vehicles have non-linear torque feedback and strict lateral limits.

### Key Benefits of Sunnypilot for Mazda CX-9:
- **Speed-Dependent Steering:** Provides lighter, responsive steering at low city speeds, and solid highway lane centering.
- **Torque Smoothing:** Prevents highway ping-ponging (micro-oscillations).
- **Smooth Longitudinal (Speed / Braking):** Works harmoniously with Mazda's adaptive cruise radar.

---

## 2. Recommended Sunnypilot Settings for 2021 CX-9

In your Comma device settings screen under **Sunnypilot Controls**:

1. **Lateral Control (Steering):**
   - **Torque Control:** Enabled.
   - **Steer Rate:** Set to Responsive / High.
   - **Dynamic Lane Profile:** Standard or Smooth.
2. **Longitudinal Control (Gas & Brakes):**
   - Keep stock radar for initial setup. If experimental longitudinal is enabled, ensure braking distance is set to 1.8s+ for smooth stops.
3. **Dashcam & Recording:**
   - Keep recording active! With **FreePilots**, your recordings are safe and only sent to your private vault.

---

## 3. Pairing FreePilots with Your Comma Four in CX-9

1. Ensure your Comma Four connects to your phone's hotspot or home Wi-Fi when parked.
2. Run the FreePilots installation script:
   ```bash
   curl -sSL https://raw.githubusercontent.com/aamabdulrhman-sudo/freepilots/main/device/install.sh | bash
   ```
3. Enter your FreePilots server URL (e.g. `https://dash.aaam.sa`) and token.
4. Enjoy continuous, private dashcam backup for every road trip!
