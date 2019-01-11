---
title: The score is 9 - some fun with Computer Vision in Python
date: 2018-02-02 21:57:50
mathjax: true
tags:
  - Python CV OpenCV
categories:
  - Computer Vision
  - Python
---

As I love playing darts, especially in summer, I often thought about some automatic counting system. 
Of course, the easiest way would be just buying an electronic darts board, but for a steel darts player this is not an option.
Second approach would be some fancy laser scanning hacking or building circuits into the dart board.
But I'm not that familiar with building circuits and laser scanning is really prone to environmental influences.
And to be onest, locating the arrow with a well positioned laser scanner would be too easy.
![](/images/dart-14.png)
We are goint to take the rocky road and try our luck with a visual approach..

<!-- more --> 

Visual approach means that our input is a camera recorded video. 
Thus, The first thing we need is a video...

{% raw %}
<div id="ytplayer"></div>

<script>
  // Load the IFrame Player API code asynchronously.
  var tag = document.createElement('script');
  tag.src = "https://www.youtube.com/player_api";
  var firstScriptTag = document.getElementsByTagName('script')[0];
  firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);

  // Replace the 'ytplayer' element with an <iframe> and
  // YouTube player after the API code downloads.
  var player;
  function onYouTubePlayerAPIReady() {
    player = new YT.Player('ytplayer', {
      height: '360',
      width: '640',
      videoId: '3GUDw6yr9NM'
    });
  }
</script>
{% endraw %}

I want to thank Jacob D. Delaney for his very shiny work, which inspired me with some useful tricks. 
You can find a copy of his project work [here](https://web.stanford.edu/class/ee368/Project_Autumn_1516/Reports/Delaney.pdf).

## The setup 
- Python 3.5
- OpenCV for Python


***If you want to have a deeper look into the code, a good starting point might be the [IPython Notebook](https://github.com/matherm/matherm.github.io/tree/master/assets/code/dart/dart.ipynb)***

This can be launched locally with Python and Jupyter:
```bash
jupyter notebook
```

_The full project can be found [here](https://github.com/matherm/matherm.github.io/tree/master/assets/code/dart)_
_(Please note that this is not likely to run as the project is messed up a bit)_

## The starting point

The first we need to to is reading an image from camera. This can be easily done with the following code:
```Python
# /dart.py

IM,BASE_FRAME_GRAY = Image_Tools.readImage('./images/vid2.png',(1080,1920))
IM2,BASE_FRAME_GRAY2 = Image_Tools.readImage('./images/vid3.png',(1080,1920))
GUI.imShow(IM)
```
![](/images/dart-1.png)
You might wonder what these nasty yellow post-its are doing. We'll come to this later in the post _(Hint: Orientation)_

## The dart board

In the second step I want to find my region of interest i.e. the dart board. There are various ways to do thi, but the most intuitive way might be using some kind of a template and search the image space for it.
But we will take a different technique and search for red and green pixels.

```Python
# /utils/dartboard_detector.py

    def detectDartboard(self,IM):
        IM_blur = cv2.blur(IM,Dartboard_Detector.ENV['DETECTION_BLUR'])
        #convert to HSV
        base_frame_hsv = cv2.cvtColor(IM_blur, cv2.COLOR_BGR2HSV)
        # Extract Green
        green_thres_low = int(Dartboard_Detector.ENV['DETECTION_GREEN_LOW'] /255. * 180)
        green_thres_high = int(Dartboard_Detector.ENV['DETECTION_GREEN_HIGH'] /255. * 180)
        green_min = np.array([green_thres_low, 100, 100],np.uint8)
        green_max = np.array([green_thres_high, 255, 255],np.uint8)
        frame_threshed_green = cv2.inRange(base_frame_hsv, green_min, green_max)
        #Extract Red
        red_thres_low = int(Dartboard_Detector.ENV['DETECTION_RED_LOW'] /255. * 180)
        red_thres_high = int(Dartboard_Detector.ENV['DETECTION_RED_HIGH'] /255. * 180)
        red_min = np.array([red_thres_low, 100, 100],np.uint8)
        red_max = np.array([red_thres_high, 255, 255],np.uint8)
        frame_threshed_red = cv2.inRange(base_frame_hsv, red_min, red_max)
        #Combine
        combined = frame_threshed_red + frame_threshed_green
        ...
```
As a result we get our region of interest.
![](/images/dart-2.png)

## Waiting for changes

When we have our region of interest we can start monitoring the video stream for changes. 
This is typically done through computing difference images.

```Python
# /utils/difference_detector.py

    def computeDifference(self,grey1,grey2):
        # blur
        blur = Difference_Detector.ENV['BLUR']
        grey2 = cv2.blur(grey2,blur)
        grey1 = cv2.blur(grey1,blur)
        #normalize
        grey1 = cv2.equalizeHist(grey1)
        grey2 = cv2.equalizeHist(grey2)
        clahe = cv2.createCLAHE(Difference_Detector.ENV['CLAHE_CLIP_LIMIT'], Difference_Detector.ENV['CLAHE_TILE_SIZE'])
        #clahe
        grey1 = clahe.apply(grey1)
        grey2 = clahe.apply(grey2)
        #diff
        diff = cv2.subtract(grey2,grey1) + cv2.subtract(grey1,grey2)
        ret2,dif_thred = cv2.threshold(diff,Difference_Detector.ENV['BINARY_THRESHOLD_MIN'],Difference_Detector.ENV['BINARY_THRESHOLD_MAX'],cv2.THRESH_BINARY)
        return dif_thred,grey1,grey2,diff
```

The result of the detection looks like this:
![](/images/dart-3.png)
![](/images/dart-4.png)

## Detecting arrows

Now, we know that the video has changed. The obvious next step is to locate the arrow within the image.
With the API this can be easily done by the following lines of code.

```Python
# /dart.py

arrow_detector = Arrow_Detector()
IM_arrow_closed,arrow_x1,arrow_y1,xxx,yyy,www,hhh, line_image,apex_image = arrow_detector.detectArrow(IM_ROI_difference,IM_ROI2_grey)
GUI.imShow(apex_image)
GUI.imShow(IM_arrow_closed)H_BINARY)
        return dif_thred,grey1,grey2,diff
```
![](/images/dart-5.png)
![](/images/dart-6.png)

A bit more difficult (maybe the most difficult thing within this project at all) is to find the apex of an arrow.
Depending on the resolution and light condition the apex is even invisible to humans.

I take the same approach proposed by Jacob D. Delaney and first compute a line through the hole arrow and afterwards extrapolate that line until the last pixel of the arrow is reached.

```Python
# /utils/arrow_detector.py

  def detectArrow(self,diff_image,IM_ROI2_grey):
        kernel_size = Arrow_Detector.ENV['DETECTION_KERNEL_SIZE']
        kernel = np.zeros(kernel_size,np.uint8)
        kernel_thickness = Arrow_Detector.ENV['DETECTION_KERNEL_THICKNESS']
        kernel[:,(kernel.shape[1]//2)-kernel_thickness:(kernel.shape[1]//2)+kernel_thickness] = 1
        max_contour_length,max_angle,max_contour,max_img = self.computeArrowOrientation(diff_image,range(0,180,Arrow_Detector.ENV['DETECTION_RADIAL_STEP']),kernel)
        
        if len(max_contour) == 0:
            return None, None, None, None,None,None,None,None,None,None
                
        xx,yy,ww,hh = cv2.boundingRect(max_contour)

        #Detect line of arrow
        arrow_x1,arrow_y1,line_image_peak,h,v = self._detectArrowLine(max_img,max_contour,xx,yy,ww,hh) 
        
        #Detect apex of arrow
        arrow_x1,arrow_y1,IM_apex = self._detectApex(IM_ROI2_grey,line_image_peak,arrow_x1,arrow_y1,h,v)

        return max_img,arrow_x1,arrow_y1,xx,yy,ww,hh,line_image_peak,IM_apex
```
This is very likely to fail most the times and you would need to take a more robost approach for a real system, but here it works as you can see in the following picture.

![](/images/dart-7.png)

_In a field deployment you would need to combine the information of several subsequent images and estimate the location of the apex through a state filter_

## Detect scoring zones

Until now we only know very little about the dart game itself. We only know something about an arrow and a dart board somwhere in the image. The more interessting part is the scoring zones. There are hundreds of ways to compute this, but we'll take the following simple approach:

1. Compute the orientation of the dart board
2. Compute a transformation of the dart board to a perfect plane
3. Compute the geometry of the dart board within the plane (triangles and circles of the dart board)

```Python
# /dart.py

    dartboard_detector = Dartboard_Detector()
    GUI.imShow(IM_ROI)
    IM_ROI_thres_color,IM_ROI_thres_color_closed,contours_structure = dartboard_detector.getOrientation(IM_ROI,IM_ROI_board)
    GUI.imShow(Image_Tools.debugContours(IM_ROI_thres_color,contours_structure))

    dartboard = Dartboard()
    M, src_points = dartboard.computePerspectiveTransformation(contours_structure,IM_ROI_grey,IM_ROI_red)

```
![](/images/dart-8.png)
![](/images/dart-9.png)
![](/images/dart-11.png)

Next step is transforming the whole image to the plane. The result speaks for itself:
![](/images/dart-10.png)

The last step is computing the geometry of the dart board artificially.
This can be done by some usual drawing.

```Python
# /utils/dartboard.py
    def drawDartboard(self):
        IM = np.zeros(Dartboard.ENV['DART_BOARD_TARGET_DIMENSION'],"uint8")
        offset = Dartboard.ENV['DART_BOARD_TARGET_OFFSET']
        center = (IM.shape[0] // 2,IM.shape[1] // 2)
        size_dartboard = 3400 + offset
        scale = IM.shape[0] / size_dartboard
        rad_board = int(3400 / 2 * scale)
        rad_bull = int(127 / 2 * scale)
        rad_ring = int(318 / 2 * scale)
        rad_double = int((3400 - 160) / 2 * scale)
        rad_triple = int((2140 - 160) / 2 * scale)
        width_rings = int(80 * scale)
        line_thickness = int(12 * scale)
        angle = 360 // 20 
        angle_offset = 9

        #rings
        cv2.circle(IM, center, rad_bull, (255,255,255),line_thickness)
        cv2.circle(IM, center, rad_ring, (255,255,255),line_thickness)
        cv2.circle(IM, center, rad_double, (255,255,255),line_thickness)
        cv2.circle(IM, center, rad_double + width_rings, (255,255,255),line_thickness)
        cv2.circle(IM, center, rad_triple, (255,255,255),line_thickness)
        cv2.circle(IM, center, rad_triple + width_rings, (255,255,255),line_thickness)
        
        #lines  
        line_shape = np.zeros(IM.shape,"uint8")
        line_shape[:,(line_shape.shape[1]//2)-line_thickness:(line_shape.shape[1]//2)+line_thickness] = 255
        IM_temp = np.zeros(IM.shape,"uint8")
        for i in range(0,360,angle):
            line_shape_rot = Image_Tools.rotateImage(line_shape,i + angle_offset)   
            IM_temp = IM_temp + line_shape_rot
        
        #restore bull
        IM_mask = np.zeros(IM.shape,"uint8")
        cv2.circle(IM_mask, center, rad_board, (255,255,255),-1)
        cv2.circle(IM_mask, center, rad_ring, (0,0,0),-1)
        IM = IM + (IM_temp * IM_mask)
        
        #create Mask
        IM_mask = np.zeros(IM.shape,"uint8")
        cv2.circle(IM_mask, center, rad_board, (255,255,255),-1)
        
        #make color
        IM_color = np.repeat(IM[:, :, np.newaxis], 3, axis=2)    
        return IM_color, IM_mask
```
The code produces the follwing digital dart board.
![](/images/dart-12.png)

## Putting it all together

Last but not least our initial task was to find out where the arrow has landed and compute the resulting score.
Until know we have all the parts together and simply need the final step: Simply apply the same transformation of the dart board to the previously computed apex location.


```Python
# /dart.py

arrow_detector = Arrow_Detector()
GUI.imShow(IM_ROI_ROTATED)
cx,cy,angle,length,cross,IM_dot,IM_line = arrow_detector.getMetricOfArrow(IM_ROI_ROTATED)
GUI.imShow(IM_dot)
```

The result looks like this:
![](/images/dart-13.png)


## Making some beautiful output

As we all like visuality and beatiful outputs. Our very last (optional) step is to compute such an output


```Python
# /dart.py

score = dartboard.calcScore(angle,length)
dartboard = Dartboard()
IM_score = dartboard.drawScore(IM_final1,score)
GUI.imShow(IM_score)
```
And here we have the final result.
***The score is 9!!***

![](/images/dart-14.png)

_Please let me know if you enjoyed the post or have any improvements. I really apperciate [sic!] reported typos and failures, too._

