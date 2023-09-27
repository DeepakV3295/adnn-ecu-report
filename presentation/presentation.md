# Training Neural Networks on Embedded Devices

## Introduction

Work by Prasanth and Deepak for Master's Thesis at Uppsala University
<!-- Deepak unable to present due to personal reasons -->

## Outline

### Introduction
### Embedded Linux
### Neural Networks
### Benchmark Applications
### Discussion

(_Introduction_)

## Embedded Devices

- Embedded platforms are varied: small computer boxes in trucks, smartphones, voting machines, educational platforms, and more (robots, rockets, RFID, refrigeration ...)
- application domains are varied from automotive, IoT, smart factories, etc

## Neural Network Applications on Embedded Devices

- Used in smart speakers for voice commands
- Autonomous driving (lots of money going into that)
- Skydio autonomous drones
- Medical Bots


## Goal : Neural Network Training on Scania ECU

(picture slide)

- Trucks are another example of embedded systems
- Embedded Device example is an Electronic Control Unit ECU aboard a Scania truck

## Traditional Paradigm

- Embedded devices collects data to a Database, Data collected at Databased, and used by a Server to perform neural network model training (figure)
- Neural network development and training on a resource rich environment (server)
- Inference applications on the ECU
- Training and Inference separated
- Requires utilizing bandwidth to send data

## Federated Learning

- Data privacy concerns pioneered federated learning approaches
- Models further trained on ECU, data kept on device
- Central Server performs aggregation

## Goal : Neural Network Training on Scania ECU

(one)

- anomaly and fault detection using neural networks
- A Driver could schedule a maintenance visit at the right time (change oil, replace a tire, etc.)

## Goal : Neural Network Training on Scania ECU

(two)

- Big benefit of training on device is not having to perform costly data movement
- Hint at _federated learning_ (talking soon about different neural network application system architecture paradigms)

## Goal : Neural Network Training on Scania ECU

(three)

- Scania is upgrading ECUs
- Repurposing ECUs for neural network tasks

## Goal : Neural Network Training on Scania ECU

(four)

- Reverse engineering efforts on Scania ECU
- programs that train a neural network model
- assess their training performances

## Embedded Devices : Hardware Outline

- Outline of an ARM board
- ARM (licences CPU design), silicon vendor (NXP, Texas Instruments), system maker (ACME, Variscite, Actia)


## ARM Boards : Examples

- Coming back again to Embedded Devices; ARM based boards cut across application domains, simplifies the picture (also on the Scania ECU)
- Microcontroller : simpler architecture, low cost, energy efficient | Real-time : automotive airbags, solid state devices | Application : general purpose, high performance


(_Embedded Linux_)

## Embedded Linux

(one)

- We looked at some hardware details, now let's look at the software
- Embedded Linux is a popular open source embedded operating system

## Embedded Linux

(two)

- Kernel (requirements may be application domain specific: e.g. real-time systems)
- Bootloaders (firmware, boot sequence)
- Device Trees (hardware/software interfaces)
- Toolchains (writing embedded applications on Embedded Linux)

## Build Systems

- How do we generate these software packages for a particular board?
- Build systems are _software development tools_
- Yocto Project is one among several (Buildroot, OpenWrt)
- YP is highly configurable, targets a large space, trade off is in learning curve and complexity

## Development Setup

- Several ways to use YP, our setup was (figure)
- Development Machine (application software development, compiled using an SDK, testing via QEMU emulation)
- Yocto Project Machine (build GCC, build kernel, build U-Boot, build SDK)
- Target Hardware (flash, test)

## Software Versions

- Let's consider how to source these software packages
- upstream more open source
- vendor fork less so
- system maker fork much less so (closed)
- closed sources contribute to the fragmentation

## Scania ECU to MCIMX6Q-SDB

- Could not reverse engineer the SoM software stack
- Pivoted to MCIMX6Q-SDB which has the same processor

(_Neural Networks_)

## Handwritten Digit Recognition Neural Network

- Coming back to Neural Networks; Our implementation considers the classical example of Handwritten Digit Recognition
- MNIST dataset

## Neural Network

- Input layer, Hidden layer, Output layer
- Weights, Biases
- Fully Connected
- Activation Function
- Floating point operations

## Neural Network Training

- Training is when _weights_ and _biases_ are decided
- Training Set
- Labels
- Backpropagation

## Learning Algorithm

- mini Batch Gradient Descent
- Determines how the neural network model learns
- Other algorithms possible

## Neural Network Inference

- Inference is when _weights_ and _biases_ are used for some task
- Application here is Classification
- Show an example not in the set

(_Benchmark Applications_)

## HDR-NN Implementations

- <http://neuralnetworksanddeeplearning.com>
- Programming using Neural Network Frameworks vs Without
- *C* based HDR-NN
- *C++* / *Eigen*
- *C++* / *libtorch* (PyTorch)
- *Python* / *Numpy* (had to get Python to Target)

## C based HDR-NN

- C Data structures
- Structs and Pointers
- Implements backpropagation in C
- Matter of checking if the neural network model could learn
- YP produced SDK that could compile

## C++ / Eigen based HDR-NN

- Eigen analogous to Numpy
- Matter of checking if the neural network model could learn
- YP produced SDK that could compile

## C++ / libtorch based HDR-NN

- PyTorch doesn't support the target
- Successfully completed a build using QEMU emulation based native compilation
- Could not do the same for Tensorflow

## HDR-NN configurability

- HDR-NN input and output layers fixed
- Can change the hidden layer shape

## HDR-NN configurability

- CLI interface
- Inference mode and Training mode
- Change hidden layer shape
- Change some learning algorithm parameters

## Experiment Considerations

- Experiment : Vary Hidden layer shape, measure accuracy, execution time
- Expectation 1 : Should have the same accuracy between implementations for the same shape
- Expectation 2 : C Should have the fastest time, C++ libtorch with better time, Python with the worst

## Accuracy

- Overall shape is the same
- Variation between the versions
- Discrepancy with C version (dropping accuracy)
- PyTorch seems to learn better

## Training Time

- C faster earlier with smaller shapes but C++/libtorch beats in larger shapes
- Python as expected has the worst execution times

(_Discussion_)

## Reverse Engineering Scania ECU

- Only access to testing / production C300 units with
- Able to put NXP processor into Serial Download Mode
- Extracted Bootloader binaries, did not put into Ghidra
- Extracting information from Linux APIs
- Ultimately abandoned due to time considerations

## Software Development on Embedded Devices

- Huge variety in hardware and software
- Less visibility into the details compared to other platforms
- Harder to test across the platforms
- Ongoing research into best practises
- C vs Python for neural network application development
- Python has libraries that are harder to port

## Future Work

- Reverse Engineering Scania ECU
- Performance Engineering of C
- Add more targets
- Add more implementations
