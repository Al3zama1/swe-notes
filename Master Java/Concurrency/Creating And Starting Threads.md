# OS Level Threads
Threads in java are managed by the underlying operating system that the JVM is running on. These threads are often referred to as OS level threads and are more heavy than is often necessary. It might require 1 to 2 MB of stack space to be allocated for each thread created.

## Project LOOM
OS level threads are too heavy, therefore project LOOK is looking to solve this by making lightweight threads that are managed by the application (JVM) instead of the operating system.

