# Devanagari-Character-Recognition
This is a brief summary of the Devanagari character recognition project.
To my knowledge, apart from the students who took the machine learning course in semester 1 2017-18 at my institute, nobody has worked on this exact problem with the same/similar dataset. Devanagari OCR is still a highly challenging problem when the dataset contains noise.

The Dataset

Eight pages from a very old book written in the Sanskrit language were photographed. Bounding boxes were manually drawn around every character and an automated script would then create a separate photo of the bounding box. The character present in this and the accents were also manually identified, and this data was stored using unicode in python. Thus, each photo had one character, and 0 - 4 accents. If joint characters were encountered, both the characters were considered.

Pre-processing the data

The dataset is a set of 2,949 RGB images, containing one or two characters and 0-3 accents in them. Pre-processing included two steps:

    Binarizing the images to Black and White using Otsu's method.
    Padding each image to 216x216 resolution (the largest image was of 190x182 resolution), and then resizing to 100x100.

Network Architecture

Conv1 : 3x3x1 convolution , 16 filters, zero-padding : yes (done for all conv layers) Activation : ReLU max_pool : false

Conv2 : 3x3x1 convolution, 32 filters Activation : ReLU max_pool : true, (2x2)

Conv3 : 3x3x1 convolution, 64 filters Activation : ReLU max_pool : false

Conv4 : 3x3x1 convolution, 128 filters Activation : ReLU max_pool : true, (2x2)

Dense layer 1 : 512 units Activation : ReLU dropout : 0.5

Readout layer : 128 units (128 classes)Activation : sigmoid

Optimizer used for training : Adam, with learning rate 10^(-2)

Training and Results

Trained for 5 epochs on a NVIDIA 940M GPU.
Accuracy on the test set : 52%
