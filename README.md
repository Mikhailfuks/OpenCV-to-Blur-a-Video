#include <opencv2/opencv.hpp>
#include <iostream>

using namespace cv;
using namespace std;

int main(int argc, char** argv) {
    // Open the default camera (0). You can replace 0 with a video file path if needed.
    VideoCapture capture(0);
    if (!capture.isOpened()) {
        cout << "Error: Could not open camera." << endl;
        return -1;
    }

    Mat frame, blurredFrame;

    // Create a window to display the results
    namedWindow("Blurred Video", WINDOW_AUTOSIZE);

    while (true) {
        // Capture frame-by-frame
        capture >> frame;
        if (frame.empty()) {
            cout << "Error: No frame captured." << endl;
            break;
        }

        // Apply Gaussian blur to the frame
        GaussianBlur(frame, blurredFrame, Size(15, 15), 0);
        
        // Show the blurred frame
        imshow("Blurred Video", blurredFrame);

        // Exit if the user presses 'q'
        if (waitKey(30) >= 0) {
            break;
        }
    }

    // Release the camera and destroy windows
    capture.release();
    destroyAllWindows();
    return 0;
}
