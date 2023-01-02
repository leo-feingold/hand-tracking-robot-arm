# hand-tracking-robot-arm
# Robotic Arm is controlled by user's physical hand movements. Hand tracking is done in Javascript using the p5js library handsfree.js

//Notes for program: press run, start webcam, press on the preview and click any key. Only after will the program work

let port, reader, writer;
var startPinching = false;
var startShoulder = false;
var startTesting = false;

async function setup() {
	sketch = createCanvas(640, 480)
	background("black");
  

	noLoop();
	({ port, reader, writer } = await getPort());
	loop();
  
    handsfree = new Handsfree({
      hands: true
    })
    handsfree.enablePlugins('browser')
    handsfree.plugin.pinchScroll.disable()
  
  buttonStart = createButton('Start Webcam')
  buttonStart.class('handsfree-show-when-stopped')
  buttonStart.class('handsfree-hide-when-loading')
  buttonStart.mousePressed(() => handsfree.start())

  // Create a "loading..." button
  buttonLoading = createButton('...loading...')
  buttonLoading.class('handsfree-show-when-loading')

  // Create a stop button
  buttonStop = createButton('Stop Webcam')
  buttonStop.class('handsfree-show-when-started')
  buttonStop.mousePressed(() => handsfree.stop())
  
}

async function draw() {
    background(0);
  
    drawHands();
	if (port && startTesting) {
		try {
			if (startTesting) {
    
				await pinch();
                await shoulder();
                await wrist();
			}

		} catch (e) { console.error(e) }
	}
  

  // background(0);
  // drawHands()
  // if(startPinching){
  //   pinch()
  // }
  
}

function drawHands () {
  const hands = handsfree.data?.hands
  
  // Bail if we don't have anything to draw
  if (!hands?.landmarks) return
  
  // Draw keypoints
  hands.landmarks.forEach((hand, handIndex) => {
    hand.forEach((landmark, landmarkIndex) => {

        circleSize = 20
  
      
      circle(
        // Flip horizontally
        sketch.width - landmark.x * sketch.width,
        landmark.y * sketch.height,
        circleSize
      )
    })
  })
}

function keyPressed(){
  startPinching = true;
  startShoulder = true;
  startTesting = true;
}

function pinch(){
  const hands = handsfree.data? handsfree.data.hands : null
  if (hands.landmarks[1][4].x - hands.landmarks[1][8].x <= 0.01){
    console.log("w");
    writer.write("pinch\n");
  }
  
   else if (hands.landmarks[1][4].x - hands.landmarks[1][8].x >= 0.12){
         writer.write("open pinch\n");
			}
  else{
   writer.write("do nothing\n");
  }

}

function shoulder(){
    const hands = handsfree.data? handsfree.data.hands : null

    if(hands.landmarks[1][4].y < 0.25){
    console.log(hands.landmarks[1][4].y);
      writer.write("shoulder up\n")
    }
    else if(hands.landmarks[1][4].y > 0.65){
      writer.write("shoulder down\n")
    }
  
    else{
      writer.write("no shoulder\n")
}
}

function wrist(){
    const hands = handsfree.data? handsfree.data.hands : null
    if(hands.landmarks[0][4].y < 0.25){
    console.log(hands.landmarks[0][4].y);
      writer.write("wrist up\n")
    }
    else if(hands.landmarks[0][4].y > 0.65){
      writer.write("wrist down\n")
    }
  
    else{
      writer.write("no wrist\n")
}
}

