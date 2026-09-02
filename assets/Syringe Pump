#include <AccelStepper.h>
#include <LiquidCrystal_I2C.h>


AccelStepper stepperX(AccelStepper::DRIVER, 3, 2);
LiquidCrystal_I2C lcd(0x27, 16, 2);


const int buttonPin = 4;
const int limitPin = 9;


const int redPin = 10;
const int greenPin = 6;
const int bluePin = 5;


bool permanentlyStopped = false;
int lastState = -1;


// USER-ADJUSTABLE VARIABLES
float flowRate_mL_min = 500; // desired flow rate in mL/min
float syringeDiameter_mm = 19.0; // syringe inner diameter in mm


// Motor variable set-up
const int motorStepsPerRev = 200; // 1.8 deg stepper
const int microstepSetting = 16; // 1/16 microstepping
const float leadScrewPitch_mm_rev = 2.0; // plunger travel per motor rev


float motorSpeed_stepsPerSec = 0.0;




// Convert flow rate to stepper speed
float calculateStepperSpeed(float flow_mL_min, float diameter_mm) {
  // 1 mL = 1000 mm^3
  float flow_mm3_sec = (flow_mL_min * 1000.0) / 60.0;
  float area_mm2 = 3.14159 * (diameter_mm / 2.0) * (diameter_mm / 2.0);


  // plunger speed in mm/s
  float plungerSpeed_mm_sec = flow_mm3_sec / area_mm2;


  // motor rev/s
  float revPerSec = plungerSpeed_mm_sec / leadScrewPitch_mm_rev;


  // microsteps/s
  float stepsPerSec = revPerSec * motorStepsPerRev * microstepSetting;
  return stepsPerSec;
}




void updateMotorSpeed() {
  motorSpeed_stepsPerSec = calculateStepperSpeed(flowRate_mL_min, syringeDiameter_mm);
  if (motorSpeed_stepsPerSec < 1.0) {
    motorSpeed_stepsPerSec = 1.0; // prevent issues with extremely tiny values
  }
  stepperX.setMaxSpeed(motorSpeed_stepsPerSec * 2.0);
  stepperX.setSpeed(motorSpeed_stepsPerSec);
}




void setup() {
  pinMode(buttonPin, INPUT_PULLUP);
  pinMode(limitPin, INPUT_PULLUP);


  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);


  lcd.init();
  lcd.backlight();
  lcd.clear();


  updateMotorSpeed();
}




void loop() {
  bool motorOn = (digitalRead(buttonPin) == LOW); // button pressed
  bool limitHit = (digitalRead(limitPin) == HIGH); // adjust if switch logic is opposite
  int currentState = 0;


  // latch permanent stop
  if (limitHit) {
    permanentlyStopped = true;
  }


  // permanently stopped
  if (permanentlyStopped) {
    analogWrite(redPin, 255);
    analogWrite(greenPin, 0);
    analogWrite(bluePin, 0);


    if (lastState != 1) {
      lcd.clear();
      lcd.setCursor(0, 0);
      lcd.print("Fully dispensed");
      lcd.setCursor(0, 1);
      lcd.print("Please reset");
      lastState = 1;
    }
    return;
  }




  // running
  if (motorOn) {
    stepperX.runSpeed();


    analogWrite(redPin, 0);
    analogWrite(greenPin, 255);
    analogWrite(bluePin, 0);


    currentState = 2;
  }
  // paused
  else {
    analogWrite(redPin, 255);
    analogWrite(greenPin, 90);
    analogWrite(bluePin, 0);


    currentState = 3;
  }




  if (currentState != lastState) {
    lcd.clear();
    if (currentState == 2) {
      lcd.setCursor(0, 0);
      lcd.print("Running at:");
      lcd.setCursor(0, 1);
      lcd.print(flowRate_mL_min, 2);
      lcd.print(" mL/min");
    }
    else if (currentState == 3) {
      lcd.setCursor(0, 0);
      lcd.print("Paused");
    }
    lastState = currentState;
  }
}
