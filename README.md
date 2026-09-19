# SIBI Sign Language Detection

A real-time computer vision app that recognizes hand signs from **SIBI (Sistem Isyarat Bahasa Indonesia)** through a webcam and shows the predicted sign on the live video stream. Built as the computer vision deployment project of the **AI for Jobs (Kampus Merdeka / Orbit Future Academy) Batch 3** program in 2022.

## How it works

1. OpenCV captures frames from the webcam.
2. MediaPipe Hands detects the hand and extracts its keypoints (landmark coordinates).
3. The keypoints are passed to a trained **SVM** classifier (scikit-learn), which predicts the sign.
4. The predicted label and FPS are drawn on the frame, and Flask streams the result to the browser as an MJPEG video feed.

## Tech stack

Python, Flask, OpenCV, MediaPipe, scikit-learn (SVM), pandas, NumPy, HTML with Bootstrap.

## Project structure

```
app.py                Flask app: webcam capture, hand keypoint extraction, prediction, video stream
model/svm_model_v3.sav Trained SVM model
SIBI_Lang_Spatio.csv  Keypoint dataset (the app reads the class names from it)
templates/index.html  Page that displays the live stream
static/images/        Logos
```

## Running locally

A webcam is required.

```bash
git clone https://github.com/SaidWildan/sibi-sign-language-detection.git
cd sibi-sign-language-detection
pip install -r requirements.txt
python app.py
```

Then open http://127.0.0.1:5000 in your browser.

> The dependencies are pinned to 2022 versions (for example mediapipe 0.8.10 and scikit-learn 1.1.2). Use Python 3.9 or 3.10 in a virtual environment for the best compatibility.

## Fixes after revisiting

- The model was loaded from `Model/` while the folder is `model/`, which breaks on case-sensitive filesystems such as Linux. The path is now correct.
- The app ran with `debug=True`, which exposes the Werkzeug interactive debugger. It now runs with debug off and binds to localhost only.

## Possible improvements

- Store the class names in a small file instead of loading the 8 MB keypoint CSV at startup.
- Release the camera cleanly when the server stops.

## Author

Said Muhammad Wildan
