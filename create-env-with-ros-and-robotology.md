# How to create an environment with both ROS and Robotology packages

## Try to install ROS packages in an existing environment 

First of all, try to install a ROS package such as `ros-humble-desktop` on the `rosenv` environment created in the [previous hands on](create-ergocub-gz-sim-env.md):

~~~
conda activate robenv
conda install -c conda-forge -c robostack-jazzy ros-jazzy-desktop
~~~

As of February 2025, this will result in an error similar to:
~~~
UnsatisfiableError: The following specifications were found
to be incompatible with the existing python installation in your environment:

Specifications:

  - ros-jazzy-desktop -> python[version='3.11.*']

Your python: python=3.9

If python is on the left-most side of the chain, that's the version you've asked for.
When python appears to the right, that indicates that the thing on the left is somehow
not available for the python version you are constrained to. Note that conda will not
change your python version to a different minor version unless you explicitly specify
that.
~~~

Why this happens? Because in the `robenv` we did not select the version of Python we wanted to install, so the latest one (Python 3.13) was installed.
However, on RoboStack only Python 3.11 is supported, so this creates a problem of compatibility w.r.t. to the packages already installed in the environment.

You can fix this by explicitly asking for Python 3.11:
~~~
conda install -c conda-forge -c robotology python=3.11
~~~

This will appropriately uninstall the packages that depend on Python 3.9, and install the equivalent version that depend on Python 3.11.

## Create a new environment with both ROS and robotology packages

An alternative strategy (that may be easier in some cases) is just to create a new environment, called for example `robrosenv`, and install directly all the required packages:
~~~
conda create -n robrosenv
conda activate robrosenv
conda install -c conda-forge -c robostack-jazzy -c robotology ergocub-models gz-sim-yarp-plugins ros-jazzy-desktop
~~~


## Test ROS installed via conda

In both cases, in the environment in which `ros-jazzy-desktop` is installed, you should be able to run ROS programs and tools such as RViz. 

To test this, open a terminal and you can run rviz:
~~~
rosrun rviz rviz
~~~
