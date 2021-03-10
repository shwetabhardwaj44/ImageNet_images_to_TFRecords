# ImageNet_Images_to_TFRecords
This repository converts the raw .JPEG images in ImageNet data to TFRecord files format.
* ``python build_tfrecords_from_images.py &> output``

# Dataset:
Raw image files are located in following directory structure:
- train/n01440764/images/n01440764_0.JPEG
- train/n01440764/images/n01440764_1.JPEG

where 'n01440764' is the unique synset label associated with these images.

- Tiny ImageNet: All images are 64x64 colored ones.
- The training data set consists of 200 sub-directories (i.e. labels) each containing 500 JPEG images for a total of 100000 JPEG images.
- The validation set contains 10,000 images.

# Utility of Script:
- This TensorFlow script converts the training data into a sharded dataset consisting of 100 TFRecord files.
- The same code can be used for validation set also.
- Each record within the TFRecord file is a serialized Example proto. The Example proto contains the following fields:
    - image/encoded: string containing JPEG encoded image in RGB colorspace
    - image/height: integer, image height in pixels
    - image/width: integer, image width in pixels
    - image/colorspace: string, specifying the colorspace, always 'RGB'
    - image/channels: integer, specifying the number of channels, always 3
    - image/format: string, specifying the format, always 'JPEG'
    - image/filename: string containing the basename of the image file, e.g. 'n01440764_10026.JPEG'.
    - image/class/label: integer specifying the index in a classification layer. The label ranges from [1, 200] (Tiny ImageNet) and [1, 1000] (ImageNet).
    - image/class/synset: string specifying the unique ID of the label, e.g. 'n01440764'
    - image/class/text: string specifying the human-readable version of the label, e.g. 'red fox, Vulpes vulpes'
    
   Note: This script supports ImageNet-1000 dataset. Running this script using 100 threads may take around ~2 minutes on Tiny-ImageNet on a macOS 10.14.6.
