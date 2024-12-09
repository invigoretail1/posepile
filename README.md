# PosePile

This is a large collection of dataset processing (and benchmark evaluation) scripts for image-based 3D human pose estimation, as used in the paper 

**Learning 3D Human Pose Estimation from Dozens of Datasets using a Geometry-Aware Autoencoder to Bridge Between Skeleton Formats** \
István Sárándi, Alexander Hermans, Bastian Leibe \
Winter Conference on Applications of Computer Vision (WACV), 2023

The repo is structured as follows. Each dataset has its own directory under `posepile/ds/$dataset_name`. Within each directory there is a main bash script `main.sh` listing the processing steps, and typically a `main.py` which is called from bash with various arguments. There can also be additional scripts in the directory, depending on the dataset and the processing steps needed. Corresponding benchmark evaluation scripts are named `eval.py` in the same directory for the most common ones.

Typically, the preprocessing consists of downloading and extracting the dataset, camera calibration processing, person detection, person segmentation, adaptive selection of frames with enough motion, generation of smaller-resolution image crops and putting it all into a common format (`posepile.datases3D.Pose3DDataset` and `posepile.datases3D.Pose2DDataset`).

Running the preprocessing for all 28 datasets (as described in the paper referenced below) takes very long. The end result is 13 million image crops with corresponding annotations. The images in JPEG format take up around 1 TB of space, while the annotations (including masks stored in RLE format) take up about 20 GB. For more convenient use of this large data, the [Barecat](https://github.com/isarandi/Barecat) library can be used to store it in sharded archives that support fast random access during training, without high memory usage or having many small files.

Unfortunately, redistribution of the processed data is not possible due to the license terms of the original datasets (except for ASPset, which is in the public domain, and hence may be released here as an example in the future).

## Reference

Please consider citing the following paper if this code helps your research (along with any of the original dataset papers you use):

```bibtex
@inproceedings{Sarandi2023dozens,
    author = {S\'ar\'andi, Istv\'an and Hermans, Alexander and Leibe, Bastian},
    title = {Learning {3D} Human Pose Estimation from Dozens of Datasets using a Geometry-Aware Autoencoder to Bridge Between Skeleton Formats},
    booktitle = {IEEE/CVF Winter Conference on Applications of Computer Vision (WACV)},
    year = {2023}
} 
```
