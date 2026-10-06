# Hand ASL

Live camera recognition of the American Sign Language alphabet. Source: [JM3927/Hand-ASL-Estimation](https://github.com/JM3927/Hand-ASL-Estimation). This page does not republish that code.

The app reads one hand from a webcam, turns the pose into a size-independent vector, and classifies it as a letter A–Z.

## Libraries

- **OpenCV** captures the frame, mirrors it, and draws the overlay.
- **MediaPipe Hands** finds one hand and returns 21 landmarks.
- **TensorFlow Lite** runs `keypoint_classifier.tflite`. The label file is A through Z.
- **NumPy** holds the landmark vector.

Python 3.12. The conda env is named `ASL`.

## How a frame becomes a letter

```mermaid
flowchart LR
  cam[Webcam] --> cv[OpenCV]
  cv --> mp[MediaPipe Hands]
  mp --> xy[21 x,y points]
  xy --> rel[Subtract the wrist]
  rel --> norm[Divide by the largest absolute value]
  norm --> tflite[TFLite classifier]
  tflite --> letter[A–Z]
  letter --> draw[Draw the letter on the frame]
```

MediaPipe is configured for one hand. Detection confidence defaults to 0.7. Tracking confidence defaults to 0.5.

`calc_landmark_list` turns each landmark into pixel coordinates on the frame. `pre_process_landmark` then:

1. Subtracts landmark 0 (the wrist) from every point, so the hand can sit anywhere in the frame.
2. Flattens the pairs into one list.
3. Divides by the largest absolute value, so a hand close to the camera and a hand far away produce the same shape.

That vector is the TFLite input. The class is `argmax` of the output. The matching row in `keypoint_classifier_label.csv` is the letter drawn on the frame.

A second model, point-history classification, is present in the tree and commented out in `app.py`. The running path is the static keypoint classifier only.

Press ESC to quit. The entry point is `python app.py` from `hand-gesture-recognition-mediapipe#/`.

## License

This note is separate from the source repo. All rights reserved for this page.
