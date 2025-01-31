<img src="docs/img/square_logo.png" align="right" width="25%"/>

[![Build Status](https://travis-ci.com/flow-project/flow.svg?branch=master)](https://travis-ci.com/flow-project/flow)
[![Docs](https://readthedocs.org/projects/flow/badge)](http://flow.readthedocs.org/en/latest/)
[![Coverage Status](https://coveralls.io/repos/github/flow-project/flow/badge.svg?branch=master)](https://coveralls.io/github/flow-project/flow?branch=master)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/flow-project/flow/binder)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/flow-project/flow/blob/master/LICENSE.md)

# Flow

[Flow](https://flow-project.github.io/) is a computational framework for deep RL and control experiments for traffic microsimulation.

See [our website](https://flow-project.github.io/) for more information on the application of Flow to several mixed-autonomy traffic scenarios. Other [results and videos](https://sites.google.com/view/ieee-tro-flow/home) are available as well.

# Installations

- [Documentation](https://flow.readthedocs.org/en/latest/)
- [Installation instructions](http://flow.readthedocs.io/en/latest/flow_setup.html)
- [Tutorials](https://github.com/flow-project/flow/tree/master/tutorials)
- [Binder Build (beta)](https://mybinder.org/v2/gh/flow-project/flow/binder)

# Experiments
- **Installation**:
    - SUMO 1.6.0 Linux ubuntu (please use the exact version for reproducibility)
        - SUMO 1.6.0 needs to be installed by building from source
        - Download source code from here: https://sourceforge.net/projects/sumo/files/sumo/
        - Sumo-src-1.6.0.zip or sumo-src-1.6.0.tar.gz
        - Check the instructions here https://sumo.dlr.de/docs/Installing/Linux_Build.html
    - Flow
        ```bash
        conda env create -f environment.yml
        conda activate flow
        python setup.py develop
        ```
- **Training**:
    - You can train using the file flow/benchmarks/rllib/ppo\_runner.py and passing in a benchmark name. I recommend passing in merge4\_Sim as a first step. Note that this will take several hours to train.
    - For **Centralized** experiments, you should run the command from the flow/benchmarks directory. The specific command you should run is: 
        ```bash
        python rllib/ppo_runner.py --benchmark_name merge4_Sim --num_cpus  number_of_cores --lr 5e-5 --num_rollouts 2
        ```
    - For **Distributed** experiments, please first go to the directory and then run the corresponding scripts:
        ```bash
        cd examples/rllib/multiagent_exps
        python multiagent_merge4_Merge4_Collaborate_lrschedule.py 
        ```

- **Evaluation**
    - Tensorboard 
    You can view the results by running 
        ```bash
        tensorboard --logdir results_dir
        ```
        - The results should be stored in your ~/ray\_results directory after training (e.g. ~/ray\_results/merge\_4/PPO/exp1) You can view the results by opening a browser to **localhost:6006**
        - Install tensorboard in base and run this command in base.
    - Policy Visualizer
        - Once it's finished try visualizing it with the file flow/visualize/new_rllib_visualizer.py. You do so by passing in a checkpoint directory and a checkpoint number. You should run the command from the MITC directory. The specific command you should run is:
        ```bash
        python flow/visualize/new_rllib_visualizer.py checkpoint_dir checkpoint_num
        ```

- **Experiments**
Here we will give an overview of the necessary python classes related to the experiment in our AAMAS paper “Scalable Multiagent Driving Policies For Reducing Traffic Congestion”

Architecture| Section in AAMAS | Description | Benchmark/File name
:-------------------------------------: | :--------------: | :---------: | :-----------------
Decentrailzed | Simple Merge | Full State Augmentation | multiagent\_merge4\_Merge4\_Collaborate\_lrschedule.py 
Centralized | Simple Merge | Human | flow.benchmarks.merge4\_IDM
Centralized | Simple Merge | Flow Reward | flow.benchmarks.merge4\_Sim
Centralized | Simple Merge | Outflow Reward | flow.benchmarks.merge4\_Sim\_Arrive.py
Centralized | Simple Merge | Average Speed Reward | flow.benchmarks.merge4\_Sim\_AvgVel
Centralized | I-696 | Window, Ouflow | flow.benchmarks.1merge\_Window\_transfer\_Arrive
Centralized | I-696 | Window, AvgVel | flow.benchmarks.1merge\_Window\_transfer\_AvgVel
Centralized | I-696 | Entire, Outflow | flow.benchmarks.1merge\_horizon2000\_warmup0\_simstep05\_flow2000\_merge200\_dePart10\_Arrive
Centralized | I-696 | Entire, AvgVel | flow.benchmarks.1merge\_horizon2000\_warmup0\_simstep05\_flow2000\_merge200\_dePart10\_AvgVel
Centralized | I-696 | ZeroShot | load policies trained in simple merge and test them in I-696



# Technical questions

If you have a bug, please report it. Otherwise, join the [Flow Users group](https://forms.gle/CuVBu6QtX3dfNaxz6) on Slack! You'll recieve an email shortly after filling out the form. 

# Getting involved

We welcome your contributions.

- Please report bugs and improvements by submitting [GitHub issue](https://github.com/flow-project/flow/issues).
- Submit your contributions using [pull requests](https://github.com/flow-project/flow/pulls). Please use [this template](https://github.com/flow-project/flow/blob/master/.github/PULL_REQUEST_TEMPLATE.md) for your pull requests.

# Citing Flow
If you are interested in extending our research, please consider citing our paper:
```
@article{cui2021scalable,
  title={Scalable multiagent driving policies for reducing traffic congestion},
  author={Cui, Jiaxun and Macke, William and Yedidsion, Harel and Goyal, Aastha and Urielli, Daniel and Stone, Peter},
  journal={arXiv preprint arXiv:2103.00058},
  year={2021}
}
```

If you use Flow for academic research, you are highly encouraged to cite the Flow paper:

C. Wu, A. Kreidieh, K. Parvate, E. Vinitsky, A. Bayen, "Flow: Architecture and Benchmarking for Reinforcement Learning in Traffic Control," CoRR, vol. abs/1710.05465, 2017. [Online]. Available: https://arxiv.org/abs/1710.05465

If you use the benchmarks, you are highly encouraged to cite our paper:

Vinitsky, E., Kreidieh, A., Le Flem, L., Kheterpal, N., Jang, K., Wu, F., ... & Bayen, A. M,  Benchmarks for reinforcement learning in mixed-autonomy traffic. In Conference on Robot Learning (pp. 399-409). Available: http://proceedings.mlr.press/v87/vinitsky18a.html

# Contributors

Flow is supported by the [Mobile Sensing Lab](http://bayen.eecs.berkeley.edu/) at UC Berkeley and Amazon AWS Machine Learning research grants. The contributors are listed in [Flow Team Page](https://flow-project.github.io/team.html).
