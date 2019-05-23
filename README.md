# Oil-Tank-Volume-Estimation

Oil storage tanks play an important role in the global economy. Crude oil is stored in tanks at many points between extraction and sale. Storage 
tanks are also used by nations to stockpile oil reserves. The volume of oil in storage is an important economic indicator. It indicates which 
oil producing nations are increasing or decreasing production and gives a window into the global demand for energy. At the same time, oil storage 
information is not transparent. Nations may hide information about oil production, consumption and storage for economic or military reasons. 
For this reason, companies like [Planet](https://www.planet.com/) and [Orbital Insight](https://orbitalinsight.com/) have made a business of 
collecting satellite imagery of oil storage tanks and estimating reserve volumes.

Volume estimation is made possible by the design of storage tanks. The tanks have a floating head that sits on top of the oil. This prevents 
flammable vapors from building up. It also creates a distinctive pair of two crescent shadows:

![](https://github.com/kheyer/Oil-Tank-Volume-Estimation/blob/master/media/tanks.png)

These shadows can be extracted from the image using computer vision algorithms.

![](https://github.com/kheyer/Oil-Tank-Volume-Estimation/blob/master/media/tank_shadows.png)

The relative areas of the shadows can be used to estimate the volume of the tank.

![](https://github.com/kheyer/Oil-Tank-Volume-Estimation/blob/master/media/tank_volumes.png)

This project consists of four parts:
* 1. Dataset Creation
* 2. Tank Object Detection
* 3. Shadow Extraction and Volume Estimation
* 4. Full Processing Pipeline

# 1. Dataset Creation

Dataset creation is in progress. 100 4800x4800 RGB images of tank containing industrial regions were collected from Google Earth. Each large 
image was split into 100 512x512 tiles, for a total of 10,000 512x512 tiles. The tiles are currently in the process of being labeled with 
bounding boxes for floating head tanks.

When dataset labeling is complete, the dataset and labels will be uploaded to Kaggle.

# 2. Tank Object Detection

Once the dataset is complete, a RetinaNet model will be trained on the dataset to detect tanks in images.

# 3. Shadow Extraction and Volume Estimation

Identified tanks will be run through a computer vision algorithm to extract the crescent shadows and estimate tank volumes. The full algorithm is 
detailed in the __Shadow Extraction Algorithm__ notebook. In short, the algorithm creates an enhanced version of the tank image using 
challens from RGB and LAB color space. Shadows are extracted from the enhanced image using thresholding. The thresholded image is cleaned up 
using morphological operations. Tank shadows are extracted from the clean image and used for volume estimation.

![](https://github.com/kheyer/Oil-Tank-Volume-Estimation/blob/master/media/tank_process.png)

# 4. Full Processing Pipeline

Once all the pieces are in place, a pipeline will be created that will take in an image containing multiple tanks, localize the tanks, and 
estimate tank volumes.
