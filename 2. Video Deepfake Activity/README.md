# 2. Video Deepfake Generation Activity

In this activity, you will make use of [Faceswap](https://github.com/deepfakes/faceswap) to generate the fakes. As this open source generator requires time and effort to train the model to perform the swap, we've provided you with a pretained model for 2 Singapore Ministers - Lawrence Wong and Chan Chun Sing. You can use this to generate as many videos as you want.

<ins>How to generate your videos:</ins>

**1) Installing repository and libraries/dependencies:**
- Clone faceswap repository in this folder. Open terminal (Ctrl + Alt + T) and enter the following commands:\
<code>git clone https://github.com/deepfakes/faceswap.git</code>
- Install conda env using the _faceswap.yml_ file provided and activate environment.\
<code>conda env create -f faceswap.yml
  conda activate faceswap</code>
- Download pretrained models from [One Drive](https://hometeamsnt-my.sharepoint.com/:f:/g/personal/ong_si_ci_hometeamsnt_onmicrosoft_com/EsvdDbQwdCREoL-Bx2YCFSEBrDZ5b_FK4-ayU6wwE9tNbw?e=hT18dO). Create a folder called "model" within the cloned faceswap folder and put the downloaded pretrained models inside. Unzip the downloaded models.

**2) Download videos from YouTube for swap**
- Use the YouTube Downloader script that you have cloned in Activity 1 to download videos of DPM Lawrence Wong and Min Chan Chun Sing by preparing the youtube links, start/end times of video in a txt file.
- Videos that you use in the generation phase should only consist of their face in the frame, as Faceswap can only perform the swap on 1 person's face in every frame. If your video contains other individuals in the scene, you may use video cropping tools (e.g. Clideo) to crop the video to contain only that 1 individual. This should be done after you have used the script above to download the video.

**3) Generate your own swap**
- Create a folder "converted" within your faceswap folder. Within "converted" folder, create sub-folders for each video that you are generating, using the following naming convention: "CCS-LW-X-Y" where X=2 or 3, depending on the pretrained model that you use, and Y=1,2,3, etc. The value of Y should correspond to the number that you record /document in the Excel sheet. 
