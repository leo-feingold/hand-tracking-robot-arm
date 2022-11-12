# hand-tracking-robot-arm
The robotic arm is controlled by the user's physical hand movements. Hand tracking is done in JavaScript using the p5js library handsfree.js

I used the p5js library handsfree.js to track the user's hands. You can see how to import the library in the html file. When specific joints
(or landmarks as the library refers to them) are held in specific places, the JavaScript sends a signal to the arduino board
using web-serial.js. Depending on the signal the arduino recieves from the JavaScript, it moves certain motors on the arm, mimicking the movements of the user. 

For information on handsfree.js and web-serial.js, see:

https://google.github.io/mediapipe/solutions/hands.html

https://developer.mozilla.org/en-US/docs/Web/API/Web_Serial_API
