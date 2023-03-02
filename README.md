# ANPL
There is three main step for detecting persian lisence plate:
- train yolov7 with persian license plate dataset for object detection
- crop and pre processing object detected from yolo
- reading lisence plate
## yolov7
in this step we need to train last layers of pre trained yolov7 because coco dataset that yolo trained with dont exist of lisence plates and for better performance we use persian lisence plate dataset.

unfortunatly i didnt found good and enought dataset so i merg 2 dataset together and make a data set with 1000 picture of lisence plates in persian(because roboflow free account limit is 1000 image).problem here is that label of each dataset is diffren so we should rename the labels and make simillar label for 2 datasets we merged for this part i used the code bellow for changing label of annotation files:
```python
from glob import glob
import pandas as pd
from pathlib import Path
for j in range (313):
    path = pd.DataFrame(glob('*'))
    path.columns=['location']
    z=path['location'].iloc[2*j+1]
    a=[]
    with open(z, "r") as f , open(fr'E:/dataset-car-plate/Vehicle Plates/Vehicle Plates/newlabels/{z}','w') as f2:
        a = f.read()
        x= a.replace("vehicle plate", "car")
        f2.write(x)
        f.closed
        f2.closed
```
now we have datasets for train yolov7. code for training available in [objectdetection.ipynb](objectdetection.ipynb).
