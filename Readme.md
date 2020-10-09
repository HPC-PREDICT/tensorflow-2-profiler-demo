## TensorFlow 2.2 Profiler demo with MNIST on Piz Daint

Taken from the [Tensorboard docs](https://github.com/tensorflow/tensorboard/blob/master/docs/tensorboard_profiling_keras.ipynb).

Steps to reproduce this example:

### Setup

Load the daint-gpu & Tensorflow modules
```
module load daint-gpu
module load TensorFlow/2.2.0-CrayGNU-20.08-cuda-10.1.168
```
and set up this example with
```
git clone tensorflow-2-profiler-demo
cd tensorflow-2-profiler-demo
mkdir site-packages && cd site-packages
pip install --upgrade --ignore-installed --target $(pwd) tensorflow-datasets tensorboard==2.2.0 tensorboard_plugin_profile==2.2.0
cd ..
```

### Run training
```
PYTHONPATH=$(pwd)/site-packages:${PYTHONPATH} srun -u -l -C gpu --partition=debug python3 train.py
```

### Run Tensorboard
```
PYTHONPATH=$(pwd)/site-packages:${PYTHONPATH} python3 -m tensorboard.main --host daintXXX --port 6006 --logdir logs
```

You should now be able to open the `PROFILE` tab on http://daintXXX:6006 in the browser.
