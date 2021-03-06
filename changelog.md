# 2018-08-10
- the build has been synchronized with 3.1 dev-master commit [9bd5315](https://github.com/godotengine/godot/commit/9bd5315d30be8cb162bd7fee6a7db17f65b5057d) v. 7. August 2018

- [PR 20137](https://github.com/godotengine/godot/pull/20137) (Reduce unnecessary COW on Vector by make writing explicit) was not taken.

- CPP Object has been reduced ( sizes in Bytes x64 - build)

      sizeof(Object)  = 24 - in dev-master 224
      sizeof(Node)    = 144 - in dev-master 512
      sizeof(Control) = 472 - in dev-master 1104 

- Object::cast_to has been eliminated, the next build will eliminate Ref<T>, WeakRef<T> and replace reference counting with generational GC.

# 2018-07-10
- Synch with 3.05 maintenance release
+ the build is full modularized - The DLLs are self registering & initializing. Depending on the entries in Project-settings Godot core DLLs, like Visual-server.DLL, Audio-server.DLL, Scene_2d.DLL, Scene_3D.DLL and many others can be loaded.
+ a new section **[preloaded_editor_module]** has been added, which lists dlls which are only loaded if the editor is started.

+ new logging modes
  + mode/visual_server
  + mode/graphic_driver
# 2018-06-25
- Synch with 3.05 maintenance release
- Internal optimizations, new BaseObject.DLL, smaller Object & Node-Sizes
- Logging output to Visual-Studio Debug-Window
- Log file-names of *.pck files ( --path <game-path> --main-pack )
# 2018-06-14
- Synch with 3.03 maintenance release
- Internal optimizations, preparation for Garbage-collection
- New DLL Variant.DLL
# 2018-06-10
- Internal optimizations, unique Strings (StringName instances) takes now 4 byte instead of 8 byte
- Sizes of Onject subclasses has been shrunken. 
- SpingArm node has been added [master PR 18822](https://github.com/godotengine/godot/pull/18822)

# 2018-06-07
- Internal optimizations 
- shrinking of core.dll, new StringName.dll
- moved Geometry to Math3D.dll
- preparation for typed GDScript dll & new AnimationEditor
- fixed crash when invoking EditorSettings dialog

# 2018-06-03
- Internal optimizations ( of instance size of C++ classes)
- update to 3.03 rc3 dev-master commit [8684b63](https://github.com/godotengine/godot/commit/8684b631182dffebba27bdf538129818321d0d7d)
- reduction of DLL dependencies
# 2018-05-29
+ fixed crashes due to python36.dll on toplevel ( moved to gd-modules )
+ main.dll does not load editor.dll & editor plugin dlls, enabling small runtimes

# 2018-05-27
+ synch with [master 130fd6b](https://github.com/godotengine/godot/commit/130fd6bcb88d7b297b13c3ed20a715b5ab9cce47)

# 2018-05-12
+ synch with [master 81b1d3c](https://github.com/godotengine/godot/commit/81b1d3c846de263cf843e9e0e9d7c0c0a94f65c8) 

dynamic registration of DLLs ( WIP ), to be able to compose the modularized Godot build DLLs, needed by the application


# 2018-04-23
+ synch with [master 1c41953(https://github.com/godotengine/godot/commit/1c419531a009f48aa074f9b5f93b98d387c33723) v. 2018.4.23
+ Engine 

  + Multi-View (WIP)
    
    allows to open more than one Window:

        view = View.new()
	    main_scene = ResourceLoader.load("res://class-browser/main.tscn")
	    view.create(Rect2(Vector2(100,100), Vector2(400,300)), "test", main_scene)

  + cherry-picks

    GLES3 rasterizer is now in sync with engine

+ GDScript

  + dynamic scripting

        extends Control
        var context = GDScript.new()

        func _ready():
	      var vi = Engine.get_version_info()
	      OS.set_window_title("Godot-LSW "+vi["build"])
        func _on_Button_pressed():
        #	$result.text = String(perform(self, "answer42"))
        #	$result.text = String(perform(self, "answer", 42))
        #	$result.text = String(perform_with_args(self, "ans"+"wer", Array([42])))
        #	$result.text = String(self.callv("ans"+"wer", Array([42])))
      	$result.text = String(context.evaluate_string($input.text))

        func answer42():
	        return(42)

        func answer(number):
	        return(number)

  + cherry-picks

    + multiline-comments

      Introduces C-Style /* */ comments to GDScript like proposed in [#18228](https://github.com/godotengine/godot/issues/18228).

# 2018-04-12
+ GDScript
  + performance improvements in method lookup
  + new binary literals in form 0b[01]*

+ GD Classes
  + Engine.get_profiler()

    answers a Profiler object which measures execution times of internal GD operations.
  + OS.start_timer_usec(), OS.get_timer_usec()

    timing functions with usec resulution

+ LUA-Integration

  LUA can be integrated within GDScript. LuaScript is still WIP.

  from example LUA_HelloWord projectproject in [GD-projects.7z]((https://github.com/frank-lesser/Godot3-Win64-LSW-Build/blob/master/GD-projects.7z)) :

      var luaVM_module = preload("/Dev/Godot/Godot3/Godot3-LSW/gd-modules/luavm.gdns");
      onready var luaVM_instance = GDLuaVM.new()
      luaVM_instance.run_file("hello_world.lua")
      String(luaVM_instance.call_function("factorial", 5))

# 2018-04-04
+ Intermediate build & synch with master
  I am still working on LUA integration.
# 24.3.2018
+ Converted various Modules found on Github ( if still for 2.x converted to 3.x ) to **GD-CPP-Native** DLLs:
  + PDF based on libharu ( not tested yet )
  + NativeDiallogs ( contains FileDialog, ColorDialog & MessageDialog )
  + Voxel, PerlinNoise, Heightmap, OpenSimplex
  + OAML ( Script test is not fixed yet )
  + XML Exporter [pugixml](https://pugixml.org)
 
+ Fixes Editor crashes due to lazy loading of Plug-Ins
+ Added logging option for **emit_signal**

  Logging of emit_signal can now added to **project.godot**, logging voor connect & disconnect is in preparation
+ Several internal optimizations
+ Internal advances on LuaScript
+ Prepared other modules for inclusion

# 2018-03-224
+ Added Steam
+ Internal engine optimizations
+ internal LUA work
# 2018-03-19
+ Added libopenmpt
+ Added mono
+ improved LuaScript
+ changed ERR_*, WARN_* logging & **call_deferred** to use the new project.godot logging options.
+ added Smaple projects in Projects.7z
+ Engine Refactorings to load more DLLs as GD-CPP-Natives

# 2018-03-15
+ Added Environment Variables
  + **GODOT_LSW_PATH** has priority over APPDATA
  + **GODOT_LSW_DATA_PATH**
  + **GODOT_LSW_CACHE_PATH**

  the new Environment Variables are useful if you have more than 1 Project which uses GDNative modules & want to use a central place for the GGodot Binaries, Data & Cache.

+ Section **[singletons**] in project.godot

  Since the build allows now dynamic loading of former statically imported DLLs under this section DLLs and plugins will be listed which are not belonging to the editors base configuration.

        [gdnative]
        singletons = [ "res://gd-modules/enet.gdnlib", "res://gd-modules/openssl.gdnlib" ]

+ Added [GD-Projects.7z](https://github.com/frank-lesser/Godot3-Win64-LSW-Build/blob/master/GD-projects.7z) which provides sample code for the new features.
+ All Modules converted to GDNative:
  + For example ENet is now no longer part of the core GD3-LSW engine
    To use the **NetworkedMultiplayerENet** class you need to load the ENet GDNative Module:

        var enet_module = preload("user://gd-modules/enet.gdns");

    The adopted example is provided under GD-Projects/networking/multiplayer_pong

    For the editor enet is a "preloaded" singleton in the main ***project.godot***. If it is omitted from the ***[singletons]*** section, the Asset Library Tab will not show in the Project-Manager.

  + GD-Editor only GD-Native extensions
    + Theora

    The Video imported is a GD-Editor only extension. To add it under the section preset_modules in **editor-settings-3-lsw.tres**
            Therora = "res://gd-modules/editor/Module_theora.gdns"
+ New Modules added to GDNative:
  + SQLite

    To use the **SQLite** class add the code bleow to the beginning of your script:

        var sqlite_module = preload("user://gd-modules/gdsqlite.gdns");

    The adopted example is provided under GD-Projects/SQLite
# 2018-03-11
+ added extended logging to Project-Settings file (godot.project)

  it is now possible to specify whether warnings/errors/failures should be logged in extended 8 including source file-name ) or short form:

      logging/file_logging/enable_file_logging = true
      logging/file_logging/log_path = "godot-log.txt"
      logging/mode/short=true # omits the filename & line-number
      logging/mode/errors=true # allows filtering of ERROR_* entries
      logging/mode/warnings=true #allows filtering of WARN_* entries
      logging/mode/fails=true #allows filtering of FAIL_* entries
      logging/mode/deferred_calls=true #allows filtering of deferred_calls
+ added GD-Native C++

  it is now possible to specify C++ DLLs as GD-Native modules.
  A DLL, containing C++ engine code - produced with the Godot3-LSW SDK, can now
  loaded with preset(Path.gdns). 

# 2018-03-03

+ Added a new **Dlls** Tab to Project-settings. The Tab shows all DLLs, currently loaded

# 2018-02-27
+ Added a new Menu **Update** to Editor/help. A currently empty update Dialog is popped up, which will show later new Versions of DLLs found on a [WinSparke](https://winsparkle.org) enabled Server.

# 2018-02-23
+ Added [symbol-files](https://github.com/frank-lesser/Godot3-Win64-LSW-Build/blob/master/Godot3.1dev-dllbuild-lsw-Win64-pdb.7z) to enable a memaningful stack-trace
