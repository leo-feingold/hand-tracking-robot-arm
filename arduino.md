# hand-tracking-robot-arm
Robotic Arm is controlled by user's physical hand movements. Hand tracking is done in Javascript using the p5js library handsfree.js


if (Serial.available()) {
        // If data is available to read,
        val = Serial.readStringUntil('\n');
        val.trim();
    }

    if (val == "pinch"){
      finger_close();
    }
    
    else if (val == "open pinch"){
      finger_open();
    }

    else if(val == "do nothing"){
      no_finger();
    }

    else if(val == "shoulder up"){
      shoulder_up();
    }

    else if(val == "shoulder down"){
      shoulder_down();
    }

    else if(val == "no shoulder"){
      no_shoulder();
    }
    
    else if(val == "wrist up"){
      wrist_up();
    }

     else if(val == "wrist down"){
      wrist_down();
    }

    else if(val == "no wrist"){
      no_wrist();
    }
}





void stop_all(){
  digitalWrite(wrist_pin_D, HIGH);
  digitalWrite(wrist_pin_U, HIGH);
  digitalWrite(elbow_pin_D, HIGH);
  digitalWrite(elbow_pin_U, HIGH);
  digitalWrite(shoulder_pin_D, HIGH);
  digitalWrite(shoulder_pin_U, HIGH);
  digitalWrite(finger_pin_O, HIGH);
  digitalWrite(finger_pin_C, HIGH);
}



void finger_open() {
  
  digitalWrite(finger_pin_O, LOW);
  digitalWrite(finger_pin_C, HIGH);

}

void finger_close() {
  digitalWrite(finger_pin_O, HIGH);
  digitalWrite(finger_pin_C, LOW);
}


void wrist_up() {
  
  digitalWrite(wrist_pin_U, LOW);
  digitalWrite(wrist_pin_D, HIGH);

  
}

void wrist_down() {
  
  digitalWrite(wrist_pin_U, HIGH);
  digitalWrite(wrist_pin_D, LOW);
}

void elbow_up() {
  
  digitalWrite(elbow_pin_U, LOW);
  digitalWrite(elbow_pin_D, HIGH);
}

void elbow_down() {
  
  digitalWrite(elbow_pin_U, HIGH);
  digitalWrite(elbow_pin_D, LOW);
}


void shoulder_up() {
  
  digitalWrite(shoulder_pin_U, LOW);
  digitalWrite(shoulder_pin_D, HIGH);
}

void shoulder_down() {
  
  digitalWrite(shoulder_pin_U, HIGH);
  digitalWrite(shoulder_pin_D, LOW);
}

void no_shoulder() {
  digitalWrite(shoulder_pin_U, HIGH);
  digitalWrite(shoulder_pin_D, HIGH);
}

void no_finger(){
  digitalWrite(finger_pin_O, HIGH);
  digitalWrite(finger_pin_C, HIGH);
}

void no_wrist(){
  digitalWrite(wrist_pin_U, HIGH);
  digitalWrite(wrist_pin_D, HIGH);
}

void rotate_right(){
  digitalWrite(rotate_R, LOW);
  digitalWrite(rotate_L, HIGH);

}

void rotate_left() {
  digitalWrite(rotate_R, HIGH);
  digitalWrite(rotate_L, LOW);

}

void rotate_stop() {
  digitalWrite(rotate_R, HIGH);
  digitalWrite(rotate_L, HIGH);
}
