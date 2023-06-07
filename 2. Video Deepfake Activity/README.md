# 2. Video Deepfake Generation Activity

In this activity, you will make use of [Faceswap](https://github.com/deepfakes/faceswap) to generate the fakes. As this open source generator requires time and effort to train the model to perform the swap, we've provided you with a pretained model for 2 Singapore Ministers - Lawrence Wong and Chan Chun Sing. You can use this to generate as many videos as you want.

<ins>Some quick terminologies:</ins>
- Source: Original video of the person that you want to replace. In this case, source = Chan Chun Sing.
- Target: The person whose face you want to put into the source video. In this case, target = Lawrence Wong.

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
- NOTE: Ensure that your _source_ video clips (Chan Chun Sing) used are **less than** 30s. Otherwise the facial alignments generation will take too long. 

**3) Generate your own swap** 

Before you can perform the face swap, you will first need to generate an _alignments.fsa_ file for all source videos (Chan Chun Sing). The alignments file holds information about all the faces it finds in each frame, specifically where the face is, and where the 68 point landmarks are. 
- Open the faceswap GUI using the following:\
<code>cd faceswap
  python faceswap.py gui</code>
- If this is the first time you are running the above, in the terminal, you will be asked to select the backend. Choose "NVIDIA" option. 
- Make the following selection options: 

| Parameter  | Option to select | Example |
| ------------- | ------------- | ------------- |
| Input Dir  | Select "Video" option. Choose the _source_ video (Chan Chun Sing) that you would like to generate the alignment for | CCS-1.mp4 |
| Output Dir | Select the output folder where you would like to store the faces. Suggest to create a separate folder called "_faces_" and store them in subfolders. | faceswap/faces/CCS-1 |

- Leave the alignments field empty. For other fields, leave it as default. 
- Once ready, click "Generate" and wait for the process to be completed. 
- The alignments file generated will be in the same folder location as your input video. 

Once the alignment files have been generated, perform the following: 
- Create a folder "converted" within your faceswap folder. Within "converted" folder, create sub-folders for each video that you are generating, using the following naming convention: "CCS-LW-X-Y" where X=2 or 3, depending on the pretrained model that you use, and Y=1,2,3, etc. The value of Y should correspond to the number that you record /document in the Excel sheet. 
- Make the following selections: 

| Parameter  | Option to select | Example |
| ------------- | ------------- | ------------- |
| Input Dir  | Select "Video" option. Choose the _source_ video (Chan Chun Sing) that you would like to use.  | CCS-1.mp4 |
| Output Dir | Selected the sub-folder you have created in the "_Converted_" folder for the respective iteration of generation.  | faceswap/converted/CCS-LW-2-1 |
| Alignments | Select the _alignments.fsa_ file that corresponds to the video selected in "Input Dir" option. | CCS-1_alignments.fsa |
| Reference Video | Select the _target_ video (Lawrence Wong) that you would like to use. | LW-1.mp4 |
| Model Dir | Select the model folder that you like to use | CCS-LW-2_snapshot_975000_iters OR CCS-LW-3_snapshot_600000_iters |
 - You may play around with the Plugin Options for Color Adjustment and Mask Type. Please select opencv as writer and leave other settings as default. 
 - Once ready, click "Convert" and wait for a few minutes for your swap to be generated. They will be generated as images in your selected Output Dir.

**4) Combining generated images into a video**
- Extract the audio file from the video file you selected in Input Dir using the following code.\
<code>ffmpeg -i [input video filepath] -vn -acodec copy [output audio filename/path]</code> \
  Example (run from faceswap folder):\
  <code> ffmpeg -i ./ChanChunSing/CCS-1.mp4 -vn -acodec copy ./ChanChunSing/CCS-1.aac</code> 
- Combined the generated frames from (3) into a video using the following code. Run this code in the Output Dir folder that you have selected in (3) \
  <code> ffmpeg -framerate [frame rate of original video] -pattern_type glob -i '\*.png' -c:v libx264 -pix_fmt yuv420p [output video name] </code>\
    Example: \
  <code> ffmpeg -framerate 30 -pattern_type glob -i '\*.png' -c:v libx264 -pix_fmt yuv420p CCS-LW-2-1-video.mp4 </code>
- Combine the extracted audio and generated video together using the following code. Run this in the main faceswap folder. \
    <code>ffmpeg -i [video filepath] -i [audio filepath] -c:v copy -c:a aac [output video name] </code> \
    Example: \
    <code>ffmpeg -i ./converted/CCS-LW-2-1/CCS-LW-2-1-video.mp4 -i ./ChanChunSing/CCS-1.aac -c:v copy -c:a aac CCS-LW-2-1.mp4 </code>
