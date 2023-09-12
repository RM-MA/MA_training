## 1.
User
-- Found PCL: pcl_common;/usr/lib/x86_64-linux-gnu/libboost_system.so.1.71.0;/usr/lib/x86_64-linux-gnu/libboost_filesystem.so;/usr/lib/x86_64-linux-gnu/libboost_date_time.so;/usr/lib/x86_64-linux-gnu/libboost_iostreams.so.1.71.0;/usr/lib/x86_64-linux-gnu/libboost_regex.so  
CMake Error at CMakeLists.txt:47 (find_package):
  By not providing "Findcartographer.cmake" in CMAKE_MODULE_PATH this project
  has asked CMake to find a package configuration file provided by
  "cartographer", but CMake did not find one.

  Could not find a package configuration file provided by "cartographer" with
  any of the following names:

    cartographerConfig.cmake
    cartographer-config.cmake

  Add the installation prefix of "cartographer" to CMAKE_PREFIX_PATH or set
  "cartographer_DIR" to a directory containing one of the above files.  If
  "cartographer" provides a separate development package or SDK, be sure it
  has been installed.


-- Configuring incomplete, errors occurred!
See also "/home/dan/cartographer_ws/build_isolated/cartographer_ros/CMakeFiles/CMakeOutput.log".
<== Failed to process package 'cartographer_ros': 
  Command '['/home/dan/cartographer_ws/install_isolated/env.sh', 'cmake', '/home/dan/cartographer_ws/src/cartographer_ros/cartographer_ros', '-DCATKIN_DEVEL_PREFIX=/home/dan/cartographer_ws/devel_isolated/cartographer_ros', '-DCMAKE_INSTALL_PREFIX=/home/dan/cartographer_ws/install_isolated', '-DPYTHON_EXECUTABLE=/usr/bin/python3', '-G', 'Unix Makefiles']' returned non-zero exit status 1.

Reproduce this error by running:
==> cd /home/dan/cartographer_ws/build_isolated/cartographer_ros && /home/dan/cartographer_ws/install_isolated/env.sh cmake /home/dan/cartographer_ws/src/cartographer_ros/cartographer_ros -DCATKIN_DEVEL_PREFIX=/home/dan/cartographer_ws/devel_isolated/cartographer_ros -DCMAKE_INSTALL_PREFIX=/home/dan/cartographer_ws/install_isolated -DPYTHON_EXECUTABLE=/usr/bin/python3 -G 'Unix Makefiles'

The error you are facing now is related to CMake not finding the Cartographer package configuration file (`cartographerConfig.cmake` or `cartographer-config.cmake`).

Here's the main error message:

```
Could not find a package configuration file provided by "cartographer" with
any of the following names:

  cartographerConfig.cmake
  cartographer-config.cmake
```

This error indicates that Cartographer has either not been installed or its installation paths are not being recognized by CMake.

Here's what you can do:

1. **Ensure Cartographer is Installed**: If you haven't installed Cartographer, you need to do so. If you're following a specific guide, make sure you've followed all the steps.

2. **Set CMAKE_PREFIX_PATH**:
   You can manually inform CMake where to find Cartographer by setting the `CMAKE_PREFIX_PATH` variable. If you know where `cartographerConfig.cmake` or `cartographer-config.cmake` is located, provide its path to CMake.

   For example:
   ```bash
   catkin_make_isolated --install -DCMAKE_PREFIX_PATH=/path/to/cartographer/installation
   ```
   Replace `/path/to/cartographer/installation` with the appropriate path.

3. **Source the Cartographer Installation**:
   If you've installed Cartographer in a non-standard location (e.g., a workspace), you need to source its environment setup file to update relevant environment variables.
   
   ```bash
   source /path/to/cartographer/install/setup.bash
   ```
   After sourcing, try running the `catkin_make_isolated` command again.

4. **Check Cartographer Installation Path**:
   If you've installed Cartographer using a tool like `catkin_make`, then the required files might be in the `devel` or `install` space of that workspace. 

   Look for `cartographerConfig.cmake` or `cartographer-config.cmake` in your system to identify the correct directory. You can use the `find` command:

   ```bash
   find /home/dan -name "cartographerConfig.cmake" 
   ```
   Or, 
   
   ```bash
   find /home/dan -name "cartographer-config.cmake"
   ```
   
   Once located, use the path to inform CMake as described in the second step.

Proceed with one of these steps based on your setup, and then try building your ROS workspace again. If the issue persists or if there are other errors, please provide further information.

## 2.
find /home/dan -name "cartographer-config.cmake"
Seems like I find nothing

Alright, if `find` didn't return any results for `cartographer-config.cmake`, it's possible that Cartographer might not be correctly installed or built in your system.

To resolve the issue, let's try installing Cartographer:

1. **Clone and Build Cartographer**:
   
   If you haven't already, clone Cartographer's repository and build it:

   ```bash
   cd /home/dan/cartographer_ws/src
   git clone https://github.com/cartographer-project/cartographer.git
   cd ..
   catkin_make_isolated --install
   ```

   Note: The above steps assume that you're using a catkin workspace named `cartographer_ws`. Adjust paths if necessary.

2. **Source the Installation**:

   Once built, source the installation environment:

   ```bash
   source /home/dan/cartographer_ws/install_isolated/setup.bash
   ```

3. **Re-Attempt Building cartographer_ros**:

   After sourcing the setup file, go back to your workspace and try building `cartographer_ros` again:

   ```bash
   cd /home/dan/cartographer_ws
   catkin_make_isolated --install
   ```

4. **Install Cartographer using ROS Dependencies**:

   As an alternative, you can also try installing Cartographer using `rosdep` which handles ROS dependencies:

   ```bash
   cd /home/dan/cartographer_ws
   rosdep install --from-paths src --ignore-src -r -y
   ```

   After installing dependencies, run `catkin_make_isolated --install` again.

One of these steps should help in resolving the missing `cartographer-config.cmake` issue. If you're still facing challenges, consider referring to the official installation guide of Cartographer to ensure that you haven't missed any steps.

## 3.
-- Could NOT find Lua (missing: LUA_LIBRARIES LUA_INCLUDE_DIR) 
CMake Error at cmake/modules/FindLuaGoogle.cmake:217 (MESSAGE):
  Did not find Lua >= 5.2.
Call Stack (most recent call first):
  CMakeLists.txt:41 (find_package)


-- Configuring incomplete, errors occurred!
See also "/home/dan/cart_ws/build_isolated/cartographer/install/CMakeFiles/CMakeOutput.log".
See also "/home/dan/cart_ws/build_isolated/cartographer/install/CMakeFiles/CMakeError.log".
<== Failed to process package 'cartographer': 
  Command '['cmake', '/home/dan/cart_ws/src/cartographer', '-DCMAKE_INSTALL_PREFIX=/home/dan/cart_ws/install_isolated', '-G', 'Unix Makefiles']' returned non-zero exit status 1.

Reproduce this error by running:
==> cd /home/dan/cart_ws/build_isolated/cartographer && cmake /home/dan/cart_ws/src/cartographer -DCMAKE_INSTALL_PREFIX=/home/dan/cart_ws/install_isolated -G 'Unix Makefiles'

Command failed, exiting.


This error indicates that CMake can't find the Lua libraries (version >= 5.2) on your system. Cartographer requires Lua for its configuration files.

To resolve this, you'll need to install the required Lua libraries:

1. **Install Lua Libraries**:
   ```bash
   sudo apt-get install liblua5.2-dev
   ```

   If you've already installed a Lua version other than 5.2, there might be conflicts. Ensure that version 5.2 is the one being detected or manually point CMake to the appropriate paths.

2. **Retry Building Cartographer**:
   Navigate back to your Cartographer workspace and try building again:
   ```bash
   cd /home/dan/cart_ws
   catkin_make_isolated --install
   ```

3. **Manually Indicate Lua Path** (if necessary):

   If you have Lua 5.2 installed, but CMake still cannot find it, you can manually point to its path using the `LUA_INCLUDE_DIR` and `LUA_LIBRARIES` variables:

   ```bash
   cd /home/dan/cart_ws
   catkin_make_isolated --install -DLUA_INCLUDE_DIR=/path/to/lua/include -DLUA_LIBRARIES=/path/to/lua/lib
   ```

   Replace `/path/to/lua/include` and `/path/to/lua/lib` with the correct paths where Lua headers and libraries are located.

Proceed with these steps based on your current setup, and then try building Cartographer again. If the issue persists or if you encounter other errors, please provide additional information.

## 4 
User
[ WARN] [1694528467.599063178]: MessageFilter [target=odom ]: Dropped 100.00% of messages so far. Please turn the [ros.gmapping.message_filter] rosconsole logger to DEBUG for more information.

The warning you're seeing indicates that the `gmapping` node's internal `MessageFilter` is dropping all the messages intended for the target frame `odom`. This is typically because the necessary transformations are not available in a timely manner.

Here are steps you can take to debug and resolve the issue:

1. **Enable DEBUG Logging**:
   - As suggested by the warning, turn on DEBUG logging for `ros.gmapping.message_filter`:
     ```bash
     rosconsole set /ros.gmapping.message_filter DEBUG
     ```
     This should give you more verbose output that will help in diagnosing the exact issue.

2. **Check TF Tree**:
   - Ensure that the transformation between `odom` and the laser's frame is being published.
     ```bash
     rosrun tf view_frames
     ```
     Examine the generated `frames.pdf` to ensure all expected transformations are present.

3. **Check Timestamps**:
   - Ensure that the timestamps on your messages (like `/scan` and `/odom`) are consistent and correct. Large discrepancies can cause TF to drop messages.

4. **Check TF Broadcast Rate**:
   - If transforms are being published too infrequently, it could lead to dropped messages. Ensure that any nodes responsible for broadcasting the relevant TFs are doing so at a suitable rate.

5. **Inspect the `odom` Topic**:
   - Confirm that the `/odom` topic is actively publishing data with the correct timestamps.
     ```bash
     rostopic echo /odom
     ```

6. **Launch Order**:
   - Ensure you launch nodes in the right order. Nodes responsible for broadcasting TFs (like `robot_state_publisher`) should typically be launched before nodes like `gmapping`.

7. **Buffer Size**:
   - The `MessageFilter` in ROS works with a buffer of transformations to allow for some delay in TF publishing. If your system has significant delays, you might need to adjust the buffer size. However, this would typically be done in the node's code or through a parameter, and it's more of an advanced adjustment. 

8. **Odometry Source**:
   - Confirm that your odometry source is functioning correctly. If you're simulating the robot, tools like Gazebo sometimes can introduce delays or issues with odometry.

9. **Network Issues**:
   - If you're working with multiple machines, ensure they are properly networked, the `ROS_MASTER_URI` is set correctly on all of them, and the system clocks are synchronized (using tools like `chrony` or `ntp`).

By systematically working through these suggestions, you should be able to identify the root cause and ensure that the necessary transformations are available for `gmapping` to operate correctly.