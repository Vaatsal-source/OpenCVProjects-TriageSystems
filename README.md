🚨 Vision-Based Disaster Triage System

An end-to-end computer vision + algorithmic decision system that detects casualties from an aerial image, assigns priorities, and optimally allocates them to rescue camps under real-world constraints.

📌 Overview

This project simulates a disaster response scenario where:

Rescue camps have limited capacity
Casualties have varying severity levels
The goal is to maximize rescue effectiveness

The system processes an image and outputs an optimized rescue plan.

⚙️ Pipeline
1. Scene Understanding (Computer Vision)
Convert image from BGR → HSV
Perform color segmentation to detect:
🟦 Blue, 🟪 Pink, ⬜ Grey → Rescue Camps
🟡/🟢/🔺 shapes → Casualties
Apply:
Thresholding (cv2.threshold, adaptiveThreshold)
Morphological operations (noise removal)
2. Object Detection
Detect objects using:
cv2.findContours()
cv2.connectedComponentsWithStats()
Extract centroids using image moments
3. Casualty Analysis
Classify based on:
Shape (triangle, square, star)
Size / cluster density
Assign priority scores:
Higher score = higher urgency
4. Camp Detection
Use HSV masks to isolate camps
Extract largest contour per camp
Assign predefined capacities:
Blue → 4
Pink → 3
Grey → 2
5. Optimization (Triage Algorithm)

Two strategies implemented:

✅ Greedy Scoring Approach
Score = priority - distance
Assign best (casualty, camp) pairs first
✅ Priority-First Assignment
Sort casualties by priority
Assign to nearest available camp
Respect:
Capacity constraints
One-time assignment
6. Evaluation Metric

Rescue Ratio (Pr):

Pr=
Total casualties
Total priority rescued
	​

Measures effectiveness of rescue allocation
Higher = better triage decision
🧠 Key Concepts Used
Computer Vision (OpenCV)
Image Segmentation (HSV masking)
Contour & Blob Detection
Spatial Reasoning (Euclidean Distance)
Greedy Algorithms
Heuristic Optimization
📊 Example Output
Detected camps: [{'blue', 'pink', 'grey'}]
Detected casualties: 13

Camp priority scores:
blue: 10
pink: 6
grey: 6

Rescue Ratio (Pr): 1.69
🚀 How to Run
1. Install dependencies
pip install opencv-python numpy
2. Run the script
python triage.py
3. Input
Place your image inside:
/task_images/1.png
📁 Project Structure
├── task_images/
│   └── 1.png
├── triage.py
└── README.md
🔥 Highlights
Combines vision + decision-making
Handles real-world constraints
Simulates autonomous rescue planning
Modular pipeline (easy to extend)
🧩 Future Improvements
Replace heuristics with ML/DL models
Use Hungarian Algorithm / Linear Programming
Real-time processing (video input)
Integration with drone navigation systems
GPU acceleration
💡 Project Motivation

This project explores how visual perception + algorithmic reasoning can be combined to build systems capable of making critical real-world decisions, such as disaster response and resource allocation.

📬 Author

Vaatsalya Srivastava
