# Imitation Learning

## Introduction

In imitation learning a [simulation engine](https://github.com/udacity/self-driving-car-sim) is used to create training datasets.  A screenshot of the simulator for the first track is shown below:

![udacity-simulator](images/udacity-simulator.png)

A convolution neural network was developed using the high level deep learning API Keras based on a Tensorflow backend.  **This network predicts steering angles from images.**

## Model Architecture and Training Strategy

The model was based on [NVIDIA's work](http://arxiv.org/abs/1604.07316) with two preprocessing stages.  The original NVIDIA model  is shown in the figure below:

![nvidia-model](images/nvidia-model.png)

and except from the normalization layer it consists of five convolutional and five flat layers. 

The model was modified as follows:

1. The preprocessing involved cropping the input images by 30 lines and 20 lines in the top and bottom of all collected images respectively.  This was done to eliminate unnecessary for the problem image content. 

2. Batch normalization for the resulting cropped images was then performed. 

```python
   model.add(Cropping2D(cropping=((50, 20), (0, 0)), input_shape=(160, 320, 3)))
   model.add(BatchNormalization(epsilon=0.001, axis=3, input_shape=(90, 320, 3)))
```

The complete model is shown in Keras API below

```python
def nvidia_model():

    model = Sequential()

    model.add(Cropping2D(cropping=((50, 20), (0, 0)), input_shape=(160, 320, 3)))
    model.add(BatchNormalization(epsilon=0.001, axis=3, input_shape=(90, 320, 3)))

    model.add(Conv2D(24, (5, 5), padding='valid', activation='relu', strides=(2, 2)))
    model.add(Conv2D(36, (5, 5), padding='valid', activation='relu', strides=(2, 2)))
    model.add(Conv2D(48, (5, 5), padding='valid', activation='relu', strides=(2, 2)))
    model.add(Conv2D(64, (3, 3), padding='valid', activation='relu', strides=(1, 1)))
    model.add(Conv2D(64, (3, 3), padding='valid', activation='relu', strides=(1, 1)))
    model.add(Flatten())
    model.add(Dense(1164, activation='relu'))
    model.add(Dense(100, activation='relu'))
    model.add(Dense(50, activation='relu'))
    model.add(Dense(10, activation='relu'))
    model.add(Dense(1, activation='tanh'))

    return model
```

The model was trained and validated on different data sets to ensure that the model was not over-fitting. 

## Datasets

The training datasets represent in our use case, **the correct driving behavior**.  The dataset collection strategy adopted was as follows:

 1. Initially three complete rounds of track-1 where the vehicle stayed as much as possible in the center of the road were recorded. 
 2. Subsequently the car was positioned such that it faced track-1 in the reverse direction and another three complete rounds of track-1 where recorded. 
 3. In selected turns, the car was positioned in orientations that recovery actions would be taken and the recoveries recorded. Note that only the recoveries 
 where recorded - we have not recorded the deviations from the center of the road as we wanted to teach the network how to recover not how to enter in challenging situations.   

For images were collected in BGR color space and were augmented via flipping each image as shown below. 

```python
images = []
augmented_images = []
measurements = []
augmented_measurements = []
for directory in drive_dirs:
    print(directory)
    with open(os.path.join(root_data_dir, directory, 'driving_log.csv')) as csvfile:
        reader = csv.reader(csvfile)
        for line in reader:
            # use all available cameras
            for camera in range(num_cameras):
                # the following line uses separator for simulator data collected in OSX
                filename = line[camera].split('/')[-1]
                # image is in BGR color space (default of cv.imread)
                image_bgr = cv2.imread(os.path.join(root_data_dir, directory, 'IMG/', filename))
                image_rgb = cv2.cvtColor(image_bgr, cv2.COLOR_BGR2RGB)
                images.append(image_rgb)
                measurements.append(float(line[3]))

# augmentation
for image, measurement in zip(images, measurements):
    augmented_images.append(image)
    augmented_images.append(cv2.flip(image, 1))
    augmented_measurements.append(measurement)
    augmented_measurements.append(measurement*(-1.0))

```

The original (top) and flipped (bottom) images are shown below. 

![original-image](images/original-image.png)
![augmented-image](images/augmented-image.png)

Cropping was applied to both images as described above. In total 5882 original images resulted in 11764 images after augmentation. With 20% validation set size, this meant 9411 images that were  used for training and 2353 images used for validation. The model used an adam optimizer, so the learning rate was not tuned manually. 

The car was then test driven by the Convolutional Neural Network (CNN) autonomously - without any human intervention. The car successfully drives 
around track one without leaving the road as shown in the video below. 

[![Imitation Learning](https://img.youtube.com/vi/1dBLLB2qasM/0.jpg)](https://www.youtube.com/watch?v=1dBLLB2qasM)

*Imitation Learning*



