# Virtual Mouse

A Python application that uses computer vision to control mouse actions through hand gestures captured via a webcam. The system detects hand landmarks to perform actions like left click, right click, double click, screenshot, and mouse movement.

## Language
- **Python**: The primary programming language, compatible with Python 3.8+.

## Dependencies
- `opencv-python`: For webcam capture and image processing.
- `numpy`: For numerical computations (e.g., angle and distance calculations).
- `pyautogui`: For mouse control and screenshot capture.
- `pynput`: For simulating mouse button presses.
- `mediapipe`: For hand landmark detection (assumed, not explicitly imported).

## Functionality
The application recognizes the following hand gestures:
- **Mouse Movement**: Move the index finger tip to control the cursor when the thumb-index distance is small and the index finger is extended.
- **Left Click**: Index finger folded, middle finger extended, thumb-index distance > 90 pixels.
- **Right Click**: Middle finger folded, index finger extended, thumb-index distance > 90 pixels.
- **Double Click**: Both index and middle fingers folded, thumb-index distance > 90 pixels.
- **Screenshot**: Both index and middle fingers folded, thumb-index distance < 50 pixels (saves as `my_screenshot_<random>.png`).

## Setup Instructions
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/kishan8354/Virtual-Mouse.git
   cd hand-gesture-mouse-control
   ```

2. **Install Python**:
   Ensure Python 3.8+ is installed. Download from [python.org](https://www.python.org/downloads/).

3. **Install Dependencies**:
   Create a virtual environment (optional) and install required packages:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install opencv-python numpy pyautogui pynput mediapipe
   ```

4. **Connect a Webcam**:
   Ensure a webcam is connected and functional.

5. **Run the Application**:
   Execute the main script (e.g., `main.py`):
   ```bash
   python main.py
   ```

## Usage
1. Launch the application with your webcam active.
2. Position your hand in front of the camera, palm facing forward.
3. Perform gestures:
   - **Move Cursor**: Point with your index finger, keeping thumb close.
   - **Left Click**: Fold index finger, extend middle finger, spread thumb.
   - **Right Click**: Fold middle finger, extend index finger, spread thumb.
   - **Double Click**: Fold both index and middle fingers, spread thumb.
   - **Screenshot**: Fold both fingers, bring thumb close to index finger.
4. Gesture feedback is displayed on the video feed (e.g., "Left click", "Screenshot Taken").

## Code Structure
- **`is_left_click(landmarks_list, thumb_index_dist)`**: Detects left click gesture based on index finger angle (<50°), middle finger angle (>90°), and thumb-index distance (>90).
- **`is_right_click(landmarks_list, thumb_index_dist)`**: Detects right click with reversed finger angles.
- **`is_double_click(landmarks_list, thumb_index_dist)`**: Detects double click when both fingers are folded.
- **`is_screenshot(landmarks_list, thumb_index_dist)`**: Detects screenshot gesture with small thumb-index distance.
- **`detect_getures(frame, landmarks_list, processed)`**: Main gesture detection logic, moves mouse or triggers actions, and annotates the frame.
- **`get_angle(a, b, c)`**: Calculates the angle between three points (hand landmarks).
- **`get_distance(landmark_list)`**: Computes and normalizes distance between two landmarks.

## Example Code Snippet
```python
def is_left_click(landmarks_list, thumb_index_dist):
    return (util.get_angle(landmarks_list[5], landmarks_list[6], landmarks_list[8]) < 50 and
            util.get_angle(landmarks_list[9], landmarks_list[10], landmarks_list[12]) > 90 and
            thumb_index_dist > 90)
```

## Limitations
- **Camera Quality**: Requires a clear webcam feed; low resolution or poor lighting may reduce accuracy.
- **MediaPipe Dependency**: Assumes MediaPipe for landmark detection; ensure proper integration.
- **Gesture Precision**: Angles and distances are hardcoded (e.g., 50°, 90 pixels), which may need tuning for different hands or cameras.
- **Platform**: Tested on Windows/Linux; macOS may require additional `pyautogui` configuration.
- **Background Noise**: Complex backgrounds may interfere with hand detection.

## Contributing
1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/new-gesture`).
3. Commit changes (`git commit -m "Add scroll gesture"`).
4. Push to the branch (`git push origin feature/new-gesture`).
5. Open a pull request.

## License
MIT License. See [LICENSE](LICENSE) for details.