# How to create an environment with both ROS and Robotology packages

## Try to install ROS packages in an existing environment 

First of all, try to install a ROS package such as `ros-noetic-desktop` on the `rosenv` environment created in the [previous hands on](create-icub-gazebo-env.md):

~~~
mamba activate robenv
mamba install -c conda-forge -c robostack ros-noetic-desktop
~~~

As of June 2021, this will result in an error such as:
~~~
UnsatisfiableError: The following specifications were found
to be incompatible with the existing python installation in your environment:

Specifications:

  - ros-noetic-desktop -> python[version='3.6.*|3.8.*']

Your python: python=3.9

If python is on the left-most side of the chain, that's the version you've asked for.
When python appears to the right, that indicates that the thing on the left is somehow
not available for the python version you are constrained to. Note that conda will not
change your python version to a different minor version unless you explicitly specify
that.
~~~

Why this happens? Because in the `robenv` we did not select the version of Python we wanted to install, so the latest one (Python 3.9) was installed.
However, on RoboStack only Python 3.8 is supported, so this creates a problem of compatibility w.r.t. to the packages already installed in the environment.

You can fix this by explicitly asking for Python 3.8:
~~~
mamba install -c conda-forge -c robotology python=3.8
~~~

This will appropriately uninstall the packages that depend on Python 3.9, and install the equivalent version that depend on Python 3.8.

## Create a new environment with both ROS and robotology packages
An alternative strategy (that may be easier in some cases) is just to create a new environment, called for example `robrosenv`, and install directly all the required packages:
~~~
mamba create -n robrosenv
mamba activate robrosenv
mamba install -c conda-forge -c robostack -c robotology icub-models gazebo-yarp-plugins ros-noetic-desktop
~~~


## Test ROS installed via conda

In both cases, in the environment in which `ros-noetic-desktop` is installed, you should be able to run ROS programs and tools such as RViz. 
To test this, open two terminals, in both of which you first run `conda activate robrosenv`. 

In the first one, you run roscore:
~~~
roscore
~~~

In the second one, you run rviz:
~~~
rosrun rviz rviz
~~~
