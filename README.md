# B-W-Photos-and-Videos-Colorizering-
This project can be used to colorise Grayscaled images using the state of the art Caffe model.


some sample:- 
sample 1 input :
![Screenshot 2024-05-08 165600](https://github.com/lifemax123/B-W-Photos-and-Videos-Colorizering-/assets/76859897/23b4b49f-5e80-41e5-9ff3-8c9b26243297)


output :
![Screenshot 2024-05-08 165630](https://github.com/lifemax123/B-W-Photos-and-Videos-Colorizering-/assets/76859897/d1960e39-100f-4e35-afe4-bb5cd3160861)


Black and white image colorization with OpenCV.
## Table of Content
  * [Demo](#demo)
  * [Overview](#overview)
  * [Motivation](#motivation)
  * [Technical Aspect](#technical-aspect)
  * [Installation And Run](#installation-and-run)
  * [Directory Tree](#directory-tree)
  * [To Do](#to-do)
  * [Bug / Feature Request](#bug---feature-request)
  * [Technologies Used](#technologies-used)
  * [Team](#team)
  * [License](#license)
  * [Credits](#credits)
## Demo
![Alt Text](https://j.gifs.com/2xVL2P.gif)

## Overview
Image colorization is the process of taking an input grayscale (black and white) image and then producing an output colorized image that represents the semantic colors and tones of the input (for example, an ocean on a clear sunny day must be plausibly “blue” — it can’t be colored “hot pink” by the model).


## Technical Aspect
- The technique we’ll be covering here today is from Zhang et al.’s 2016 ECCV paper, [Colorful Image Colorization](http://richzhang.github.io/colorization/). Developed at the University of California, Berkeley by Richard Zhang, Phillip Isola, and Alexei A. Efros.

- Previous approaches to black and white image colorization relied on manual human annotation and often produced    desaturated results that were not “believable” as true colorizations.

- Zhang et al. decided to attack the problem of image colorization by using Convolutional Neural Networks to  “hallucinate” what an input grayscale image would look like when colorized.

- To train the network Zhang et al. started with the [ImageNet dataset](http://image-net.org/) and converted all images from the RGB color space to the Lab color space.

- Similar to the RGB color space, the Lab color space has three channels. But unlike the RGB color space, Lab encodes color information differently:
  - The **L channel** encodes lightness intensity only
  - The **a channel** encodes green-red.
  - And the **b channel** encodes blue-yellow.

- As explained in the original paper, the authors, embraced the underlying uncertainty of the problem by posing it as a classification task using class-rebalancing at training time to increase the diversity of colors in the result. The Artificial Intelligent (AI) approach is implemented as a feed-forward pass in a CNN (“Convolutional Neural Network”) at test time and is trained on over a million color images.

- The color photos were decomposed using Lab model and “L channel” is used as an input feature and “a and b channels” as classification labels as shown in below diagram.

<img target="_blank" src="https://user-images.githubusercontent.com/71431013/99061015-eb844a80-25c6-11eb-8850-bcc9f74d91e6.png" width=500>

- The trained model (that is available publically and in models folder of this repo or [download it by clicking here]( http://eecs.berkeley.edu/~rich.zhang/projects/2016_colorization/files/demo_v2/colorization_release_v2.caffemodel)), we can use it to colorize a new B&W photo, where this photo will be the input of the model or the component “L”. The output of the model will be the other components “a” and “b”, that once added to the original “L”, will return a full colorized image.

## The entire (simplified) process can be summarized as:
- Convert all training images from the RGB color space to the Lab color space.
- Use the L channel as the input to the network and train the network to predict the ab channels.
- Combine the input L channel with the predicted ab channels.
- Convert the Lab image back to RGB.

<img target="_blank" src="https://user-images.githubusercontent.com/71431013/99061033-f048fe80-25c6-11eb-8bc5-d6312c7021b6.png" width=500>

## Installation And Run 
1.The Code is written in Python 3.7. If you don't have Python installed you can find it [here](https://www.python.org/downloads/). If you are using a lower version of Python you can upgrade using the pip package, ensuring you have the latest version of pip. To install the required packages and libraries, run this command in the project directory after [cloning](https://www.howtogeek.com/451360/how-to-clone-a-github-repository/) the repository:
Download from this link : [here](https://www.dropbox.com/s/dx0qvhhp5hbcx7z/colorization_release_v2.caffemodel?dl=1) and patse in Model folder.
```bash
pip install -r requirements.txt
```
2. [Run the file with](https://docs.streamlit.io/en/stable/):
 ```bash
 $ streamlit run app.py
 ```
 
## Directory Tree 
```   
|   app.py  
+---Input_images
|       che-guevara-.jpg
|       pexels-pixabay-141651.jpg
|       pexels-pixabay-36755.jpg      
+---models
|       colorization_release_v2.caffemodel
|       models_colorization_deploy_v2.prototxt
|       pts_in_hull.npy     
\---Result_images
        colored_c1.jpg
        colored_c7.jpg
        colored_c8.jpg
```
## To Do
- To Convert the application to colorize black and white videos.


