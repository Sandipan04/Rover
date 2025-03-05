# Contents

Use pyfirmata2 with Arduino wherever necessary.

- Inverse Kinematics (with [one hinge](Sensor%20Integration/inverse%20kinematics/inverse_kin%202%20arms.py) and [two hinges](Sensor%20Integration/inverse%20kinematics/inverse_kin%203%20arms.py))
- [Working arm controller](Sensor%20Integration/arm_working.ipynb) (rotates the arm to a given $(x,y,z)$ coordinate)
- [Manipulator Base Alignment](Sensor%20Integration/basealign.py) (rotates the arm base to a given angle)
- Arduino Integrations
  - [Servo Motor](Sensor%20Integration/servo/servo.py)
  - [Ultrasonic Sensor](Sensor%20Integration/ultrasonic/ultrasonic.py)
  - Stepper Motor ([A4988 driver](Sensor%20Integration/StepperLib.py))
  - [DC Motor](Sensor%20Integration/dcmotor_encoder.py)
  - [MPU 6050](Sensor%20Integration/mpu6050.py) (accelerometer and gyroscope module)
  - [NRF 2401](Sensor%20Integration/nrf.py) (wireless transceiver)

# Stepper Motor Control Usage

This section describes how to use the `Stepper` and `Stepper_ULN2003` classes to control stepper motors with an Arduino using PyFirmata.

## Prerequisites

Ensure you have the following installed:
- Python 3
- `pyfirmata` library (`pip install pyfirmata`)
- Arduino with Firmata firmware uploaded
- Stepper motor driver (A4988 or ULN2003)

## Initializing the Stepper Motor

### A4988 Driver-Based Stepper Motor

```python
from stepper_module import Stepper  # Assuming the file is named stepper_module.py

stepper = Stepper(board, dir_pin=8, step_pin=7, micro_step_pins=(2,3,4), total_steps=200)
```

### ULN2003 Driver-Based Stepper Motor

```python
from stepper_module import Stepper_ULN2003

stepper = Stepper_ULN2003(board, pins=(8,9,10,11))
```

## Controlling the Stepper Motor

### Rotating by a Specific Angle (A4988)

```python
stepper.turn_angle(90)  # Rotates the stepper motor by 90 degrees
```

### Setting Step Delay

```python
stepper.set_delay(0.005)  # Adjusts step delay for speed control
```

### Rotating the Stepper Motor (ULN2003)

```python
stepper.rotate(num_rotations=2, direction=True)  # Rotates 2 full turns clockwise
stepper.rotate(num_rotations=1, direction=False)  # Rotates 1 full turn counterclockwise
```

## Additional Information

### Setting Microstep Resolution (A4988)

The driver supports multiple resolutions:
- `0` - Full step
- `1` - Half step
- `2` - Quarter step
- `3` - 1/8 step
- `4` - 1/16 step

Example:

```python
stepper.set_resolution(2)  # Sets quarter-step resolution
```

### Switching Rotation Direction

```python
stepper.switch_direction()
```

## Notes
- Ensure proper power connections to avoid damaging the stepper driver.
- The Arduino must have the StandardFirmata firmware uploaded.

This concludes the stepper motor usage guide. More modules will be added in separate sections as the project expands.

