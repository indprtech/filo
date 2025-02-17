Chromium Embedded Framework (CEF) Standard Binary Distribution for Linux
-------------------------------------------------------------------------------

Date:             October 19, 2024

CEF Version:      130.1.2+g48f3ef6+chromium-130.0.6723.44
CEF URL:          https://bitbucket.org/chromiumembedded/cef.git
                  @48f3ef63e26c0e7b4d6980e71edf95a6b72302fc

Chromium Version: 130.0.6723.44
Chromium URL:     https://chromium.googlesource.com/chromium/src.git
                  @0927c68589810ccc6488dbc8c79c9d37e4a0d52f

This distribution contains all components necessary to build and distribute an
application using CEF on the Linux platform. Please see the LICENSING
section of this document for licensing terms and conditions.


CONTENTS
--------

bazel       Contains Bazel configuration files shared by all targets.

cmake       Contains CMake configuration files shared by all targets.

Debug       Contains libcef.so and other components required to run the debug
            version of CEF-based applications. By default these files should be
            placed in the same directory as libcef.so and will be copied there
            as part of the build process.

include     Contains all required CEF header files.

libcef_dll  Contains the source code for the libcef_dll_wrapper static library
            that all applications using the CEF C++ API must link against.

Release     Contains libcef.so and other components required to run the release
            version of CEF-based applications. By default these files should be
            placed in the same directory as libcef.so and will be copied there
            as part of the build process.

Resources   Contains resources required by libcef.so. By default these files
            should be placed in the same directory as libcef.so and will be
            copied there as part of the build process.

tests/      Directory of tests that demonstrate CEF usage.

  cefclient Contains the cefclient sample application configured to build
            using the files in this distribution. This application demonstrates
            a wide range of CEF functionalities.

  cefsimple Contains the cefsimple sample application configured to build
            using the files in this distribution. This application demonstrates
            the minimal functionality required to create a browser window.

  ceftests  Contains unit tests that exercise the CEF APIs.

  gtest     Contains the Google C++ Testing Framework used by the ceftests
            target.

  shared    Contains source code shared by the cefclient and ceftests targets.


USAGE
-----

Building using CMake:
  CMake can be used to generate project files in many different formats. See
  usage instructions at the top of the CMakeLists.txt file.

Building using Bazel:
  Bazel can be used to build CEF-based applications. CEF support for Bazel is
  considered experimental. For current development status see
  https://github.com/chromiumembedded/cef/issues/3757.

  To build the bundled cefclient sample application using Bazel:

  1. Install Bazelisk [https://github.com/bazelbuild/bazelisk/blob/master/README.md]
  2. Install the patchelf package:
     $ sudo apt install patchelf
  3. Build using Bazel:
     $ bazel build //tests/cefclient
  4. Run using Bazel:
     $ bazel run //tests/cefclient

  Other sample applications (cefsimple, ceftests) can be built in the same way.

  Additional notes:
  - To generate a Debug build add `-c dbg` (both `build` and `run`
    command-line).
  - To pass arguments using the `run` command add `-- [...]` at the end.

Please visit the CEF Website for additional usage information.

https://bitbucket.org/chromiumembedded/cef/


REDISTRIBUTION
--------------

This binary distribution contains the below components.

Required components:

The following components are required. CEF will not function without them.

* CEF core library.
  * libcef.so

* Unicode support data.
  * icudtl.dat

* V8 snapshot data.
  * snapshot_blob.bin
  * v8_context_snapshot.bin

Optional components:

The following components are optional. If they are missing CEF will continue to
run but any related functionality may become broken or disabled.

* Localized resources.
  Locale file loading can be disabled completely using
  CefSettings.pack_loading_disabled. The locales directory path can be
  customized using CefSettings.locales_dir_path. 
 
  * locales/
    Directory containing localized resources used by CEF, Chromium and Blink. A
    .pak file is loaded from this directory based on the value of environment
    variables which are read with the following precedence order: LANGUAGE,
    LC_ALL, LC_MESSAGES and LANG. Only configured locales need to be
    distributed. If no locale is configured the default locale of "en-US" will
    be used. Without these files arbitrary Web components may display
    incorrectly.

* Other resources.
  Pack file loading can be disabled completely using
  CefSettings.pack_loading_disabled. The resources directory path can be
  customized using CefSettings.resources_dir_path.

  * chrome_100_percent.pak
  * chrome_200_percent.pak
  * resources.pak
    These files contain non-localized resources used by CEF, Chromium and Blink.
    Without these files arbitrary Web components may display incorrectly.

* ANGLE support.
  * libEGL.so
  * libGLESv2.so
  Support for rendering of HTML5 content like 2D canvas, 3D CSS and WebGL.
  Without these files the aforementioned capabilities may fail.

* SwANGLE support.
  * libvk_swiftshader.so
  * libvulkan.so.1
  * vk_swiftshader_icd.json
  Support for software rendering of HTML5 content like 2D canvas, 3D CSS and
  WebGL using SwiftShader's Vulkan library as ANGLE's Vulkan backend. Without
  these files the aforementioned capabilities may fail when GPU acceleration is
  disabled or unavailable.


LICENSING
---------

The CEF project is BSD licensed. Please read the LICENSE.txt file included with
this binary distribution for licensing terms and conditions. Other software
included in this distribution is provided under other licenses. Please visit
"about:credits" in a CEF-based application for complete Chromium and third-party
licensing information.
