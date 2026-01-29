# UAS-DTU-Submissions
My- Main File 
It consists of parts such as : 
1. My pratice Jupyter Nb of Py3 ( I wrote all the codes by my hand after understanding each line just to make sure I properly understand the working of the whole program and each keyword )
2. My pratice Jupyter Nb of Open CV ( again I wrote all the codes myself )
3. i)Proj1( OpenCV ) ---->>>> Air Sketch ( First I wrote the code while taking help from the youtube tutorial and then later after encountering bugs fixed up them by taing help from docs and other sources )
   ii)Proj2( OpenCV ) ---->>>> Doc Scanner
   iii)Proj3( OpenCV ) ---->>>> LicensePlate Scanner 
4.My NumPy pratice file  
5. Triage ---> This project implements triage system using computer vision it is about detecting rescue camps and casualties from a map image assigning priorities based on severity and computing a rescue ratio to evaluate effectiveness
     The main workflow I decide was :
   
   1)Camp Detection
   i)Camps are detected using HSV color segmentation.
   ii)Only the largest contour per camp color is retained to avoid background misclassification (e.g., ocean regions).
   iii)Each camp is assigned a predefined capacity.

   2)Casualty Detection
   i)The image is binarized using adaptive thresholding to preserve low-contrast symbols.
   ii)Connected component analysis is used to detect casualty symbol fragments.
   iii)To prevent overcounting, spatially close components are merged using distance-based clustering.
   iv)Each cluster represents one casualty.

   3)Priority Assignment
   i)Casualty priority is assigned heuristically based on cluster size.
   ii)Larger clusters indicate higher severity.

   4)Triage Assignment
   i)Casualties are sorted by priority.
   ii)Each casualty is assigned to the nearest camp with available capacity.​

   I had to work out the codes many times :
   
   i)lower_blue = [90, 50, 50]
     upper_blue = [140, 255, 255]
     ocean_mask = cv2.inRange(hsv, lower_blue, upper_blue)

   At first I naively used HSV blue range to detect blue camps This resulted in both camps and ocean being detected in blue it later resulted in Multiple blue camps ,Incorrect camp locations
   I fixed it by :
   Selecting the largest contour per color
   Rejecting irrelevant blue regions
   Treating camps as symbols, not background
   
   ii)edges = cv2.Canny(gray, 80, 160)
      contours = cv2.findContours(edges)

   secondly I detected casualties via edges + contours but this had a problem , One casualty symbol = many edge contours this further resulted in 
   Same casualty being detected 5–8 times
   Inflated casualty count's around (30–40)
   Rescue Ratio being collapsed
   This was because Edges detect boundaries not objects
   I fixed this by :
   Switching to connected component analysis
   Treating casualties as filled blobs
   
   iii)threshold(gray, 200)
       morphologyEx(..., iterations=2)
       area filter [80–800]

   Then I tried to aggressively remove noise However his too had a lot of problems casualty symbols are light gray , Threshold was too high which resulted in symbols erased , Morphology was too aggressive which      resulted in blobs destroyed
   I later fixed this by :
   Implementing Adaptive thresholding
   relaxing morphology
   Relaxing area limits
   iv) Finally I was able to make correct camp detections but wrong counting of casualties
   because I thought Connected components correctly detected symbol fragments
   however Connected components are not equal to semantic objects
   I finally fixed it by :
   Spatial clustering:
   Group components within a radius
   One cluster is equal to one casualty
   Cluster size = priority
   This was the key conceptual leap

   In the end the main challenge was The main challenge was preventing overcounting caused by symbol fragmentation This was solved by clustering connected components spatially which aligns detections with            semantic objects rather than raw pixels
   After fixing all of these issues my code in the final notebook was running fine and was finally displaying optimal results as:
   Each detection stage is semantically aligned:
   Colors = camps
   Blobs = casualties
   Clusters = people
   Noise is handled statistically not aggressively

   
