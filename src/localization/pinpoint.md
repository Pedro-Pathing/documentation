# Setting Up Your Pinpoint Localizer

## Prerequisites
* Pinpoint module connected to an I2C port.
* Dead wheel encoder wires properly connected to the Pinpoint module.

---

## Default Values
These are the default values of the PinpointConstants. You can copy and paste this into your `static{}` block within `LConstants`:
```java
    PinpointConstants.forwardY = 1;
    PinpointConstants.strafeX = -2.5;
    PinpointConstants.distanceUnit = DistanceUnit.INCH;
    PinpointConstants.hardwareMapName = "pinpoint";
    PinpointConstants.useYawScalar = false;
    PinpointConstants.yawScalar = 1.0;
    PinpointConstants.useCustomEncoderResolution = false;
    PinpointConstants.encoderResolution = GoBildaPinpointDriver.GoBildaOdometryPods.goBILDA_4_BAR_POD;
    PinpointConstants.customEncoderResolution = 13.26291192;
    PinpointConstants.forwardEncoderDirection = GoBildaPinpointDriver.EncoderDirection.REVERSED;
    PinpointConstants.strafeEncoderDirection = GoBildaPinpointDriver.EncoderDirection.FORWARD;
```

---

## Steps

### 1. Setup

Navigate to the file `LConstants` and into the `static{}` block and configure the following:

1. Pinpoint Port: 
   - Set the `PinpointConstants.hardwareMapName` variable to the name of the I2C port connected to the Pinpoint module. 
   - Make sure that the I2C port is not the Control Hub built-in IMU port (port 0).
2. Odometry Measurements:
   - Input the `forwardY` and `strafeX` values. These values represent the distance of the odometry pods from the robot's center of rotation on the [robot coordinate grid](./setup.md#robot-coordinate-grid).
   - The default values are `1` for `forwardY` and `-2.5` for `strafeX`.
   - The default distance measurement is in inches, which can be changed by modifying the `Pinpoint.distanceUnit` variable.
3. Encoder Resolution:
   - By default, the encoder resolution is set to `GoBildaPinpointDriver.GoBildaOdometryPods.goBILDA_4_BAR_POD`.
   - If you are using a custom encoder resolution, set `PinpointConstants.useCustomEncoderResolution` to `true` and input the custom resolution in the `PinpointConstants.customEncoderResolution` variable.
4. Encoder Directions:
   - Ensure the encoder directions are correctly set. You can test this by running the `LocalizationTest` TeleOp Opmode.
     - If the `x` value ticks down when the robot moves forward, reverse the direction by changing the `GoBildaPinpointDriver.EncoderDirection` values for `PinpointConstants.forwardEncoderDirection`
     - If the `y` value ticks down when the robot moves left, reverse the direction by changing the `GoBildaPinpointDriver.EncoderDirection` values for`PinpointConstans.strafeEncoderDirection`.
   - The default values are `GoBildaPinpointDriver.EncoderDirection.REVERSED` for `forwardEncoderDirection` and `GoBildaPinpointDriver.EncoderDirection.FORWARD` for `strafeEncoderDirection`.
5. Yaw Scalar:
   - If you want to use a yaw scalar, set `PinpointConstants.useYawScalar` to `true` and input the scalar value in the `PinpointConstants.yawScalar` variable.
   - Note: The Yaw Scalar overrides the calibration done by GoBilda. It is recommended to use leave `PinpointConstants.useYawScalar` as `false` unless you have a specific reason to change it.

### 2. Verifying Pinpoint Connection

Run the `SensorGoBildaPinpointExample.java` file located in the `tuners` folder. This will ensure the Pinpoint is correctly connected and operational.

---

## Testing Your Localizer

After completing the tuning steps, you can test your localizer's accuracy.

1. Go to `Localization Test` and drive your robot around.

2. Open the FTC Dashboard at http://192.168.43.1:8080/dash.

3. Switch the view to "field view" from the top right corner dropdown.

4. The dashboard should display the robot's position on the field.

5. Observe the movements, moving the robot forward should make `x` increase and strafing left should make `y` increase.

---

## Congratulations on successfully setting up your localizer!
