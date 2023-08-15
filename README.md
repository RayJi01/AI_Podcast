# 🕹AI_Podcast🤖

Welcome to the AI Podcast Demo! This repository showcases the capabilities of our AI-powered podcast recommendation system. Here, you will not only see the AI chat and respond to the human's problems, but also see how a **real-chat** (speaking and listening) can happened between the user and clients. You will also see a chat-room with more than 1 agents (two in our podcast but you can add more) and how they interact with not only your prompts, but also each others' responses. At the AI_Podcast, You can have the feelings of the what is **AI future** feels like. 

<img width="1042" alt="a4e0e04c889658eacc1d8ead0dd554c" src="https://github.com/RayJi01/AI_Podcast/assets/89424938/4066a069-eb7f-4070-a4f4-bda56c3db3e7">

## Table of Contents

- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [Usage](#usage)
- [Features](#features)
- [Demo-Videos](#Demo-Videos)
- [Contributing](#contributing)
- [License](#license)

## Getting Started
To try out AI_Podcast on your computer, you should only need a computer with a GPU environment(either CUDA or Metal for MacOS) or a strong CPU for computation and inference. 

The **AI_Podcast** is built by:
- @OpenAI's whisper
- @ggerganov's ggml
- @WizardLM_AI's wizardlm v1.0
- @lmsysorg's vicuna v1.3
- @Xorbitsio's inference as a launcher

The **AI_Podcast_ZH** is built by:
- @OpenAI's whisper
- @PyTorch's PyTorch
- @Baichuan-inc's Baichuan-chat
- @Xorbitsio's inference as a launcher


## Prerequisites
- A machine with either Windows, Ubuntu, or MacOS system. 
- Only MacOS can access radio output(by the system provided "say" command in MacOS) with the source code. For Windows or Ubuntu, try ''pyttsx3'':
  
  ```
  pip install pyttsx3
  ```
- For the AI_Podcast version, ensure you have at least 16G memory storage for computing.
- For the AI_Podcast_ZH version, ensure you have at least 24G memory storage for launching one model. If you want to launch two Baichuan
- Make sure you have the latest version of ''Xinference''. Install it by
  
  ```
  pip install "xinference[all]"
  ```
  For detailed information about this package, [click here to read more](https://github.com/xorbitsai/inference)

## Installation
Clone this repository: 
```
git clone https://github.com/RayJi01/AI_Podcast.git
```

## Usage
1. Navigate to the project directory:
   ```
   cd AI_Podcast
   ```
3. Install the required dependencies(except for Whisper):
   ```
   pip install -r requirements.txt
   ```
   For Openai Whisper, please download this [packages](https://pypi.org/project/openai-whisper/)
4. To start the Xinference Service：
   * Start an `Instance` locally:
     ```
     xinference
     ```
     This will start the service at default `http://localhost:9997`.
     
   * Start a `Cluster` locally, you need to start a Xinference supervisor on one server and Xinference workers on the other servers. Follow the steps below:
     
     **For Supervisor**:
     ```
     xinference-supervisor -H "${supervisor_host}"
     ```
     Replace ${supervisor_host} with the actual host of your supervisor server.
     
     **For Worker**:
     ```
     xinference-worker -e "http://${supervisor_host}:9997"
     ```
     This will start the service at `http://${supervisor_host}:9997`, where `${supervisor_host}` is the hostname or IP address of the server where the supervisor is running.
     
5. For AI_Podcast.py, run the system by:
   ```
   python AI_Podcast.py -e ${supervisor_host}
   ``` 
7. For AI_Podcast_ZH.py, run the system by:
   * At the supervisor side to see all the model supported, and find Baichuan-chat or any other models you want:
     
     ```
     xinference list --all
     ```  
   * At the client side, launch the Baichuan-chat-13B model from `${supervisor_host}` by:
     
     ```
     xinference launch -n Baichuan-chat -q 4_bit -s 13
     ```
     If success, the system will return a `model_uid`. You can launch two different models or launch one model to act on two characters. 
   * Start the system by:
     
     ```
     python Ai_Podcast.py -e ${supervisor_endpoint} -m1 ${model_uid} -m2 ${model_uid}
     ```
     `${supervisor_endpoint}` is where your supervisor is launched and running. `${model_uid}` is the id returned from successful launching. 

## Features
- ⚡️ State-of-the-Art Models: Experiment with cutting-edge built-in models using Xinference to receive good performances. 
- 🖥 Heterogeneous Hardware Utilization: With the support from Xinference, the AI_Podcast can be run in heterogeneous hardware, including GPUs and CPUs, to accelerate your model inference tasks.
- 🌐 Two AIs Chat Together: Instead of chatting with AI individually, two agents can answer your question with a shared chat context. You can then have different advice from different models to compare with. You can also let the AI criticize each other so that the win-win strategy may be yielded from that competition. 
- 🔌 Model Versatility: You can quickly shift to other models you want with Xinference, either by editing the source code of launching models in AI_Podcast.py or launching different models for AI_Podcast_ZH.py. Both English model or Chinese model are available.
- 🎧 Audio to Audio Service: With **Whisper** and MacOS's **say**, the Podcast makes the users feel like they are **chatting** through **speaking** and **listening**, not "pseudo-chatting through key-board," with AI agents. You can even change each AI is voice to best-fit your environment.

## Demo-Videos:

- AI_Podcast(English Version): Please Checkout the Tweet of the Demo to see the video!
- [Twitter Video Demo](https://twitter.com/yichaocheng/status/1679129417778442240)


## Contributing
Contributions are welcome! If you'd like to contribute to AI_Podcast, follow these steps:
1. Fork this repository
2. Create a new branch: `git checkout -b feature-name`
3. Make your changes and commit them: `git commit -m "Add some feature"`
4. Push to your forked repository: `git push origin feature-name`
5. Create a pull request detailing your changes

## License
This project is licensed under the Apache License, Version 2.0 - see the [LICENSE](https://www.apache.org/licenses/LICENSE-2.0) file for details.
