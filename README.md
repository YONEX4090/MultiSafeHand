## Safe multi-agent reinforcement learning for bimanual dexterous manipulation

In this paper, we propose Multi-Agent Constrained Proxi-mal Advantage Optimization (MACPAO), which considers the sequence of agent updates and integrates non-stationarity into sequential update schemes. we designed a system comprising three components: object datasets, bimanual dexterous tasks, and the Safe MARL algorithm. **Supplemental material** is available at the provided [link](https://github.com/YONEX4090/MultiSafeHand/files/14512193/Supplementary_material_for_IROS.1.pdf)
.
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
This task requires robotic agents to learn how to close a door, which involves gripping the handle and exerting the appropriate amount of force, while considering factors such as the door's inertia and the design of the handle. In this environment, doors that are closed can only be pushed inward, adding complexity to the task as it cannot be achieved by a mere push but requires a coordinated maneuver to grab, push, and then pull the door open.
<div align="left">
  <img src="safe-policy/assets/closedoor.jpg" width="75%"/>
</div>

#### OpenPenCap
This environment involves two hands and pen, we need to use two hands to open the pen and prevent slippage or damage.
<div align="left">
  <img src="safe-policy/assets/openpencap.jpg" width="75%"/>
</div>

#### ClosePenCap
This environment involves two hands and pen, we need to use two hands to close the pen and prevent slippage or damage.
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
The comparison of performance across four tasks—Hand Over, Close the Door, and Open/Close Pen Cap—is depicted with rewards on the top side of the graph and costs on the bottom. The shaded areas represent the standard deviation of scores from more than three trials, showing that MACPAO outperforms all baseline Safe MARL algorithms (MACPO, MAPPO-Lag) as well as Unsafe MARL algorithms (HAPPO).

<div align="left">
  <img src="safe-policy/assets/performance.png" width="100%"/>
</div>

### Video


https://github.com/YONEX4090/MultiSafeHand/assets/148365280/8125f164-ae13-487a-bbe1-b52335d39624






