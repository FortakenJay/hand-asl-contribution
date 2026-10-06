# Hand ASL — my contribution

The recognition app is [JM3927/Hand-ASL-Estimation](https://github.com/JM3927/Hand-ASL-Estimation). I do not own that repo, and this page does not republish it.

My only commit there is [`04443c0`](https://github.com/JM3927/Hand-ASL-Estimation/commit/04443c0) (`env update`). It adds `environment.yml` and `requirements.txt`, and replaces the README with Windows setup steps: Python 3.12.12, a conda env named `ASL`, then `python app.py` from `hand-gesture-recognition-mediapipe#/`. I did not write the recognizer.

## What that app is

From `app.py` in that repo: OpenCV reads the camera, MediaPipe tracks the hand, and a keypoint classifier (`KeyPointClassifier`) labels the gesture. Detection confidence defaults to 0.7 in the argument parser. That code is theirs.

## How to run their project

Follow their README. The setup I committed is the conda env and the requirements file in that folder.

## License

This note is mine. Their source stays under whatever license is on their repo. All rights reserved for this page.
