# Training Neural Networks on Embedded Devices

## Introduction

Work by Prasanth and Deepak for Master's Thesis at Uppsala University
<!--> Deepak unable to present due to personal reasons </!-->

## Outline

### Neural Networks in Embedded Devices
### Embedded Linux
### Neural Networks
### Benchmark Applications
### Discussion

(begin _Neural Networks in Embedded Devices_)

## Neural Network Applications on Embedded Devices

- Used in smart speakers for voice to activate features, "Ok, Google"
- Autonomous driving (lot of money going into that)
- Skydio autonomous drones

## Embedded Devices

- Embedded platforms more varied than these : small computer boxes in trucks, smartphones, voting machines, educational units, robots, so many more
- Also present in simpler devices such as IoT lights, smart appliances, etc.

## Goal : Neural Network training on Scania C300

- anomaly detection applications
- hint at federated learning (we shall soon talk about the different paradigms for neural network application lifecycle)

## ARM Boards : Examples

- ARM: Energy-efficient processors for diverse devices
- Application : general purpose, high performance, smartphone | Real-time : automotive airbags, solid state devices | Microcontroller : simpler architecture, low cost, energy efficient

## ARM Boards : Outline

- ARM board internals
- ARM, silicon vendor (NXP), system maker (ACME, Variscite)
- internal communication protocols, external interfaces, serial communication buses

(begin _Embedded Linux_)

## Embedded Linux

- Embedded Linux is a popular open source embedded operating system based on the popular operating system Linux
- Let's consider what are the different pieces of software that are required for embedded platforms

## Build Systems

- Software development tool

## The Yocto Project

- Pretty Complicated

## Yocto Project : Development

- Development Machine, Yocto Project Machine, Target Hardware

## Software Versions

- Let's consider how to source these software packages
- upstream more open source

## Scania C300 to MCIMX6Q-SDB

- could not reverse engineer the SoM software stack
- pivoted to MCIMX6Q-SDB which has the same processor

(begin _Neural Networks_)

## Handwritten Digit Recognition Neural Network

- MNIST

## Neural Network Training

- Training Set

## Learning Algorithm

- mini Batch Gradient Descent
- other algorithms possible

## Neural Network Inference

- Show an example not in the set

## Traditional Paradigm

- Utilize bandwidth to send data

## Federated Learning

- Data privacy

(begin _Benchmark Applications_)

## C Based HDR-NN

- Find the code on GitHub

## HDR-NN configurability

- Can change the hidden layer shape

## HDR-NN configurability

- Accepts command line arguments

## Accuracy

- Talk about accuracy plot

## Training Time

- Talk about training time curves
- PyTorch unexpectedly faster

(begin _Discussion_)

## Development Journey

## Software Development on Embedded Devices

## Future Work
