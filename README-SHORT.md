# Capjet-Orientation-Control-System Documentation

## Overview

The **Capjet-Orientation-Control-System** helps keep the ROV stable underwater by using a gyroscope to monitor its rotation along the **RightLeft/Y** and **FrontBack/X** axes. When active, the system adjusts the thrusters in real-time to correct any unintentional movement caused by external forces like currents.

### Flowchart

The flowchart below shows how the system operates:

<img src="./img/FlowChart.png" alt="Flowchart" width="400"/>

1. The system checks the gyroscope for rotational movement.
2. If the rotation is within the **Tolerance Level**, no action is taken.
3. If the rotation exceeds the tolerance but is still safe, the system adjusts the thrusters to correct it.
4. If the rotation is beyond the **Out of Bounds** limit, the system shuts down automatically.
5. Manual stop is also available at any time.

---

## Inputs

- **Gyroscope Rotations**: Measures the rotational speed in **degrees per second** across two axes:
  - **RightLeft/Y Rotation**: Rotation along the Y-axis (left to right).
  - **FrontBack/X Rotation**: Rotation along the X-axis (front to back).

For testing, you can manually input values to simulate the gyroscope's readings.

## Outputs

- **Thruster Signals**: The system generates four output signals to control the thrusters:
  - Front Left, Front Right, Back Left, and Back Right thrusters.

These signals are displayed on the front panel via Thruster Gauges, which show real-time adjustments. The signals connect directly to the thrusters to keep the ROV stable.

### Threshold Parameters

- **Tolerance Level**: Defines the threshold for ignoring small, insignificant rotations.
- **Out of Bounds Level**: Sets the maximum allowed rotational speed. Exceeding this limit shuts down the system to prevent damage.
- **Output Amplifier**: Adjusts the strength of the signals sent to the thrusters, controlling how much power is applied based on the detected rotation.

---

## Front Panel Elements

<img src="./img/labViewPanel.png" alt="labViewPanel" width="550"/>

### Controls

- **Rotation Inputs**: Measures the rotational speed from the gyroscope or can be entered manually for testing (Y-axis and X-axis).
- **Tolerance Level**: Ignores small rotations below the set threshold.
- **Out of Bounds Level**: Sets the maximum safe rotation speed, shutting the system down if exceeded.
- **Output Amplifier**: Adjusts thruster power based on rotation data for fine-tuned control.

### Indicators

- **Thruster Gauges**: Show real-time power applied to each thruster.
- **Out of Bounds Indicator**: Lights up when the system detects unsafe rotational speeds.
- **Stop Button**: Manually stops the system anytime.

---

## Block Diagram Breakdown

<img src="./img/labViewBlockDiagram.png" alt="labViewBlockDiagram" width="550"/>

### Input Processing

- Rotations from the Y and X axes are compared to the **Tolerance Level**. If the rotation exceeds this value, the system activates the thrusters.

### Compensation Logic

- For both axes, if the rotation is above the tolerance level, the system sends signals to the thrusters to correct it.
- The **Output Amplifier** controls the strength of the signals, adjusting thruster power based on the rotation detected.
- **Multipliers** ensure the right amount of compensation is applied to each thruster to stabilize the ROV.

### Out of Bounds Detection

- If rotation exceeds the **Out of Bounds Level**, the system:
  - Activates the **Out of Bounds Indicator**.
  - Shuts down to prevent instability.

### Stop Logic

- The **Stop Button** halts the system manually, ensuring it stops either when pressed or when the **Out of Bounds** condition occurs.