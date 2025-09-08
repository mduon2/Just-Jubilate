# Just-Jubilate

This repository is a cleaned-up version of the one submitted to the 2024 cuHacking Computer Vision Event. It seeks to solve the problem of Carleton University's lack of exercise options revolving around rhythm-based dance games; Just Dance Now the mobile app simply doesn't cut it with its limited tracking capabilities (you only have to wave your hand to score points).

Just Jubilate addresses these issues by tracking **full-body** poses and comparing them to a dance video, necessitating actual exercise and engagement in order to be awarded points for adherence. 

Even just 2 minutes of daily exercise can improve heart health, boost mood, and reduce stress, with studies showing that regular physical activity can reduce health risks by up to 14%. So throw on a quick song and... *Just Jubilate*!

# How it works

In `camera.py`, OpenCV is used to capture video footage of the user dancing by accessing a device webcam, convert the frames to RGB so they are compatible with MediaPipe's pose estimation library, and process the frames using Tensorflow's machine learning model to recognize poses by detecting and drawing on a frame for the body using MediaPipe's body landmarks.
In `game.py`, the same process is repeated concurrently with a user's desired dance video, and every 100 frames, pose data from both the user's webcam and the video are written to a runtime-created file called angles.txt for comparison purposes. At the end of the dance video, both webcam and video capturing processes are killed, and `angles.txt` is read to determine the user's final score. A margin of error of 45 degrees is employed to account for sources of error in camera positioning and webcam waver, and if the user was able to generate a pose with all joint angles forming a difference of less than 45 degrees with the video, they are awarded 100 points. For example, if they accurately hit 10 poses during the dance video's runtime via our metrics, they would be awarded 1000 points. At the end, the user's final score is displayed, and `angles.txt` is deleted.

# How to play it

1. Download `camera.py` and `game.py` and place them in the same directory.
2. Download your desired dance video as an MP4 file and name it "dance.mp4"
3. Run game.py
4. Enjoy your exercise made fun!

# Possible future implementations

- Include a preset library of dances that the user can choose to dance from with accompanying UI.
- Make a GUI with html/css/js
- Make it into a mobile/desktop app with a framework like electron, flutter, etc... 
- Live server to introduce multiplayer gameplay, with database management to save high scores, etc... (SQL, postegreSQL, MongoDB) 
