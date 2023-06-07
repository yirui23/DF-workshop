# 1. Audio Deepfake Generation Activity 

<ins>How to generate your audio clips:</ins>

**1) Download videos from YouTube**
- Clone YouTube Download script from [here](https://github.com/ongsici/YT-AV-Downloader)
- Follow the instructions in that page to create conda environment, install requirements and run the script.
- To select Youtube videos for the target speaker you want to clone, find an audio clip with minimum 8 to 10 sec of airtime with only the speaker talking. Download at least 25 samples, minimize the audio silence or words that got cut in the middle (can download Audacity to verify the clips as well as clean it up if required). However we suggest not to do so as this will require additional processing. 

**2) Use ElevenLabs to generate the voice clones**
- Go to [ElevenLabs](https://beta.elevenlabs.io/). Follow the login details shown on the PPT slides to login.
- Select VoiceLab tab, and select Add Generative or Cloned Voice. 
![alt text](https://github.com/ongsici/DF-workshop/blob/main/1.%20Audio%20Deepfake%20Activity/images/VoiceLab.png?raw=true)

- Select Instant Voice Cloning when the following windows pops out. 
- Insert name of the person whom’s voice you will be cloning e.g. Elon Musk, upload 25 audio clips (ranging 8 to 10 seconds, total about 4 to 5 mins) 

![alt text](https://github.com/ongsici/DF-workshop/blob/main/1.%20Audio%20Deepfake%20Activity/images/Add%20Voice.png?raw=true)

- Create audio deepfakes with roughly 8~10 sec worth of speech (You can use chatGPT to generate the sentences), you can experiment with both monolingual and multilingual model.
 
![alt text](https://github.com/ongsici/DF-workshop/blob/main/1.%20Audio%20Deepfake%20Activity/images/Speech%20Synthesis.png?raw=true)

- Download each clip and store it in the respective folders 


<ins>Additional Task (if time permits):</ins>
- If there is time, can check out [sovits svc](https://github.com/voicepaw/so-vits-svc-fork) where you can clone your own voice and make it sing using your own voice. 
- If your have issue installing the requirements for the environment you can use the free plan of [Google Colab](https://colab.research.google.com/github/34j/so-vits-svc-fork/blob/main/notebooks/so-vits-svc-fork-4.0.ipynb)
- You can also check out this [link](https://www.youtube.com/watch?v=xgvT7UnUTng&ab_channel=JarodsJourney) for the guide on how to use the google colab. 
