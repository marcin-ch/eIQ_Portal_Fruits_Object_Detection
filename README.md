# Overview
This is guide how to create eIQ Portal project (`*.eiqp`) for object detection purposes using custom VOC-type dataset.

# Dataset
The dataset can be found [here](https://www.kaggle.com/mbkinaci/fruit-images-for-object-detection). The dataset contains fruit images (apple, banana, orange and mixed) in `*.jpg` format and corresponding annotations in `*.xml` format. Annotations are in Pascal VOC format. For training there are 240 images and for testing 60 images. For this guide the dataset has been used "AS-IS" without any changes to its content.

# Workflow
This guide assumes you want to create your eIQ Portal project in `C:\eIQ_workspace\fruits_object_detection` (however, it is up to you)
1. Go to your eIQ Portal project directory
2. Download here the dataset (account is required) and unzip
3. Create two folders: `dataset_fruits_train` and `dataset_fruits_test`
    * in each folder create two subfolders: `Annotations` and `JPEGImages`
4. Copy images and annotations from downloaded dataset to newly created folders and subfolders according to rules:
    * train images to `dataset_fruits_train\JPEGImages` and train annotations to `dataset_fruits_train\Annotations`
    * test images to `dataset_fruits_test\JPEGImages` and test annotations to `dataset_fruits_test\Annotations`
5. Compress `dataset_fruits_train` and `dataset_fruits_test` into two corresponding TAR files
    * if you use 7-Zip: right mouse click on folder -> choose `7-Zip` -> `Add to archive` -> `Archive format` choose `tar` -> hit `OK`
    * you get `dataset_fruits_train.tar` and `dataset_fruits_test.tar`
6. Run eIQ Portal and hit `COMMAND LINE`
    * in opened console change current directory to your eIQ Portal project directory:
    ```
    cd C:\eIQ_workspace\fruits_object_detection
    ```
    * run importer for training dataset
    ```
    deepview-importer.exe -group train -truncated -project fruits_object_detection.eiqp dataset_fruits_train.tar
    ```
    * run importer for testing dataset
    ```
    deepview-importer.exe -group test -truncated -project fruits_object_detection.eiqp dataset_fruits_test.tar
    ```
    * `-truncated` causes the importer to include annotations flagged as truncated (without that option images where corresponding annotations have been marked as `<truncated>1</truncated>` have not been imported)
    * `-project` name remains the same
7. Go back to eIQ Portal and hit `OPEN PROJECT`
    * choose newly created project `fruits_object_detection.eiqp` and explore

> **Additional info**
> * Based on **eIQ Toolkit User's Guide** available after eIQ Toolkit installation in `eIQ_Toolkit_install_dir\docs\eIQ_Toolkit_UG.pdf` (especially section **5.2.2 Importing custom VOC-type datasets**)