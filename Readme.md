This is my attempt to implement a semantic segmentation network on darknet framework.

I implement a modified version of U-Net (https://arxiv.org/abs/1505.04597) to detect road surface.

Input to model: 224 x 224 x 3 images

Output: 224 x 224 binary label

I added a bunch of code to the darknet source files for data pre processing.

I recommend using cscope to browse through the code, makes life easier!

Sample data to train and test can be found in data/unet folder. (Note that I have only added 5 pairs of images to get you started)

The main program that I implemented is unet_segmenter.c please browse through the code to understand it.

Inorder to run this version of darknet for unet segmentation you need to build the code using makefile build system and then run:

./darknet unet_segmenter train unet.data unet.cfg

Also kindly note that you need to update the train.list and labels.list to reflect the path to the train and labels folder on your local file system.

With the provided samples the network will not train completely as the train size is too small just 5 images. You need to add your own data in the same format as per the samples provided.

Once successfully trained the weights file will be saved under the name unet.backup under the main folder. Then you can run the prediction by using this command:
./darknet unet_segmenter test

I have uploaded my trained weights file under the main folder so you can directly test it.

Feel free to adapt the code to your needs.

**Notes:**
The input images have to be reshaped to 224x224x3 (RGB) and the output label is a binary image (0's & 1's) as I only predict one class. If you want to use a different size image or multi-class prediction you need to the change the shape of input and output layer accordingly in the config file.

I normalize the image channel-wise using the mean for each channel, if you want use different normalization you have to the change the **ipl_into_image** function in the src/image.c file.

All the Unet specific code that I added to darknet has been commented with "Unet code" so you can easily track the changes.

Cheers!


Sample:

![input image](data/unet/test/5.png)
![output image](data/unet/result/5.png.png)
