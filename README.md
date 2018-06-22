How to build tensorflow on Windows in China with VS2017
======================================================
0.you need VPN in China

1.download tensorflow_master.zip

2.download tools: bazel zip file for windows, msys2 for windows, anaconda3 for windows

3.install msys2 in C:\XXX, assume it is C:\tensorflow_tools, bring up msys2 shell, and run "pacman -Syuu --noconfirm", and then "pacman -S --noconfirm unzip perl patch", result: C:\tensorflow_tools\msys64

4.install anaconda3 in same folder as msys3, assume it is C:\tensorflow_tools, result: C:\tensorflow_tools\Anaconda3

5.unzip bazel zip file to C:\tensorflow_tools

6.unzip tensorflow_master.zip to a folder, assume it is D:\tf\tensorflow-master

7.run following commands in cmd:
        
        set BAZEL_SH=C:\tensorflow_tools\msys64\usr\bin\bash
        set PYTHON_DIRECTORY=tensorflow_tools\Anaconda3
        set BAZEL_VC=C:\Program Files (x86)\Microsoft Visual Studio\2017\Professional\VC
        if not exist C:\tools md C:\tools
        if not exist C:\tools\bazel md C:\tools\bazel
        if not exist C:\tools\bazel\bazel.exe copy C:\tensorflow_tools\bazel.exe C:\tools\bazel\bazel.exe
        set path=C:\tools\bazel;%path%
        set path=C:\tensorflow_tools\msys64\usr\bin;%path%
        set path=C:\tensorflow_tools\Anaconda3;%path%
        set path=C:\tensorflow_tools\Anaconda3\Scripts;%path%
        cd /d D:\tf\tensorflow-master
        where git
        where python
        where bazel
        where unzip
        where perl
        where patch
        rem MUST use slash "/" path separator
        %BAZEL_SH% -l %cd%/tensorflow/tools/ci_build/windows/cpu/pip/build_tf_windows.sh
        pause
        
8.if you don't have VS2017, download it from www.visualstudio.com, VS2015 has a bug, cannot compile openssl.
9.to test tensorflow with python, you need install python modules:

        set path=C:\tensorflow_tools\Anaconda3;%path%
        set path=C:\tensorflow_tools\Anaconda3\Scripts;%path%
        cmd /k
        
        pip install google pyreadline portpicker absl-py astor gast grpcio protobuf termcolor msgpack

<div align="center">
  <img src="https://www.tensorflow.org/images/tf_logo_transp.png"><br><br>
</div>

-----------------


| **`Documentation`** |
|-----------------|
| [![Documentation](https://img.shields.io/badge/api-reference-blue.svg)](https://www.tensorflow.org/api_docs/) |

**TensorFlow** is an open source software library for numerical computation using
data flow graphs.  The graph nodes represent mathematical operations, while
the graph edges represent the multidimensional data arrays (tensors) that flow
between them.  This flexible architecture enables you to deploy computation to one
or more CPUs or GPUs in a desktop, server, or mobile device without rewriting
code.  TensorFlow also includes [TensorBoard](https://www.tensorflow.org/programmers_guide/summaries_and_tensorboard), a data visualization toolkit.

TensorFlow was originally developed by researchers and engineers
working on the Google Brain team within Google's Machine Intelligence Research
organization for the purposes of conducting machine learning and deep neural
networks research.  The system is general enough to be applicable in a wide
variety of other domains, as well.

Keep up to date with release announcements and security updates by
subscribing to
[announce@tensorflow.org](https://groups.google.com/a/tensorflow.org/forum/#!forum/announce).

## Installation
*See [Installing TensorFlow](https://www.tensorflow.org/get_started/os_setup.html) for instructions on how to install our release binaries or how to build from source.*

People who are a little more adventurous can also try our nightly binaries:

**Nightly pip packages**
* We are pleased to announce that TensorFlow now offers nightly pip packages
under the [tf-nightly](https://pypi.python.org/pypi/tf-nightly) and
[tf-nightly-gpu](https://pypi.python.org/pypi/tf-nightly-gpu) project on pypi.
Simply run `pip install tf-nightly` or `pip install tf-nightly-gpu` in a clean
environment to install the nightly TensorFlow build. We support CPU and GPU
packages on Linux, Mac, and Windows.


#### *Try your first TensorFlow program*
```shell
$ python
```
```python
>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> sess.run(hello)
'Hello, TensorFlow!'
>>> a = tf.constant(10)
>>> b = tf.constant(32)
>>> sess.run(a + b)
42
>>> sess.close()
```
Learn more examples about how to do specific tasks in TensorFlow at the [tutorials page of tensorflow.org](https://www.tensorflow.org/tutorials/).

## Contribution guidelines

**If you want to contribute to TensorFlow, be sure to review the [contribution
guidelines](CONTRIBUTING.md). This project adheres to TensorFlow's
[code of conduct](CODE_OF_CONDUCT.md). By participating, you are expected to
uphold this code.**

**We use [GitHub issues](https://github.com/tensorflow/tensorflow/issues) for
tracking requests and bugs. So please see
[TensorFlow Discuss](https://groups.google.com/a/tensorflow.org/forum/#!forum/discuss) for general questions
and discussion, and please direct specific questions to [Stack Overflow](https://stackoverflow.com/questions/tagged/tensorflow).**

The TensorFlow project strives to abide by generally accepted best practices in open-source software development:

[![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/1486/badge)](https://bestpractices.coreinfrastructure.org/projects/1486)


## Continuous build status

### Official Builds

| Build Type      | Status | Artifacts |
| ---             | ---    | ---       |
| **Linux CPU**   | ![Status](https://storage.googleapis.com/tensorflow-kokoro-build-badges/ubuntu-cc.png) | [pypi](https://pypi.org/project/tf-nightly/) |
| **Linux GPU**   | ![Status](https://storage.googleapis.com/tensorflow-kokoro-build-badges/ubuntu-gpu-cc.png) | [pypi](https://pypi.org/project/tf-nightly-gpu/) |
| **Linux XLA**   | TBA | TBA |
| **MacOS**       | ![Status](https://storage.googleapis.com/tensorflow-kokoro-build-badges/macos-py2-cc.png) | [pypi](https://pypi.org/project/tf-nightly/) |
| **Windows CPU** | [![Status](https://ci.tensorflow.org/buildStatus/icon?job=tensorflow-master-win-cmake-py)](https://ci.tensorflow.org/job/tensorflow-master-win-cmake-py) | [pypi](https://pypi.org/project/tf-nightly/) |
| **Windows GPU** | [![Status](http://ci.tensorflow.org/job/tf-master-win-gpu-cmake/badge/icon)](http://ci.tensorflow.org/job/tf-master-win-gpu-cmake/) | [pypi](https://pypi.org/project/tf-nightly-gpu/) |
| **Android**     | [![Status](https://ci.tensorflow.org/buildStatus/icon?job=tensorflow-master-android)](https://ci.tensorflow.org/job/tensorflow-master-android) | [![Download](https://api.bintray.com/packages/google/tensorflow/tensorflow/images/download.svg)](https://bintray.com/google/tensorflow/tensorflow/_latestVersion) [demo APK](https://ci.tensorflow.org/view/Nightly/job/nightly-android/lastSuccessfulBuild/artifact/out/tensorflow_demo.apk), [native libs](https://ci.tensorflow.org/view/Nightly/job/nightly-android/lastSuccessfulBuild/artifact/out/native/) [build history](https://ci.tensorflow.org/view/Nightly/job/nightly-android/) |


### Community Supported Builds

| Build Type      | Status | Artifacts |
| ---             | ---    | ---       |
| **IBM s390x**       | [![Build Status](http://ibmz-ci.osuosl.org/job/TensorFlow_IBMZ_CI/badge/icon)](http://ibmz-ci.osuosl.org/job/TensorFlow_IBMZ_CI/) | TBA |
| **IBM ppc64le CPU** | [![Build Status](http://powerci.osuosl.org/job/TensorFlow_Ubuntu_16.04_CPU/badge/icon)](http://powerci.osuosl.org/job/TensorFlow_Ubuntu_16.04_CPU/) | TBA |


## For more information

* [TensorFlow Website](https://www.tensorflow.org)
* [TensorFlow White Papers](https://www.tensorflow.org/about/bib)
* [TensorFlow YouTube Channel](https://www.youtube.com/channel/UC0rqucBdTuFTjJiefW5t-IQ)
* [TensorFlow Model Zoo](https://github.com/tensorflow/models)
* [TensorFlow MOOC on Udacity](https://www.udacity.com/course/deep-learning--ud730)
* [TensorFlow Course at Stanford](https://web.stanford.edu/class/cs20si)

Learn more about the TensorFlow community at the [community page of tensorflow.org](https://www.tensorflow.org/community) for a few ways to participate.

## License

[Apache License 2.0](LICENSE)
