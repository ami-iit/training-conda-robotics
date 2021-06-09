## Check the environment

First of all, check if conda is correctly installed:
~~~
conda info
~~~

The output should be something like:
~~~
     active environment : None
            shell level : 0
~~~

If that works fine, you can list all the existing environments with:
~~~
conda env list
~~~

If you just installed `conda` you should only have the `base` environment.
It is recommended to not install scientific-related software in the `base`  environment, and only use `base` to install conda and related tools.

## Create the environment and install packages
Let's create an environment called `robenv` 
~~~
conda create -n robenv
~~~

We can activate it via:
~~~
conda activate robenv
~~~

Then install the packages necessary to run a Gazebo simulation of iCub:
~~~
conda install -c conda-forge -c robotology icub-models gazebo-yarp-plugins
~~~

After the installation is completed, you can see the packages that are now installed in the environment with:
~~~
conda list
~~~

➡️ Note: if the installation process is slow, you can try to use [`mamba`](https://github.com/mamba-org/mamba), a fast drop-in replacement for conda, with `conda install -c conda-forge -n base mamba` . `mamba` is a drop-in replacement for conda, so you should be able to run all the documented steps with `mamba` in place of `conda` and everything should work.

## Run the simulation

Open three terminals, and in each one first of all run:
~~~
conda activate robenv
~~~
to activate the environment. 

Now, in the first terminal run the yarp name server:
~~~
yarpserver --write
~~~

In the second terminal, run Gazebo:
~~~
gazebo
~~~

Once gazebo is running, spawn the `iCubGazeboV2_5_visuomanip` model and launch it in simulation.

In the third terminal, run:
~~~
yarpmotorgui --robot icubSim
~~~
In the initial gui, deselect the two legs and launch it. Now you can control the robot.
