## How to create an environment to quickly develop a project

Let's say that you want to work on an issue that is affecting (for example) the [iDynTree library](https://github.com/robotology/idyntree). 
How do you quickly setup an environment to work on it?

## Clone the repo

First of all, you can clone the repo in the location that you prefer:
~~~
git clone https://github.com/robotology/idyntree
~~~

## Create environment
After you clone the repository, you can navigate to the `idyntree` directory:
~~~
cd idyntree
~~~

You can create a conda environment inside it, using the `-p` option of conda create to create an environment in a given directory, as opposed to create an environment by specifying a name (with `-n`)
~~~
conda -p ./env
~~~

After you create this environment, you can list all the environments in the system with `conda env list`:
~~~
conda env list
~~~

In this list, you should see the difference between the one that you created with a name (with `-n`) that were created in `miniforge3\envs`, and the one created with the directory (`-p`) that are in arbitrary directories.

After you created the environment by specifying its location, you can activate it with:
~~~
conda activate ./env
~~~

Then you can install the dependencies of the project, both its dependencies and the tools necessary to build:
~~~
conda install -c conda-forge -c robotology compilers cmake pkg-config ninja irrlicht yarp osqp-eigen icub-main eigen ipopt libxml2
~~~
If you are on Windows and you use Visual Studio 2019, you also need to install:
~~~
conda install -c conda-forge vs2019_win-64
~~~

After installing the dependencies, you can then create a build directory and build the project as usual: 
~~~
mkdir build
cd build
cmake -GNinja -DCMAKE_BUILD_TYPE=Release -DBUILD_TESTING:BOOL=ON -DCMAKE_INSTALL_PREFIX=./install ..
cmake --build . 
ctest
~~~

