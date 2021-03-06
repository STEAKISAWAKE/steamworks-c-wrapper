This library wraps around Valve's Steam API (Steamworks) to allow C programs to use it.

Basic instructions:

Linux
-----
 * Get the Steamworks SDK. You should know how to do this.
 * Install the SDK in a system search path or otherwise set an environment variable pointing to it (e.g. export STEAMWORKS_ROOT="dependencies/steamworks")
The FindSTEAMWORKS.cmake module is pretty bad right now...You'll have to edit it manually for your system. I know, I don't like it either, but that's the current state of affairs.
 * Run cmake.
 * Run make
 * Run make install
The library and headers will be be in lib/ and include/

Windows
-------
I'm not quite sure as to the exact steps to compile this on Windows as I don't have a Windows development environment, but, roughly:
 * Get the Steamworks SDK.
 * Do something such that CMake sees an environment variable telling it where you downloaded the SDK. If you're running a shell that supports SH scripts, then you can do export STEAMWORKS_ROOT="whatever/the/path/is"
If not, I'm not sure what you could do. I'd assume there's a batch equivalent? Maybe you could pass it as an argument to CMake? Modify CMakeLists and do set(STEAMWORKS_ROOT "whatever/the/path/is")?
Windows users, please let me know how you do it.
 * After doing that, run cmake, making sure it knows where STEAMWORKS_ROOT is.
 * make
 * make install

Using this library
------------------
 * Include steam_wrapper.h (should be #include \<steamworks_cwrapper/steam_wrapper.h>) (if you're reading this as a raw text file instead of on GitHub, the \ is to escape GitHub Flavored Markdown)
 * Take a look at steam_wrapper.h. Note two things: 1) Everything's prepended with c_. So you'd call c_SteamAPI_Init() instead of SteamAPI_Init().
    2) A class's member function is called by c_SomeClass_DoSomething(), instead of SomeClass::DoSomething() or SomeClass_instance.DoSomething().


General notes:
-------------
STEAMWORKS_SDK should point to the directory containing the "sdk" folder in the zip download. For example:
/home/ciprian/programming/c/steamapi-c-wrapper/dependencies/steamworks/sdk/redistributable_bin/linux32/
Is the full path to the location of the .so cmake will link against.
Whereas, you will set STEAMWORKS_SDK to:
/home/ciprian/programming/c/steamapi-c-wrapper/dependencies/steamworks

Q: "So when I export the steamworks sdk location as an environment variable do I want to export the location with the Readme.txt and the client, glmgr, public, redistributable_bin, etc. folders? Or the one above it?"
A: The one above it. It should just have a folder named "sdk"




Also, you need to define bool before you include the wrapper's header. Otherwise, a C compiler will slap you with a fish.
This could probably be changed so it just uses an int which it converts to a bool in the C++ code, but I'll leave it like this for the moment.