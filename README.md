# intelfaceswap
Deepfakes's Intel-based Python FaceSwap

THIS IS FOR INTEL-BASED PYTHON, BUT YOU STILL CAN TRY TO ADAPT IT USING REGULAR PYTHON OR ANACONDA

RECOMMENDED FOR WINDOWS 10, WITH NVIDIA

this tutorial is made to help the beginners and the community. if you are quietly a pro, just do it by yourself.

**********************************

**before we start,**

install
* Intel-Python (w_python3_pu_2018.1.021) to C:\IntelPython3
* CUDA (cuda_8.0.61_win10)
* Visual C++ Build Tools (visualcppbuildtools_full)
* CMake (cmake-3.10.1-win64-x64)
* GIF Animator (GIFAnimator-Setup)

extract
* CUDNN to `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0`

setting the environment
* create and set `PYTHONPATH` to `C:\IntelPython3` in *Environment Variables*

----------------------------------

**gear up!**

in cmd, type:

    conda install pip
    pip install tensorflow-gpu dlib opencv-python keras scipy numpy h5py matplotlib tqdm scikit-image
    conda install -c peterjc123 pytorch cuda80

(if the pip doenst work, download the wheel, pick based on your system and python, then run `pip install whatever_the-name-is.whl` in the directory of the wheel downloaded)

----------------------------------

**intro**

* get ready
* open code.txt in \face-swap
* run cmd, `cd [FACE-SWAP DIRECTORY HERE]`
* run in cmd, `activate tensorflow` and `python train.py`
* wait for several hours, stop the training by clicking on the faces window (not X), and then press Q.
* exit the cmd

----------------------------------

**get the data!**

* collect tons of images of target (200+)
* gather the images in a new folder, and rename as *target*, and copy to `\face-alignment-master`

* find the video that satisfies your imagination (POV view recommended)
* convert the video to jpg by using FFMPEG or any video software
* to convert, read the code.txt in bin directory in FFMPEG folder
* run cmd, 

    `cd [BIN DIRECTORY INSIDE OF FFMPEG HERE]`
        `ffmpeg -i file.mp4 -r 1/1 $filename%d.jpg` 
(change *file.mp4* to your video name with its extensions, and *$filename%d.jpg* to any name eg *riley%d.jpg*)

* copy the jpgs to a new folder, rename to *source*, and copy to `\face-alignment-master`

----------------------------------

**i'm ready!**

before do anything:

     pip install -r requirements.txt
     python setup.py install

* align both *target* and *source* images, to get aligned, cropped faces:

    `python align_images.py target`
    `python align_images.py source`
    
* open *target* and *source* folder, take a look at the *aligned* folder in both folder
* remove unwanted images. rename folder to *targetA* and *sourceA*. copy **aligned** folder in both *target* and *source* to `\face-swap\data`
* rename *cage* and *trump* to *cageA* and *trumpA*, and rename *targetA* and *sourceA* to *cage* and *trump*

* after done, copy *align_images.py*, *merge_faces.py*, *umeyama.py*, *source* folder to `\face-swap`

----------------------------------

**lets train!**

* run the same code for training, `activate tensorflow` and `python train.py`
* after it done, new *output* folder can be access
* have a look of the training data. if satisfied, proceed
* run cmd `python merge_faces_masked.py source`
* a new *aligned* folder can be access in *source* folder
* take a look at the merged faces

----------------------------------

**but, no gif?**

from the *merged* folder,
* go to GIFMaker , to convert jpg to gif. (it easier!)
* you can also use the install GIF Animator to make GIF
* DONE

----------------------------------

**kinda bored. need some audio!**

use FFMPEG, to convert gif to video

    ffmpeg -i try.gif -movflags faststart -pix_fmt yuv420p -vf "scale=trunc(iw/2)*2:trunc(ih/2)*2" try.mp4

use any video software

* add the source video (video + audio)
* add the final deepfake video
* align it correctly to the time/frames of the source video
* delete the source video
* render and voilà, now you have a new fake video with sound!

