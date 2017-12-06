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
The volume argument allows the user to specify the volume of this sound (between 0.0 and 1.0).
  ```
  mSpeaker = getSpeaker("Speaker");  
  mSpeaker->setLanguage("en-US"); //en-US" for American English
  Speaker::speak(const std::string &text, double volume);
  ```
Encouragement function
```
  mSpeaker->speak("You can do it!",1.0);
  wait(3000);
  mSpeaker->speak("Keep Going!",1.0);
  wait(1000);
```
Three difficult level
```
case 0:  strncpy(command, "5", sizeof(command) - 1);
         mSpeaker->speak("Let’s start with our third exercise. Please follow the demonstration and repeat three times.",1.0);
         wait(6000); 
         break;
case 1:  strncpy(command, "10", sizeof(command) - 1);
         mSpeaker->speak("Let’s start with our third exercise. Please follow the demonstration and repeat five times.",1.0);
         wait(6000); 
         break;
case 2:  strncpy(command, "15", sizeof(command) - 1);
         mSpeaker->speak("Let’s start with our third exercise. Please follow the demonstration and repeat eight times.",1.0);
         wait(6000); 
         break;
```
```
  if(resultFromCNN == 0){
    std::cout << "Result from CNN == 0, let's decrease level if posibble"<< std::endl;
    currentLevel--;
    if(currentLevel < 0){
      currentLevel = 0;
    }
  }else if(resultFromCNN == 1){
    std::cout << "Result from CNN == 1, let's increase level if posibble"<< std::endl;
    currentLevel++;
    if(currentLevel > 2){
      currentLevel = 2;
    }
  }
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
The step method has to be called to run it (before calling the robot step function).
```
myStep();
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
![OP2 SERVOS](https://raw.githubusercontent.com/omichel/webots-doc/master/robotis-op2/images/robotis_op2_servo_map.png)

Change the rad of six servos to get motions.

```"hand_extend.motion"```:
```
#WEBOTS_MOTION,V1.0,ArmLowerL,ArmUpperL,ShoulderL,ArmLowerR,ArmUpperR,ShoulderR
00:00:000,handsU,0.02,-0.8,-1.65,-0.02,0.8,1.65
00:02:000,handsExtend,1.63, -0.8, -1.65,-1.65, 0.8, 1.65
00:04:000,handsU,0.02,-0.8,-1.65,-0.02,0.8,1.65
```
`"hand_high.motion"`:
```
#WEBOTS_MOTION,V1.0,ArmLowerL,ArmUpperL,ShoulderL,ArmLowerR,ArmUpperR,ShoulderR
00:00:000,handsU,0.02,-0.8,-1.65,-0.02,0.8,1.65
00:02:000,handsUp,1.63,0.77,-3.14,-1.65,-0.68,3.14
00:04:000,handsU,0.02,-0.8,-1.65,-0.02,0.8,1.65
```

```
mMotionManager->playPage(15);
    wait(500);
    mMotionManager->playPage(1);
```
Play a motion.
```
void playPage(int id);
```
![OP2 motion files](https://i.imgur.com/PZbc2a2.png)


