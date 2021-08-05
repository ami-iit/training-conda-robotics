# How to create an environment to simulate the iCub robot in Gazebo

## Check the environment

First of all, check if conda and mamba are correctly installed:
~~~
mamba info
~~~

The output should be something like:
~~~
     active environment : None
            shell level : 0
~~~

If that works fine, you can list all the existing environments with:
~~~
mamba env list
~~~

If you just installed `conda` you should only have the `base` environment.
It is recommended to not install scientific-related software in the `base`  environment, and only use `base` to install conda and related tools (such as `mamba`).

## Create the environment and install packages
Let's create an environment called `robenv` 
~~~
mamba create -n robenv
~~~

We can activate it via:
~~~
mamba activate robenv
~~~

Then install the packages necessary to run a Gazebo simulation of iCub:
~~~
mamba install -c conda-forge -c robotology icub-models gazebo-yarp-plugins
~~~

After the installation is completed, you can see the packages that are now installed in the environment with:
~~~
mamba list
~~~

## Run the simulation

Open three terminals, and in each one first of all run:
~~~
mamba activate robenv
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
