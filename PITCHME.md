@title[Introduction]
## Conan.io

#### The C/C++ Package Manager for Developers

FISL18

---?image=assets/img/lego-dark-green.png
@title[Theme Switcher]

@div[left-70]
Hello!
<br>
<br>
**Uilian Ries**
<br>
<br>
C++ and Python Developer
<br>
Work at **@khomp**
<br>
<br>
@uilianries
<br>
@fa[github] @fa[twitter] @fa[linkedin]
@divend

@div[right-30]
![me](assets/img/me.png)
@divend

---?image=assets/img/lego-dark-red.png

### POPULAR C/C++ PROJECTS

##### Because you need good libraries

---?image=assets/img/lego-dark-blue.png
@title[A New Problem]

Let's start a new C++ project!

What does it need?

@div[left-50]
<ul>
  <li>OpenSSL</li>
  <li>Qt</li>
  <li>Boost</li>
  <li>OpenCV</li>
  <li>POCO</li>
</ul>
@divend

---?image=assets/img/lego-dark-green.png

#### ALL OF THEM NEED TO BE BUILT
@title[All need to be built]

* Download the source. Build on your machine
  - It may take several minutes, or even hours
  - There may be external dependencies
  - You need to know how to build

* Install by system package manager
  - The version may not be as expected
  - There may be a patch applied

---?image=assets/img/lego-dark-green.png

#### Build from source? Install from distro?

![build-all](assets/gif/good-bad-ugly.gif)

---?image=assets/img/lego-dark-red.png

### PACKAGE MANAGERS
@title[Package Managers]

##### How to avoid *externals* in your project

---?image=assets/img/lego-dark-green.png

#### POPULAR PACKAGE MANAGERS

@div[left-50]
<br>
<ul>
  <li>Python</li>
  <ul>
    <li>pip, Conda</li>
  </ul>
  <li>Rust</li>
  <ul>
    <li>Cargo</li>
  </ul>
  <li>Java</li>
  <ul>
    <li>Maven</li>
  </ul>
  <li>JavaScript</li>
  <ul>
    <li>npm</li>
  </ul>
</ul>
@divend
@div[right-50]
![languages](assets/img/languages.png)
@divend

---?image=assets/img/lego-dark-blue.png

![bjarne](assets/img/bjarne.png)

---?image=assets/img/lego-dark-blue.png

#### C++ UNIVERSE
@title[Cpp Universe]

@div[left-50]
<br>
<ul>
  <li>CONAN</li>
  <li>HUNTER</li>
  <li>BUCKAROO</li>
  <li>VCPKG</li>
  <li>CGET</li>
  <li>CPM</li>
<ul>
@divend
@div[right-30]
![cpp](assets/img/cpp-logo.png)
@divend

---?image=assets/img/lego-dark-red.png

## CONAN

Not the barbarian

![conan-barbarian](assets/gif/conan.gif)

---?image=assets/img/lego-dark-blue.png

@div[left-70]
<br>
<ul>
  <li>FOSS</li>
  <li>MIT License</li>
  <li>Decentralized, GIT style</li>
  <li>Handles from source/binaries</li>
  <li>Generators for CMake, VS, XCode, qmake …</li>
  <li>Developed in Python</li>
  <li>+100 contributors</li>
  <li>2K stars (Github)</li>
</ul>
@divend
@div[right-30]
![cpp](assets/img/logo.png)
@divend

---?image=assets/img/lego-dark-green.png

### INSTALL

`$ pip install conan`

---?image=assets/img/lego-dark-red.png

### CONAN IN ACTION
@title[Conan in Action]

Talk is cheap. Show me the code.

![torvalds](assets/img/torvalds.png)

---?image=assets/img/lego-dark-green.png

#### CONAN IN ACTION
@title[Conan in Action File]

* Digest MD5 using Poco project
* Check string by Boost Regex
* Build using CMake

![projects](assets/img/projects.png)

---?image=assets/img/lego-dark-green.png

#### CONAN IN ACTION
@title[Conan in Action Dir]

```
example
|   main.cpp
|   conanfile.txt
|   CMakeLists.txt
```

---?image=assets/img/lego-dark-green.png

#### CONAN IN ACTION
@title[Conan in Action main.cpp]

main.cpp

```cpp
#include <Poco/MD5Engine.h>
#include <boost/regex.hpp>
#include <iostream>

int main() {
    Poco::MD5Engine md5;
    md5.update("Hello World");
    std::string md5string = Poco::DigestEngine::digestToHex(md5.digest());
    std::cout << "MD5= " << md5string << '\n';

    boost::regex expr{R"(\w+\s\w+)"};
    std::cout << boost::regex_match("Hello World", expr) << '\n';
    return EXIT_SUCCESS;
}
```

---?image=assets/img/lego-dark-blue.png

#### CONAN IN ACTION
@title[Conan in Action conanfile]

conanfile.txt

```
[requires]
Poco/1.8.0.1@pocoproject/stable
Boost/1.9.0@conan/stable

[generators]
cmake
```

@[1-3]
@[5-6]

---?image=assets/img/lego-dark-green.png

#### CONAN IN ACTION
@title[Conan in Action cmake]

CMakeLists.txt - **TARGET**

```cmake
cmake_minimum_required(VERSION 2.8)
project(example CXX)

find_package(Boost 1.67.0 REQUIRED regex)
find_package(Poco 1.9.0 REQUIRED Foundation)

add_executable(example main.cpp)
target_link_libraries(example ${Boost_LIBRARIES} ${Poco_LIBRARIES})
```

@[1-2]
@[4-5]
@[7-8]

---?image=assets/img/lego-dark-green.png

#### CONAN IN ACTION
@title[Conan in Action cmake]

CMakeLists.txt - **WITH CONAN**

```cmake
cmake_minimum_required(VERSION 2.8)
project(example CXX)

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

add_executable(example example.cpp)
target_link_libraries(example ${CONAN_LIBS})
```

@[1-2]
@[4-5]
@[7-8]

---?image=assets/img/lego-dark-green.png

#### CONAN IN ACTION
@title[Conan in Action build]

How to Build

`$ conan install .`

```
PROJECT: Installing /home/conan/project/conanfile.txt
Packages
    OpenSSL/1.0.2o@conan/stable:0abbb2ea17cdc92f4a2ac8a9e55de717e3b5a9d1 - Download
    Poco/1.9.0@pocoproject/stable:8a67b44a092c0074e3cb946a9ddada338054b11e - Download
    boost/1.67.0@conan/stable:eacfdb5f448bfd89f0b2950fb6b7a79e44c7ea08 - Download
    bzip2/1.0.6@conan/stable:76f87539fc90ff313e0b3182641a9bb558a717d2 - Download
    zlib/1.2.11@conan/stable:d358fec34c04bcd89832a09158783c750a3304dc - Download
PROJECT: Generator cmake created conanbuildinfo.cmake
PROJECT: Generator txt created conanbuildinfo.txt
PROJECT: Generated conaninfo.txt
```

---?image=assets/img/lego-dark-green.png

#### CONAN IN ACTION
@title[Conan in Action build]

How to Build

```
$ conan install .
$ cmake .
$ cmake --build .
$ bin/example
```

@[1]
@[2]
@[3]
@[4]

---?image=assets/img/lego-dark-red.png

### CONAN IN A NUTSHELL
@title[Conan in a nutshell]

How the barbarian works.

![nutshell](assets/img/nutshell-conan.png)

---?image=assets/img/lego-dark-blue.png

#### UNDERSTANDING CONAN
@title[Understand Conan]

* Package naming
* System setup
* Package distribution
* Local cache

---?image=assets/img/lego-dark-green.png

#### PACKAGE NAMING
@title[Package Naming]

**`name/version@user/channel`**

* Examples
  * Poco/1.9.0@pocoproject/stable
  * Boost/1.67.0@conan/testing
  * Qt/5.11.0@bincrafters/stable

---?image=assets/img/lego-dark-green.png

#### SYSTEM SETUP
@title[System Setup]

* Based on Profiles

**Conan settings + Host configuration = Profile**

---?image=assets/img/lego-dark-green.png

#### PROFILE
@title[profile]

`$ conan profile show default`

```
Configuration for profile default:

[settings]
os=Linux
os_build=Linux
arch=x86_64
arch_build=x86_64
compiler=gcc
compiler.version=8
compiler.libcxx=libstdc++11
build_type=Release
[options]
[build_requires]
[env]
```

---?image=assets/img/lego-dark-green.png

#### PACKAGE DISTRIBUTION
@title[package distribution]

* Git flavor
* Support multiple remotes
* Central repository - JFrog Bintray
* Easy to run a local server instance
  * `$ conan_server`
* JFrog Artifactory can be used together

---?image=assets/img/lego-dark-red.png

#### PACKAGE DISTRIBUTION
@title[package distribution]

![distribution](assets/img/systems.png)

---?image=assets/img/lego-dark-green.png

#### LIST REMOTES
@title[list remotes]

`$ conan remote list`

```
my-company: http://172.0.1.42:9300
conan-center: https://conan.bintray.com
bincrafters: http://api.bintray.com/conan/bincrafters/public-conan
```
