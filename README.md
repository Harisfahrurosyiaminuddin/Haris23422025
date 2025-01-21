1. # Step 1: Install necessary libraries!pip install ultralytics  # Install YOLOv8
!pip install matplotlib opencv-python-headless!pip install roboflow
2. # Step 2: Import libraries
import matplotlib.pyplot as pltfrom ultralytics import YOLO
from google.colab import filesimport cv2
import numpy as np
3. !pip install roboflow
from roboflow import Roboflowrf = Roboflow(api_key="p9AE4cfyWZVtKr7MenmF")
project = rf.workspace("uasdeteksi").project("mobil-chseg")version = project.version(1)
dataset = version.download("yolov8")
4. !pip install roboflow
from roboflow import Roboflowrf = Roboflow(api_key="p9AE4cfyWZVtKr7MenmF")
project = rf.workspace("uasdeteksi").project("mobil-chseg")version = project.version(1)
dataset = version.download("yolov8")
5. import os
# Lihat folder tempat dataset diunduhdataset_location = dataset.location  # dari RoboFlow download
print("Dataset downloaded to:", dataset_location)
6. from ultralytics import YOLO
# Buat model YOLOv8 baru
model = YOLO("yolov8n.pt")  # "yolov8n.pt" adalah versi YOLOv8 Nano
# Jalankan pelatihan dengan datasetmodel.train(data="/content//mobil-1/data.yaml", epochs=3, imgsz=640)
7. dataset = version.download("yolov8")
8. result = model.predict(source="/content/mobil-1/valid/images", save=True, imgsz=640)
9. # Ambil elemen pertama dari hasil prediksi
image_result = result[0]
# Menampilkan hasil deteksi
from IPython.display import Image, displayimage_path_with_predictions = image_result.plot()  # Mengembalikan array gambar
# Tampilkan menggunakan Matplotlib
import matplotlib.pyplot as pltplt.imshow(image_path_with_predictions)
plt.axis("off")plt.show()
10. # Step 3: Upload image
uploaded = files.upload()image_path = list(uploaded.keys())[0]
11. # Step 4: Load YOLO model
model = YOLO('yolov8n.pt')  # Use a pre-trained YOLOv8 model (nano version for speed)
12. # Step 5: Perform object detectionresults = model(image_path)  # Run inference on the uploaded image
13.  # Step 6: Visualize results
# Save the annotated imageannotated_img = results[0].plot()  # Create an annotated image (numpy array)
14. # Display the annotated image using matplotlib
plt.figure(figsize=(10, 10))plt.imshow(cv2.cvtColor(annotated_img, cv2.COLOR_BGR2RGB))
plt.axis("off")plt.title("YOLO Detected Objects")
plt.show()
