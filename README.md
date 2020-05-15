# SFND 2D Feature Tracking

<img src="images/keypoints.png" width="820" height="248" />

The idea of the camera course is to build a collision detection system - that's the overall goal for the Final Project. As a preparation for this, you will now build the feature tracking part and test various detector / descriptor combinations to see which ones perform best. This mid-term project consists of four parts:

* First, you will focus on loading images, setting up data structures and putting everything into a ring buffer to optimize memory load. 
* Then, you will integrate several keypoint detectors such as HARRIS, FAST, BRISK and SIFT and compare them with regard to number of keypoints and speed. 
* In the next part, you will then focus on descriptor extraction and matching using brute force and also the FLANN approach we discussed in the previous lesson. 
* In the last part, once the code framework is complete, you will test the various algorithms in different combinations and compare them with regard to some performance measures. 

See the classroom instruction and code comments for more details on each of these parts. Once you are finished with this project, the keypoint matching part will be set up and you can proceed to the next lesson, where the focus is on integrating Lidar points and on object detection using deep-learning. 

## Dependencies for Running Locally
* cmake >= 2.8
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1 (Linux, Mac), 3.81 (Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* OpenCV >= 4.1
  * This must be compiled from source using the `-D OPENCV_ENABLE_NONFREE=ON` cmake flag for testing the SIFT and SURF detectors.
  * The OpenCV 4.1.0 source code can be found [here](https://github.com/opencv/opencv/tree/4.1.0)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools](https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory in the top level directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./2D_feature_tracking`.

### Performance
#### MP.7 Performance Evaluation 1
Number of detected keypoints for each detector on the preceding vehicle for total of 10 images
| Detector | Number of detected Keypoints |
| --- | --- |
| SHITOMASI | 1189 |
| HARRIS | 1084 |
| FAST | 4136 |
| BRISK | 2714 |
| ORB | 1150 |
| AKAZE | 1655 |
| SIFT | 1371 |
#### MP.8 Performance Evaluation 2
The number of matched keypoints for all 10 images using all possible combinations of detectors and descriptors
| Detector\Descriptor | BRISK | BRIEF | ORB | FREAK | AKAZE | SIFT |
| --- | --- | --- |--- |--- |--- |--- |
|**SHITOMASI**	|771|	953|914	|768|	N/A	|928|
|**HARRIS**	|393	|423|	412	|443|	N/A|	409|
|**FAST**|	2248	|2924|	2869	|2284|	N/A|	2805|
|**BRISK**	|1563|	1805	|1496	|1518	|N/A|	1620
|**ORB**|	753	|576|	757	|438|	N/A|	763|
|**AKAZE**	|1206|	1322|	1186|	1183|	1249	|1263|
|**SIFT**	|602|	751|	Out of Memory	|626|	N/A	|820|

#### MP.9 Performance Evaluation 3
Average Processing Time (ms) on all images for each detector/descriptor combination
| Detector\Descriptor | BRISK | BRIEF | ORB | FREAK | AKAZE | SIFT |
| --- | --- | --- |--- |--- |--- |--- |
|**SHITOMASI**|	601.261|	25.3585|	34.3536|	104.04|	N/A|	63.8929|
|**HARRIS**	|564.416|	28.8252|	35.3673|	103.321|	N/A|	59.392|
|**FAST**|	554.408|	11.0708|	17.3062|	88.828|	N/A|	75.9405|
|**BRISK**	|1174.21|	616.871|	645.412|	691.046|	N/A|	702.332|
|**ORB**|547.948|	20.8855|	50.7708|	100.113|	N/A|	112.002|
|**AKAZE**|	745.616|	215.533|	232.859|	286.765|	344.428|	257.345|
|**SIFT**	|762.529|	227.408|	Out of Memory	|326.65|	N/A|	343.704|


#### TOP 3 suggestion
Given that we are not looking into the correctness of matched points, I rank the performance mainly based on processing time.
The combination that runs faster while getting fairly good amount of matched points is ranked higher.
Top 3 combinations are ranked as following:
|Rank |Combination  | 	Processing Time(ms) | Matched Points|
| --- |--- | --- | --- |
|1 |FAST/BRIEF|	161	|2924				|
|2 |ORB/BRIEF|	77	|2869				|
|3 |HARRIS/BRIEF	|91	|757|