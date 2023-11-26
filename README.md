# Curvature Corrected Moving Average (CCMA)

![alt text](./figures/MA_vs_CCMA.gif "Moving Average vs. Curvature Corrected Moving Average Visualization")

The CCMA is a **model-free**, **general-purpose** smoothing algorithm designed for **2D/3D** paths. It
addresses the phenomenon of the inwards bending phenomenon in curves that commonly occurs with
conventional moving average filters. The CCMA method employs a **symmetric filtering**.
However, due to its symmetric approach, it primarily serves as accurate smoothing rather than state estimation.

The implementation offers a user-friendly experience (see minimal working examle), 
making it remarkably easy to apply filtering to given points represented as a numpy array. 
Users can effortlessly choose from different kernels, including truncated normal, uniform, or the sophisticated Pascal triangle kernel (default).

Furthermore, the implementation provides different boundary behaviors --
padding, wrapping, decreasing filtering width, 
or using no boundary strategy at all. 
This adaptability ensures that the implementation caters to a wide range of scenarios and preferences.

While the code itself may not provide a complete understanding, further details
and insights can be found in the paper.

If you use the CCMA, please cite the original [paper](https://ieeexplore.ieee.org/abstract/document/10186704?casa_token=sCW2rP_gkSUAAAAA:7MEXKPZzc0XU3YpXb6ayjTlCSrhMYROKe40QmfmABCYxmjoopMwrGztIDzH0F-icaJ6V56P9Aw):

```
@inproceedings{Steinecker23,
  title={A Simple and Model-Free Path Filtering Algorithm for Smoothing and Accuracy},
  author={Steinecker, Thomas and Wuensche, Hans-Joachim},
  booktitle={2023 IEEE Intelligent Vehicles Symposium (IV)},
  pages={1--7},
  year={2023},
  organization={IEEE}
}
```

An informative article that simplifies the explanation of CCMA can be found [here](https://medium.com/@steineckertommy/an-accurate-model-free-path-smoothing-algorithm-890fe383d163).

![alt text](./figures/MA_vs_CCMA.png "Moving Average vs. Curvature Corrected Moving Average")

### Minimal Working Example

```python
import numpy as np
from ccma.ccma import CCMA

# Create noisy points on an unit circle
n = 50
noise = np.random.normal(0, 0.05, (n, 2))
points = np.array([np.cos(np.linspace(0, 2*np.pi, n)),
                   np.sin(np.linspace(0, 2*np.pi, n))]).T
noisy_points = points + noise

# Create ccma-object and smooth points by using padding (default) and Pascal's Triangle kernel/weights (default)
ccma = CCMA(w_ma=5, w_cc=3)
points_smoothed = ccma.filter(noisy_points)
```