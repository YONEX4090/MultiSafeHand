## Advanced Dexterous Manipulation in MARL: MultiSafHand & MACPAO Integration

In this project, we introduce MultiSafHand, which combines tasks ith different levels of difficulty and a variety of objects to facilitate learning to use both hands for dexterous manipulation. Concurrently, we clarify strategies in multi-agent optimization, with a notable emphasis on safety, offering innovative solutions in dexterous manipulation and MARL. MultiSafHand is adept at ensuring safe manipulation and supports effective methods for solving CMDPs. Additionally, we examine the complexity of safety issues in multi-agent environments and introduce MACPAO, a Safe MARL algorithm that has realized advancements in safety while maintaining the higher rewarding results comparable to existing state-of-the-art methods.
<div align="center">
  <img src="safe-policy/assets/overview.jpg" width="75%"/>
</div>

### Installation
The operating system we use is **Ubuntu20.04**. Before you begin the installation, please make sure you have installed **Anaconda**.

To start with, you should first install **IsaacGym Preview 4**. Download the source code from [here](https://developer.nvidia.com/isaac-gym) to the custom directory and decompress it. Then run the following commands to install. The **pytorch** we used in this project is the newest version 2.1.0. **mujoco200** is needed and the installation details are shown in safe-policy/Installation.md.
```bash
conda create -n env_name python=3.8
conda activate env_name
cd isaacgym/python/
pip install -e .
conda install mpi4py
conda install torch
```

This project is based on **safety-gymnasium**, which is a highly scalable and customizable Safe Reinforcement Learning (SafeRL) library designed by PKU-Alignment. The source code is from [safety-gymnasium](https://github.com/PKU-Alignment/safety-gymnasium). In our project, we implement some new task including ''CloseDoor'' and ''OpenPenCap'' and applied some different constraints to the base environments. You can directly install this library using commands as following:
```bash
wget https://github.com/YONEX4090/MultiSafHand.git
conda activate env_name
cd safety-gymnasium
pip install -e .
```
We compare our algorithm with baselines from [Safe-Policy-Optimization](https://github.com/PKU-Alignment/Safe-Policy-Optimization), run the following commands to install the necessary dependencies.
```bash
conda activate env_name
cd safe-policy
pip install -e .
```
### Tasks
#### HandOver
This environment requires that one hand must adeptly toss an object, while the other must catch it with precision, avoiding excessive force that could lead to accidental object damage, unstable grasp, or potential safety risks.
<div align="left">
  <img src="safe-policy/assets/handover.jpg" width="75%"/>
</div>

#### CloseDoor
This environment requires that closed doors can only be pushed inwards, but this is relatively difficult as the task cannot be accomplished by a simple push, which requires the hand to grab the
handle and push it and then open it.
<div align="left">
  <img src="safe-policy/assets/closedoor.jpg" width="75%"/>
</div>

#### OpenPenCap
This environment involves two hands and pen, we need to use two hands to open the pen.
<div align="left">
  <img src="safe-policy/assets/openpencap.jpg" width="75%"/>
</div>

#### ClosePenCap
This environment involves two hands and pen, we need to use two hands to close the pen.
<div align="left">
  <img src="safe-policy/assets/closepencap.jpg" width="75%"/>
</div>

### Train Model
You can use the following commands to train your model. The project supports multi-agent algorithms including happo, macpo, mappolag and macpao. The trained models and logs are stored in the safe-policy/safepo/runs
```bash
cd safe-policy/safepo/multi_agent
python macpao.py --task HandOver --experiment benchmark
```
### Plot Experimental Results
Run following commands to plot the results. The pictures are stored in the safe-policy/safepo/results
```bash
cd safe-policy/safepo
# if you want to plot a comparision picture for all tasks
python plot.py --logdir ./runs/benchmark
# if you want to plot a comparision picture for the specific task
python plot.py --logdir ./runs/benchmark/HandOver
# if you want to plot a comparision picture for the specific task with the specific algorithm
python plot.py --logdir ./runs/benchmark/HandOver/macpao 
```
### Performance
<div align="left">
  <img src="safe-policy/assets/performance.png" width="100%"/>
</div>
### Video
<video src="safe-policy/assets/video.mov" controls="controls">
</video>



