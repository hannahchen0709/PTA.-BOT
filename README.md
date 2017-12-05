First, We need to include the required packages.
```
#include "Walk.hpp"
#include <webots/LED.hpp>
#include <webots/Motor.hpp>
#include <webots/PositionSensor.hpp>
#include <RobotisOp2MotionManager.hpp>
#include <webots/utils/Motion.hpp>
#include <webots/Speaker.hpp>
#include <webots/Keyboard.hpp>
#include <unistd.h>
#include <iostream>
#include <cstdlib>
#include <fstream>
#include <string.h>
#include <unistd.h>
#include <sys/wait.h>
```

#### -Text-to-speech
  ```
  mSpeaker = getSpeaker("Speaker");  
  mSpeaker->setLanguage("en-US");
  ```
  
### -Motion
Define 20 MOTORS and assign to positionSensors[].
```
for (int i=0; i<NMOTORS; i++) {
   mMotors[i] = getMotor(motorNames[i]);
   string sensorName = motorNames[i];
   sensorName.push_back('S');
   mPositionSensors[i] = getPositionSensor(sensorName);
   mPositionSensors[i]->enable(mTimeStep);
  }
```

Let MotionManager operate this robot.
```
mMotionManager = new RobotisOp2MotionManager(this);
```
Get frequency
```
Motion::getDuration();
```
Do the `"hand_extend.motion"` two times for demonstration
```
Motion motion_1("hand_extend.motion");
    int time1 = motion_1.getDuration();
    for (int i=0; i<2; i++){
    	motion_1.play();
    	wait(time1);
    }
```
>OP2 SERVOS:
>![OP2 SERVOS](https://raw.githubusercontent.com/omichel/webots-doc/master/robotis-op2/images/robotis_op2_servo_map.png)

`"hand_extend.motion"`
```
#WEBOTS_MOTION,V1.0,ArmLowerL,ArmUpperL,ShoulderL,ArmLowerR,ArmUpperR,ShoulderR
00:00:000,handsU,0.02,-0.8,-1.65,-0.02,0.8,1.65
00:02:000,handsExtend,1.63, -0.8, -1.65,-1.65, 0.8, 1.65
00:04:000,handsU,0.02,-0.8,-1.65,-0.02,0.8,1.65
```



