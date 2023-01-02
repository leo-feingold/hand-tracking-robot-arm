# hand-tracking-robot-arm

The robotic arm is controlled by the user's physical hand movements. Hand tracking is done in JavaScript using the p5js library handsfree.js and the code for the arm is Arduino.

  We started the project with an old robotic arm. We took it apart, and wired it up to an Arduino board with relay switches. We added an IR receiver to the Arduino board, and our first iteration of the project was just a wirelessly remote controlled arm.

  Then, we began experimenting with hand tracking API's. After reading about handsfree.js and getting a sense of the documentation, we started writing code to just track the hands and print a string when I pinched my pointer and thumb together. When that was working, we wanted to light up an LED instead of just printing a string, but we ran into a problem. The hand tracking was in JavaScript and we wanted to use Arduino to turn on the light. We looked into ways to relay data from our JavaScript program to the Arduino board and found p5.serialcontrol, an downloadable application that was created to solve this problem. However, for some reason, this was wildly unreliable and didn't work to our liking, so we looked for other solutions and found the web-serial.js API. This API worked and we were able to turn on an LED when I pinched (or did any other movement consisting of raising my hand up or down or side to side). We then finished this iteration of the project by moving the corresponding motors with our hand movements. While this was an awesome accomplishment, we knew that could be improved by using servo motors instead of DC motors, so we moved onto the next iteration of the project.

  We purchased a new arm that was controlled by servo motors, and repeated the process over again with the new arm, with only a couple of differences. With the first iteration of the hand tracking, we programmed the arm to move depending on the x and y position of our hand (example: if the distance between the tip of my thumb and the tip of my pointer is less than some threshold, run the pinch function on the arm). With the new arm, we changed the code to map the position of each important value (like the distance between my thumb and pointer) to a corresponding value between 0 and 180. This way, the moment I started pinching, the arm would start moving, unlike before where I would finish pinching and the arm would then start to move.

  One problem we noticed is that the distance reading was dependent on how far or close we were to the webcam, which meant that users who stood either very close or very far from the camera would have many misreadings. To solve this, we changed the distance to a distance ratio, dividing the value of the distance by the distance between the bottom two joints on my pinky (because that distance is constant and won't change if you bend or move your hand). This ratio distance was constant regardless of how close or far I was from the webcam.


For information on handsfree.js and web-serial.js, see:

https://google.github.io/mediapipe/solutions/hands.html

https://developer.mozilla.org/en-US/docs/Web/API/Web_Serial_API

Note:
You can see how to import the libraries in the html file
