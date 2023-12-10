# **2023.11.27-12.1**

#### **New night mode**

1. Our existing day/night switching method didn't work well in the Shandong case. I've studied the following methods with 24-hr video data (Note: by eye inspection, camera 206&207 need to switch to the night mode at night due to the significant noise)

   1. luminance threshold. Can't distinguish 206/207 from the other cameras.
     ![image-20231210145612115](reports.assets/image-20231210145612115.png)

   2. Color saturation. Better but still not working.

      ![image-20231210150056284](reports.assets/image-20231210150056284.png)

   3. Red-channel difference between two adjacent frames. It works! (the threshold is around 30)

      ![image-20231210150442602](reports.assets/image-20231210150442602.png)

2. Cameras switch between day/night modes frequently when it's dawn and dusk. I added a 5-min time interval to smooth the curve and solved the problem.

#### New text look

1. Added white strokes to texts so that they can be more clearly seen. Removed the white background of texts.
2. Use relative positions and fontsizes. Text display won't change when vis images are rescaled.
3. Modified the text-related parameters in detectors.json so that they are fewer and cleaner.

​	Old look

<img src="reports.assets/image-20231210150603167.png" alt="image-20231210150603167" style="zoom: 33%;" />

​	New look

<img src="reports.assets/image-20231210150638080.png" alt="image-20231210150638080" style="zoom:33%;" />

#### Debug: ir video display issue

Issue: when in night mode, the displayed ir image looks unnatural. The light distribution isn't continueous.

Solution: found that the pixel values are truncated when converting from 16-bit to 8 bit. Fixed it.

Old look