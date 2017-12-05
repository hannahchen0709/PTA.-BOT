First, We need to include the required packages.
>#include "Walk.hpp"
> #include <webots/LED.hpp>
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
#include <string.h>`

#### Text-to-speech
`code(mSpeaker = getSpeaker("Speaker");  
mSpeaker->setLanguage("en-US");
)`
