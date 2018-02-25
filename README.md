# Grand Theft Auto Vice City Self Driving Car

<a href="https://www.youtube.com/watch?v=1O8nNedZ-l8" target="_blank"><img src="https://github.com/ezchx/gta_self_driving_car/blob/master/Screenshot%202018-02-24%2013:26:06.png"></a>

Trains a neural network to control the vehicles in Grand Theft Auto Vice City. Developed with Ubuntu 16.04, Python 3.6, Keras, VGG16, and TensorFlow and trained on a GTX 1080 ti.

Step 1 – Install GTA Vice City    
Install PlayOnLinux and Wine on your computer. Set up an account on Steam and purchase GTA VC ($10). Configure Wine to emulate a virtual desktop of 800 x 600 and position the window in the upper left corner of your screen. This was the hardest part, so don't despair.

Step 2 – Create the Data    
Set up the data directories on your computer:
```
raw_data
└───train
│   │   forward
│   │   left
│   │   reverse
|   |   right

data
└───train
│   │   forward
│   │   left
|   |   right
└───valid
│   │   forward
│   │   left
|   |   right
```

Start the game and get in a car. Run screen_grabber.ipynb and start driving the car with the following keys:

w – forward    
a – left    
s – reverse    
d – right    

Whenever you press one of these keys, the program takes a screen shot and saves it to your computer. You can stop the program at any time by pressing the Esc key. You can save additional images by setting the starting number of images to the number of images you have saved so far and rerunning screen_grabber.ipynb.

Since you need to balance the number of images by command, the total dataset will equal the minimum number of images for a particular direction x the number of directions you use for your model. For my screen grabs, the totals were:

forward = 19,903    
left = 3,525    
reverse = 749    
right = 3,763    

Since I did not use reverse for my model, my minimum was “left” at 3,525, so I balanced out “forward” and “right” to match this total. You can do the same for your data by copying the corresponding totals from the raw_data directories to the data directories – i.e. 3,525 images from raw_data/forward to data/forward, 3,525 images from raw_data/left to data/left, and 3,525 images from raw_data/right to data/right.

Finally, copy 10%-20% of your training data to the corresponding “valid” directories.

Step 3 – Train the Model    
Run train_vgg_model.ipynb. Notice that we are using the Keras VGG16 model with pre-trained weights, removing the output layer of 1,000 classes and replacing it with an output layer of 3 classes. Also, since we are setting all layers to trainable, the model requires a very small learning rate of 0.0001. Feel free to replace VGG with another model.

Train the model. For my data, the best train / validation accuracy was 0.7973 / 0.7451 after 6 epochs (10 minutes). Your results may vary. Be sure to save the best trained model.

Step 4 – Test the Model    
Restart GTA, get in a car, and run test_vgg_model.ipynb. Be careful when toggling between windows because the Main Function will spew keyboard commands all over the place! To stop the program, toggle to the simulator window and press the "q" key.

That’s it. Enjoy! You can use this program to apply any AI to any game or application that you can run on your computer.

Many thanks to Sentdex for the original application to GTA V on Windows with InceptionNet (sorry man, I just had to do Vice City) and Jeremy / Rachel of fast.ai for their AMAZING course on Deep Learning.

Sentdex: https://www.youtube.com/watch?v=ks4MPfMq8aQ&list=PLQVvvaa0QuDeETZEOy4VdocT7TOjfSA8a    
Fast.ai: http://course.fast.ai/    
