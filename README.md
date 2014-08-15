python_cpp_interop
==================

This project gives a simple calling C++ code from Python.
The basic idea is to use ctypes module in Python to call an library with plain 'c' interface,
using Google Protocol Buffers to exchange complex data structures.

Steps to run this example
=========================

1. Download and unpack https://protobuf.googlecode.com/files/protobuf-2.5.0.tar.gz

2. Download and unpack protoc.exe from https://protobuf.googlecode.com/files/protoc-2.5.0-win32.zip

3. Follow instructions in protobuf-2.5.0\python\README.txt to build and install python on windows.

   Basically you should run three steps:

      python setup.py build
      
      python setup.py install
      
      python setup.py test

    Note that protoc.exe has to be placed under protobuf-2.5.0\python, because it is used by setup.py script.

4. Run the 'use_library.py' script

      python use_library.py

   This script uses native_library.dll to calculate square root of some numbers.
   Google protocol buffers are used to pass the numbers into the library.


Steps to recompile 'native_library.dll' on Windows
==================================================

Use Visual Studio 2012 to compile native_library/native_library.sln.
This will produce native_library.dll. Replace this file in the root of this
distributive so that it gets picked up by use_library.py script.

If you use different version of Visual Studio, then you have to recompile projects 
under protobuf-2.5.0\vsprojects\ to produce appropriate static library
(libprotobuf.lib).


Steps to recompile 'messages.proto' on Windows
==============================================

1. Download and unpack https://protobuf.googlecode.com/files/protoc-2.5.0-win32.zip
2. protoc.exe --cpp_out=native_library --python_out=. messages.proto

The resulting files are 
	native_library/messages.pb.h, 
	native_library/messages.pb.cc,
	python_library/messages_pb2.py.
