#include <opencv2/highgui/highgui.hpp>
#include <opencv2/imgproc/imgproc.hpp>
#include <iostream>

using namespace cv;
using namespace std;

Mat rotate(Mat src, double angle){
    Mat dst;
    Point2f pt(src.cols/2., src.rows/2.); // It Points to the Center of the Image
    Mat r = getRotationMatrix2D(pt, angle, 1.0); // 1 denotes original size
    warpAffine(src, dst, r, Size(src.cols, src.rows));
    return dst;
}

int main(){
    string imgname;
    double ang;
    Mat src, dst;

    cout << "Enter the Path of the Image followed by Extension: ";
    cin >> imgname;
    src = imread(imgname, CV_LOAD_IMAGE_UNCHANGED); // Reading the Image
    cout << "Enter the angle of Rotation: ";
    cin >> ang;
    
    dst = rotate(src, ang);

    // Show the Original Image
    const char* pzOriginalImage = "Original Image";
    namedWindow(pzOriginalImage, CV_WINDOW_AUTOSIZE);
    imshow(pzOriginalImage, src);
    
    // Show the Rotated Image
    const char* pzRotatedImage = "Rotated Image";
    namedWindow(pzRotatedImage, CV_WINDOW_AUTOSIZE);
    imshow(pzRotatedImage, dst);

    waitKey(0);
    return 0;
}
