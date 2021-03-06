# Quick tour to Keras api (keras is default api for TF 2.0) - pseudocode


                  
##  ConvNet Model build (Sequential api), compile, train, save weights, predict api 
```Python
    from keras import backend as K
    tf.set_random_seed(89)
    K.set_session(sess)
	model= Sequential([
        Conv2D(32, (3, 3), activation='relu', input_shape=(224,224,3), use_bias=True, bias_initializer='zeros',padding='same'),
        MaxPooling2D(pool_size=(2,2), strides=2),
        Flatten(),
        Dense(2, activation='softmax')])
    model.compile(Adam(lr=.0001), loss='sparse_categorical_crossentropy', metrics=['accuracy'])
    model.fit(scaled_train_samples, train_labels, validation_split=0.1, batch_size=10, epochs=20, shuffle=True, verbose=2)
    model.save('medical_trial_model.h5')
    model.predict(test_batches, steps=1, verbose=0)
	
  ```


   
## Importing pretrained model application (such as State of art VGG16 model)   

```Python
  keras.applications.vgg16.VGG16()
```

## ImageDataGenerator (Data augmentation) preprocessing api 

```Python

    ImageDataGenerator(rotation_range=10, width_shift_range=0.1, height_shift_range=0.1, shear_range=0.15, zoom_range=0.1, channel_shift_range=10., horizontal_flip=True)
```

```Python
    ImageDataGenerator().flow_from_directory(train_path, target_size=(224,224), classes=['dog', 'cat'], batch_size=10)
```

## Autoencoder Model: 
 Encoding and decoding input file to get an output which is close to input one. So loss function is minimised. Main utility is to remove noise

## Flattening in CNN:
 It’s actually very simple: the fully connected layer expects a vector as input. For example - Convolution outputs a series of filters, which each are a grid shape. Flattening specifies a function mapping from these filters to a vector, so you can backpropagate errors back through the convolutional layers.

## verbose in Keras Model.fit
By setting verbose 0, 1 or 2 you just say how do you want to 'see' the training progress for each epoch.

verbose=0 will show you nothing (silent)
verbose=1 will show you an animated progress bar 
verbose=2 will just mention the number of epoch 



