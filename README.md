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
>`mMotionManager = new RobotisOp2MotionManager(this);`

Do the `"hand_extend.motion"` two times for demonstration
```
Motion motion_1("hand_extend.motion");
    int time1 = motion_1.getDuration();
    for (int i=0; i<2; i++){
    	motion_1.play();
    	wait(time1);
    }
```
