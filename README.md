# skripsi-sample
Deteksi mata uang asli dan palsu menggunakan Tensorflow

# Proses Pre-Processing pada gambar
Resize gambar
```
index_resize.py
```

Convert dataset meta labels xml to csv
```
python xml_For_csv.py
```

Convert csv dataset labels to TFRecord file format
```
python tfrecord.py --type=train --csv_input=data/trainlabels.csv  --output_path=data/train.record
python tfrecord.py --type=test --csv_input=data/testlabels.csv  --output_path=data/test.record
```

# Simpan di directory training untuk pemodelan
```
wget http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v1_coco_2018_01_28.tar.gz

```
atau bisa [clik aja](http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v1_coco_2018_01_28.tar.gz)

# Setting Konfigurasi model dan class pada object

```
wget https://github.com/tensorflow/models/blob/master/research/object_detection/samples/configs/ssd_mobilenet_v1_pets.config

```
atau bisa [clik aja](https://github.com/tensorflow/models/blob/master/research/object_detection/samples/configs/ssd_mobilenet_v1_pets.config)

# Memulai pelatihan pada model

Proses Pelatihan Berjalan
```
python train.py --logtostderr --train_dir=training/ --pipeline_config_path=training/ssd_mobilenet_v1_pets.config
```

Export graph dan Model yang telah kita latih
Proses Pelatihan Berjalan
```
python export_inference_graph.py \
    --input_type image_tensor \
    --pipeline_config_path training/ssd_mobilenet_v1_pets.config \
    --trained_checkpoint_prefix training/model.ckpt-1000 \
    --output_directory uang
```

# Buka Android Studio

clone tensorflow android repo buka folder project
```
git clone https://github.com/tensorflow/tensorflow.git
```
atau bisa [clik aja](https://github.com/tensorflow/tensorflow.git)

Install Bazel [clik aja](https://docs.bazel.build/versions/master/install.html)

Build untuk .so pada file bazel
```
bazel build -c opt //tensorflow/contrib/android:libtensorflow_inference.so 
  --crosstool_top=//external:android/crosstool
  --host_crosstool_top=@bazel_tools//tools/cpp:toolchain
  --cpu=armeabi-v7a
```

Build  Java counterpart
```
bazel build //tensorflow/contrib/android:android_tensorflow_inference_java
```

Open android studio kemudian klik  Click open the **existing project** buka direktori /tensorflow/examples/android
libtensorflow_inference.so and libandroid_tensorflow_inference_java.jar disimpan pada folder android
libandroid_tensorflow_inference_java.jar di set pada **Add As Library**

libtensorflow_inference.so diset pada **Link C++ Project with Gradle** kemudian pilih  CMake.txt

Kemudian Run Project









