# HandVolumeControl

This project demonstrates how computer vision and hand gesture recognition can be used to control the system volume using hand movements. Instead of manually adjusting the volume through keyboard keys or system controls, the user can simply move their fingers in front of a webcam to increase or decrease the volume.

The system detects the distance between the thumb and index finger using real-time hand tracking. The distance is then mapped to the system's audio volume range, allowing smooth and intuitive volume control.

This project is built using Python, OpenCV, MediaPipe-based hand tracking, and Pycaw for system audio control, combining intermediate computer vision concepts with real-world interaction.


# Features

1.Real-time hand tracking using webcam
2.Detects thumb and index finger positions
3.Calculates distance between fingers
4.Maps finger distance to system volume level
5.Displays volume bar UI
6.Shows real-time FPS counter
7.Smooth volume control using interpolation


# Concepts Used

This project uses several intermediate computer vision and Python concepts:
1.Real-time video processing
2.Hand landmark detection
3.Gesture-based interaction
4.Distance calculation using Euclidean formula
5.Mapping values using interpolation
6.System audio control using COM interface
7.Frame rate calculation (FPS)


# Python Libraries Used

1. OpenCv:
   Used for -
   1.Capturing webcam video
   2.Drawing UI elements (circles, lines, rectangles)
   3.Displaying the processed video frame
       pip install opencv-python

2. MediaPipe (inside HandTrackingModule):
   Used for -
   1.Detecting hand landmarks
   2.Tracking finger positions
   3.Identifying thumb and index finger coordinates
        pip install mediapipe

3. NumPy:
   Used for -
   1.Interpolation between hand distance and volume range
   2.Numerical calculations
        pip install numpy

4. Pycaw:
   Used for -
   1.Controlling system audio volume
   2.Interfacing with Windows audio endpoint
         pip install pycaw

5. Comtypes:
   Used for -
   Handling COM interfaces required by Pycaw to control system audio.
          pip install comtypes



# Step-by-Step Working Process

Step 1: Capture Webcam Video
OpenCV is used to access the system webcam and capture frames continuously.
      cap = cv2.VideoCapture(0)
Each frame from the webcam is processed in real-time.

Step 2: Detect Hands
A custom HandTrackingModule based on MediaPipe is used to detect hands and extract landmark points.
      img = detector.findHands(img)
lmList = detector.findPosition(img)
MediaPipe detects 21 hand landmarks.

Step 3: Extract Finger Positions
We extract coordinates of:
      Thumb tip → Landmark 4
      Index finger tip → Landmark 8
            x1, y1 = lmList[4][1], lmList[4][2]
            x2, y2 = lmList[8][1], lmList[8][2]

Step 4: Calculate Distance Between Fingers
The distance between the two fingers is calculated using the Euclidean distance formula.
        distance = √((x2-x1)² + (y2-y1)²)

_Implemented using Python_:
        length = math.hypot(x2 - x1, y2 - y1)
        
Step 5: Map Distance to Volume Range
The finger distance is mapped to the system's volume range using NumPy interpolation.
Hand distance range:
     50 → fingers close
     300 → fingers far

Volume range:
     -65 → minimum volume
      0 → maximum volume

Mapping:
     vol = np.interp(length, [50,300], [minVol,maxVol])

     
Step 6: Control System Volume
Using Pycaw, the mapped value is applied to the system volume.
     volume.SetMasterVolumeLevel(vol, None)
     
Step 7: Display Volume Bar
A visual volume bar is displayed using OpenCV to represent the current volume level.
      cv2.rectangle(img,(50,150),(85,400),(0,255,0),3)
The filled portion represents the active volume.

Step 8: Show FPS
Frames per second (FPS) is calculated to monitor real-time performance.
       fps = 1/(cTime-pTime)


# Project Output


When the program runs:

1️⃣ Webcam opens
2️⃣ Hand is detected
3️⃣ Thumb and index finger distance is measured
4️⃣ Moving fingers apart increases volume
5️⃣ Moving fingers closer decreases volume
6️⃣ Volume bar updates in real time


# Project Structure

Hand-Gesture-Volume-Control
│
├── VolumeHandControl.py
├── HandTrackingModule.py
├── requirements.txt
└── README.md


# Future Improvements

Possible enhancements for this project:

1.Gesture-based mute/unmute
2.Gesture-based media control (play/pause)
3.Smooth volume control using filters
4.Add GUI dashboard
5.Multi-hand gesture recognition
6.Integration with AI voice assistant


# Learning Outcomes

Through this project I learned:
1.Real-time computer vision applications
2.Hand landmark detection
3.Gesture-based human-computer interaction
4.System-level audio control
5.OpenCV visualization techniques


# Author

Ankit Kumar Jha

Aspiring Machine Learning & Computer Vision Developer passionate about building interactive AI systems and real-world automation projects.
