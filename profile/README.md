# The Mission AIpossible demo (with Artifical Intelligence and Edge Computing)

![](/profile/avatar.png)

## Abstract

Message to Agent Red Hat:

> The LEGO train is running without a driver!
> Your mission: develop and deploy an AI on board the train to stop it before it derails.
> This message will self-destruct in five seconds. Four… Three… Two… One…

🎵 tum tum tada tum tum tada tum tum tada tum tum tada tiduduuummm tiduduuummm 🎵

Full abstract [here](https://docs.google.com/document/d/135Y6yAEaJZleIXPm74G5dfwyMH8KfNT6hi4YLT4tCkw/edit).

## Demo

[![Watch the video](https://img.youtube.com/vi/RhbbA3oTgdM/maxresdefault.jpg)](https://youtu.be/RhbbA3oTgdM)

## Software components

| Component | Description | Git Repository | Container Image |
| --- | --- | --- | --- |
| **train-controller** | Receives commands through MQTT and acts on the Lego Hub accordingly. | [Demo-AI-Edge-Crazy-Train/train-controller](https://github.com/Demo-AI-Edge-Crazy-Train/train-controller) | [quay.io/demo-ai-edge-crazy-train/train-controller](https://quay.io/repository/demo-ai-edge-crazy-train/train-controller) |
| **intelligent-train** | Receives images through MQTT, process them with an AI model and sends the results back to MQTT | [Demo-AI-Edge-Crazy-Train/intelligent-train](https://github.com/Demo-AI-Edge-Crazy-Train/intelligent-train) | [quay.io/demo-ai-edge-crazy-train/intelligent-train](https://quay.io/repository/demo-ai-edge-crazy-train/intelligent-train) |
| **train-ceq-app** | Manages messages between the train-controller, intelligent-train, capture-app, MQTT and Kafka. | [Demo-AI-Edge-Crazy-Train/train-ceq-app](https://github.com/Demo-AI-Edge-Crazy-Train/train-ceq-app) | [quay.io/demo-ai-edge-crazy-train/train-ceq-app](https://quay.io/repository/demo-ai-edge-crazy-train/train-ceq-app) |
| **train-monitoring-app** | Displays images streamed through Kafka. | [Demo-AI-Edge-Crazy-Train/train-monitoring-app](https://github.com/Demo-AI-Edge-Crazy-Train/train-monitoring-app) | [quay.io/demo-ai-edge-crazy-train/train-monitoring-app](https://quay.io/repository/demo-ai-edge-crazy-train/train-monitoring-app) |
| **train-capture-image-app** | Captures and compresses images from the webcam. Sends them over MQTT. | [Demo-AI-Edge-Crazy-Train/train-capture-image-app](https://github.com/Demo-AI-Edge-Crazy-Train/train-capture-image-app) | [quay.io/demo-ai-edge-crazy-train/train-capture-image-app](https://quay.io/repository/demo-ai-edge-crazy-train/train-capture-image-app) |

## Bill of Materials

| Component                                                                                                            | Reference                                                       | Price    |
|----------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|----------|
| [Lego Express Passenger Train](https://www.lego.com/en-fr/product/express-passenger-train-60337)                     | #60337                                                          | 159,99 € |
| [NVIDIA JETSON ORIN NANO 8GB DEVELOPMENT KIT](https://www.siliconhighwaydirect.com/product-p/945-13766-0005-000.htm) | 945-13766-0005-000                                              | 469,06 € |
| USB Webcam with UVC support and fixed focus                                                                          | Logitech C505 HD                                                | 20,00 €  |
| [Traffic signs](https://www.amazon.fr/dp/B00I65IH3I)                                                                 | Siku 5597                                                       | 11,04 €  |
| [LR03 / AAA battery pack](https://www.amazon.fr/dp/B003A6FA60)                                                       | Varta Long Life Power                                           | 8,66 €   |
| [USB-C Power Bank with PD support](https://sharge.com/products/storm2-slim)                                          | Shargeek 130                                                    | 185,35 € |
| [USB-C Portable Display](https://www.lenovo.com/us/en/p/accessories-and-software/monitors/office/61dduar6us)         | Lenovo ThinkVision M14                                          | 229,01 € |
| [USB-C to DisplayPort adapter](https://www.amazon.fr/gp/product/B081VK7Q94/)                                         | Amazon Basics Bi-Directional USB-C to DisplayPort Cable         | 11,63 €  |
| [USB-C PD Trigger, 9-19V, 5.5/2.5 barrel jack](https://www.amazon.fr/gp/product/B0B9FTJHGV/)                         | DSD TECH MagicConn SH-CP15A USB Type C PD to DC Power Cable-15V | 12,99 €  |
| [USB Keyboard](https://www.amazon.fr/gp/product/B082VYZ694/)                                                         | Rii Mini Keyboard K01X1                                         | 19,99 €  |
| [NVMe M.2 2280 SSD](https://www.amazon.fr/dp/B0C2WGL8DQ)                                                             | Crucial P3 1To M.2 PCIe Gen3                                    | 65,99 €  |

Total budget to forecast: **1 193,71 €**.

If you want to replace the green bricks by red ones and make the train a bit more professional, you can spend another 25,99 € on [LEGO Pick a Brick](https://www.lego.com/pick-and-build/pick-a-brick). See the additional [Bill of Materials](pick-a-brick-order.csv).

## Administration

- [rhde-nvidia-jetson-orin](https://github.com/Demo-AI-Edge-Crazy-Train/rhde-nvidia-jetson-orin): RHEL for Edge images for the Jetson Orin Nano
- [gitops](https://github.com/Demo-AI-Edge-Crazy-Train/gitops): OpenShift GitOps manifests

## Base container images

- [openjdk-opencv](https://quay.io/repository/demo-ai-edge-crazy-train/openjdk-opencv): OpenJDK + OpenCV base image for ARM64 and x86_64
- [nvcr.io/nvidia/l4t-jetpack](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/l4t-jetpack): NVidia Base image to leverage GPU acceleration on the Jetson Orin Nano
- [base-developer-image](https://quay.io/repository/demo-ai-edge-crazy-train/base-developer-image): Base Developer Image with OpenCV included
- [universal-developer-image](https://quay.io/repository/demo-ai-edge-crazy-train/universal-developer-image): Universal Developer Image with OpenCV included

## Dependencies

### Bluetooth

- [node-ble](https://github.com/Demo-AI-Edge-Crazy-Train/node-ble): NodeJS library to use the BlueZ DBUS API under Linux
- [noble](https://github.com/Demo-AI-Edge-Crazy-Train/noble): NodeJS library that provides a cross-platform abstraction to communicate over Bluetooth Low Energy (BLE)
- [node-poweredup](https://github.com/Demo-AI-Edge-Crazy-Train/node-poweredup): NodeJS library that communicates with Lego hubs over Bluetooth Low Energy (BLE)

### OpenCV

- [cekit-images](https://github.com/Demo-AI-Edge-Crazy-Train/cekit-images): Cekit manifests to build OpenJDK images with OpenCV included
- [devspaces-developer-images](https://github.com/Demo-AI-Edge-Crazy-Train/devspaces-developer-images): Universal Developer Image for OpenShift DevSpaces, with OpenCV included

## Live Events

This demo has been showcased at the following events:

- [OpenShift AI Roadshow 2024](https://www.itix.fr/fr/speaking/openshift-ai-roadshow-2024/) 🇫🇷
- [Platform Day 2024](https://www.itix.fr/fr/speaking/platform-day-2024/) 🇫🇷
- [Worldline Tech Forum eXplore France 2024](https://www.itix.fr/fr/speaking/worldline-tech-forum-explore-france-2024/) 🇫🇷
- [Riviera Dev 2024](https://www.itix.fr/fr/speaking/riviera-dev-2024/) 🇫🇷
- [Red Hat Summit Connect France 2024](https://www.itix.fr/speaking/red-hat-summit-connect-france-2024/) 🇬🇧
- [Red Hat Open Demo: Mission impossible #1 - Stop the crazy Train with AI and Edge before it is too late!](https://www.itix.fr/speaking/red-hat-open-demo-mission-impossible-stop-the-crazy-train-with-ai-and-edge-before-it-is-too-late/) 🇬🇧

## Watch the demo!

[![Red Hat Open Demo - Mission impossible #1 - Stop the crazy Train with AI and Edge before it is too late!](http://img.youtube.com/vi/8BTLBF0eQqc/0.jpg)](http://www.youtube.com/watch?v=8BTLBF0eQqc "Red Hat Open Demo: Mission impossible #1 - Stop the crazy Train with AI and Edge before it is too late!")

