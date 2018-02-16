# Godot3-Win64-LSW-Build
Build of Godot 3 - without SCons

The new Godot 3.1-dev DLL build will be in synch with 3.1 - dev.
The development cycle has speed up enormously. There is no need to recompile Godot if extending Godot's class hierarchy. New Development can be kept in separate DLLs. With VS's Edit & continue feature & introduction of precompiled Headers the development cycle will shrink further.

Godot3.1dev-dllbuild-lsw-Win64.7z ( without Mono ) :

+ Godot3-LSW.exe (383 KB) with 101 DLL's
based on [master commit **79f48cd** v. 14.2.2018](https://github.com/godotengine/godot/commit/79f48cde3d9c47e64cca6090c3db0bff1c9e557f)

The build contains pythonscript.dll which allows to use PythonScript.
It is based on Python 3.64. No Installation of Python is needed. The Python 3 interpreter is included in the PythonScript.dll and the Python-runtime is in Python-Runtime-3.64.7z. 
**PythonScript is not functional yet.**


## New in build v. 2018-2-16
This build contains the possibility to get meaningful stack-trackes in case of crashes. 

Download [the pdb 7z](https://github.com/frank-lesser/Godot3-Win64-LSW-Build/blob/master/Godot3.1dev-dllbuild-lsw-Win64.7z), unzip it into the folder of **Godot3-lsw.exe**. In case of an engine crash you should see the execution-stack in the log.


The next major update which contains also 7z infrastructure is planned for end of February 2018:

## Further development plans:
+ Preload and delay load of Godot DLL's & own DLLs.
  + one set of DLLs for Editor & Runtime
  + Dynamic registration of DLLs
  + DLL-Versioning & Auto updater
  + Win64 debug builds, Win32 build & debug builds

+ More Language Bindings tighter integrated with Godot:
  + JavaScript ( based on MS-Chakra )
  + Smalltalk ( JIT-compiled )
+ JIT for GDScript

  Just in time compilaton based on our Smalltalk-JIT will speed up GDScript.
+ New Memory allocators

  experimiental faster allocation of Objects