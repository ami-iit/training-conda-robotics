# How to create an environment to simulate the iCub robot in Gazebo

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

Then install the packages necessary to run a gz-sim simulation of ergoCub:
~~~
conda install -c conda-forge ergocub-models gz-sim-yarp-plugins
~~~

After the installation is completed, you can see the packages that are now installed in the environment with:
~~~
conda list
~~~

## Run the simulation

For each terminal you open, remember to always run:

~~~
conda activate robenv
~~~

to activate the environment. 

Now you can simulate ergoCub following the docs in https://github.com/robotology/gz-sim-yarp-plugins/blob/main/docs/how-to-use-plugins-with-ergoCub.md .
