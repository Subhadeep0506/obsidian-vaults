Automatic detection of plant diseases is an important research topic as it may prove beneficial in monitoring large fields of crops, and thus automatically detect the diseases from the symptoms that appear on the plant leaves. This enables machine vision that is to provide image-based automatic inspection and process control. Comparatively, visual identification is labour intensive, less accurate and extremely time-consuming tedious task. When scouting the field, instant identification saves the need to waste time on identifying the problems and recording the results. 

So, in this article we will explore how can we avoid the laboring task of identifying plant diseases and automate the process using leaf images and Convolutional Neural Network.

## Problem Statement

Plants are highly susceptible to diseases that inhibit plant development, which has an effect on the farmer's ecology. Use of an automated disease detection technique is advantageous in detecting a plant disease at an early stage. Plant diseases manifest themselves in various parts of the plant, such as the leaves. It takes a long time to manually diagnose plant disease using leaf images. As a result, computational methods would help speed up the process by automating disease detection and classification using leaf images.

Hence, image processing and deep learning models can be employed for the detection of plant diseases. In this project, we have described the technique for the detection of plant diseases with the help of their leaves pictures. Deep learning is a sub part of artificial intelligence which works automatically or give instructions to do a particular task by leveraging artificial neural networks like Convolutional Neural Network architectures.

## About the Dataset

There are several visual prediction datasets of healthy and infected leaf images of various plants. The PlantVillage Dataset is the most leveraged one. The PlantVillage dataset consists of, 54303 healthy and unhealthy leaf images divided into 38 categories by plant species and disease. Another one is popularly known as the PlantDoc dataset, which is more likely to be worked with in a real-world setting. The reason being, that the PlantVillage dataset contains images taken under controlled settings. This dataset limits the effectiveness of detecting diseases because, in reality, plant images may contain multiple leaves with different types of background conditions with varying lighting conditions. On the contrary, PlantDoc dataset was created by downloading infected and healthy images from Google Images and Ecosia for accurate plant disease detection in the farm setting. 

However, the dataset we used for carrying out this experiment is a publicly available open-source dataset hosted at Kaggle. The dataset is popularly known as the PlantVillage Dataset. In this dataset, 38 different classes of plant leaf and background images are available. The data-set containing 163k images. We will use different augmentation techniques for increasing the data-set size. There is a total of 38 Classes that we have to predict using the CNN Model (for simplicity, in this article I will be using only 15 diseases).

#IMAGE-GOES-HERE

We will load the data from the folders. The category labels will be taken from the folder label itself. We will resize the images to 128x128 pixels from their original resolution of 256x256 pixels. While loading the data we will convert them to numpy array. Then we will scale the numpy array values between 0 to 1. 

```python
np_image_list = np.array(image_list, dtype=np.float16) / 255.0
```

Then, we will split the data into train and validation set with validation set having 20% of the data. Then we will create a Data Augmentor that will be used later to augment the images to desired dimensions, shapes and sizes. We will use the following augmentation:

```
Rotation: 45             # Randomly rotates images in range [-45, 45] degrees
Width Shift: 0.1         # Randomly shifts width of images by 10%
Height Shift: 0.1        # Randomly shifts height of images by 10%
Shear: 0.2               # Creates shears in image by 20%
Zoom: 0.2                # Zooms into the image by 20%
Horizontal Flip: True    # Flips the images horizontally
Vertical Flip: True      # Flips the images vertically
```

The augmentor variable will be used during training. Several samples of the image will be generated during training and will be fed to the model. The augmentor variable is created as such: 

```python
aug = ImageDataGenerator(
    rotation_range=45,
    width_shift_range=0.1,
    height_shift_range=0.1,
    shear_range=0.2,
    zoom_range=0.2,
    horizontal_flip=True,
    vertical_flip=True,
    fill_mode="nearest"
)
```

## Creating the Deep Learning Model

For this experiment we will use DenseNet121 pretrained weights. We will build our model on top of DenseNet121 pretrained weights and fine-tune it according to our use-case. The model's low level parameters will be unchanged but we will add few high level parameters on top of those parameters. We will use the following extra parameters: 

1. GlobalAveragePooling2D()
2. BatchNormalization()
3. Dropout(0.5)
4. Dense(256, activation='relu')
5. BatchNormalization()
6. Dropout(0.5)

We will be using TensorFlow 2 library for this experiment. We will use the Keras API to download DenseNet121 pretrained weights and add out layers upon them. 

We will use the Adam optimizer to minimize loss function, with a learning rate of 1E-3. We will use Categorical Crossentropy as the Loss Function. Using these, we will compile our model as such:

```python
optimizer = Adam(
    lr=INIT_LR, 
    decay=INIT_LR / EPOCHS
)

model.compile(
    loss='categorical_crossentropy', 
    optimizer=optimizer, 
    metrics=['accuracy']
)
```

Here we pass another parameter to Adam, `decay`. `decay` parameter is used to decrease the learning rate over time to make sure the optimizer reaches global minima.

#IMAGE-GOES-HERE

Also, during the training process, we will use callbacks to save the best model. The best model will be saved with respect to the validation loss. 

```python
checkpoint = ModelCheckpoint(
    'best_model.h5', 
    monitor='val_loss',
    verbose=1,
    save_best_only=True, 
    mode='auto'
)
```

Using this checkpoint, the best model will be saved during the training. Each time a better validation loss is achieved, that model will be saved by the name `best_model.h5`. 

## Training the Model

Now that our model is ready for training, we can proceed to, well start training the model using the data we have prepared. Remember we split the data into train and validation sets? We will use them now for the training. TensorFlow does everything for us internally. We only need to pass the data, mention for how many epochs we want to run it for, and add callbacks, in this case, the `ModelCheckpoint` to save best model. 

The augmentor object that we created previously, will be used not to generate the augmented data. Using the `flow()` function from the augmentor object, we feed generated data into the model to train. We use a batch size of 32, and we will run the training for 50 epochs. We can train the model using the `model.fit()` method. We pass the data, mention the epochs, pass the callbacks and the model starts training. 

```python
history = model.fit_generator(
    aug.flow(x_train, y_train, batch_size=BS),
    validation_data=(x_test, y_test),
    steps_per_epoch=len(x_train) // BS,
    epochs=EPOCHS, 
    verbose=1,
    callbacks=[checkpoint]
)
```

The model will train for 50 epochs and for each epoch it will train the model using training set and validate the model using validation set. It will save the model in a particular epoch if it's validation loss is lower than any other previous lower validation loss.

The history object will contain all the training history information which can be accessed to plot the history graph for all epochs or a certain range of epochs. Let's create a graph and view our training history for this experiment.

#IMAGE-GOES-HERE

## Testing on Test Data

Now that our model training is complete, we need to check how it performs on the test data. For this we will use 100 images for each class from the dataset that were not used in training and validation dataset. We will do the same preprocessing of data just like we did in training, like resizing them to 128x128 resolution, converting them to numpy array and scaling the pixel values between 0 to 1. 

```python
def image_to_array(path):
	img = cv2.imread(path)
	new_arr = cv2.resize(img,(128, 128))
	new_arr = np.array(new_arr/255)
	new_arr = new_arr.reshape(-1, 128, 128, 3)
	return new_arr
```

To check how the model classifies the diseases, we need some metrics. We will generate a confusion matrix and a classification report for this task. As both of those need arrays to calculate the results, we will store the actual disease labels and predicted disease labels in a list, sequentially. 

Now we loop through the test data loader and predict the labels for each images, simultaneously store the labels in lists. 

```python
for i in range(len(test_image_list)):
    image = image_to_array(test_image_list[i])
    prediction = test_model.predict(image, verbose=0)

    actual.append(test_label_list[i])
    predicted.append(CATEGORIES[prediction.argmax()])
```

Now we have all we need to visualize how our model performed on the unseen data. We will generate confusion matrix using the lists and display it in a heatmap. Fingers crossed 🤞🏻.

#IMAGE-GOES-HERE 

Perfect! The model seems to perform very well on test data. It predicts more than 90 labels correctly for each class. That should be nearly 97% accurate overall. But, enough guessing. Let's generate a classification report and check the metrics. We will use classification report from Scikit-Learn for this. 

```
Classification report: 
                                             precision    recall  f1-score   support

              Pepper__bell___Bacterial_spot       1.00      0.99      0.99       100
                     Pepper__bell___healthy       1.00      1.00      1.00       100
                      Potato___Early_blight       0.93      1.00      0.96       100
                       Potato___Late_blight       0.99      0.96      0.97       100
                           Potato___healthy       1.00      1.00      1.00       100
                      Tomato_Bacterial_spot       1.00      0.95      0.97       100
                        Tomato_Early_blight       0.96      0.92      0.94       100
                         Tomato_Late_blight       0.96      0.95      0.95       100
                           Tomato_Leaf_Mold       1.00      0.97      0.98       100
                  Tomato_Septoria_leaf_spot       0.91      1.00      0.95       100
Tomato_Spider_mites_Two_spotted_spider_mite       0.98      0.97      0.97       100
                        Tomato__Target_Spot       0.96      0.95      0.95       100
      Tomato__Tomato_YellowLeaf__Curl_Virus       1.00      1.00      1.00       100
                Tomato__Tomato_mosaic_virus       1.00      1.00      1.00       100
                             Tomato_healthy       0.99      1.00      1.00       100

                                   accuracy                           0.98      1500
                                  macro avg       0.98      0.98      0.98      1500
                               weighted avg       0.98      0.98      0.98      1500
```

And voilà. It's actually really good results. The model gave a 98% accuracy on test data, which is pretty impressive.