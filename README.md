# SampleRecorder - A Cassette-based continous sample collection and acuisition tool

Welcome to the openUC2 Sample Recorder Hackathon! Our goal in this hackathon is to address the critical need for an open-source device that can continuously collect various types of microscopic samples. To achieve this, we aim to repurpose old audio cassettes and integrate them into our microscopes.

We already have a functional prototype that serves as a starting point for this project. However, we need to extend it with a UV curing assembly. This assembly will first apply UV nail polish to the cassette, which will then be cured using UV LEDs. The reason for using UV nail polish is that it is sticky enough to collect particles from the air, yet flexible enough to be rolled up once it has dried.

Our primary objective is to design the device in such a way that it can be easily attached to a bike. This will allow us to capture airborne microparticles as the bike is ridden through different environments. To facilitate this, we plan to incorporate GPS technology to track the location of particle collection. Additionally, we may explore integrating weather services to gather data on weather conditions during sampling.

This documentation serves as an overview of the continuous sample recorder project. It covers the motivation behind the project, outlines our specific goals, and provides background information on the existing prototype. By developing an open-source device that can continuously collect microscopic samples, we aim to contribute to scientific research and environmental monitoring efforts.

For more detailed information, including instructions, schematics, and code implementation, please refer to our project's GitHub repository. We encourage collaboration and welcome contributions from the community. Together, we can create an innovative solution that addresses the need for continuous sample collection and empowers researchers worldwide.


## Motivation

The motivation behind the continuous sample recorder project is to address the widespread presence of microplastics in various environments such as mountains, oceans, and even the air. Despite their prevalence, the sources and factors influencing microplastic concentrations remain unclear. In order to tackle this issue, it is important to analyze the air we breathe and understand the distribution and composition of microparticles. The project emphasizes the importance of community involvement to collectively contribute towards monitoring and studying microparticles. Furthermore, the project aims to leverage the abundance of audio cassettes for recycling purposes.

## Goal

The primary goal of the continuous sample recorder project is to develop a cassette-derived device capable of collecting airborne particles. The project draws inspiration from the Bike Particle Accelerator, a similar concept that focuses particles onto a slit before collection. The device will be designed to be mounted on a bicycle and will utilize a continuous airtrap with a sticky tape recorder. The tape will serve as a medium for collecting microparticles, which can later be analyzed using various techniques such as microscopy and spectroscopy.

To achieve the goals of the project, the following steps will be undertaken:

1. Develop a cassette-derived device: The device will be designed and constructed using a combination of cassette components and additional custom components necessary for particle collection and tracking.

2. Incorporate a particle focusing mechanism: Inspired by the Bike Particle Accelerator, the device will include a mechanism to focus particles onto a slit before they are collected. This will ensure efficient particle capture.

3. Track location and weather data: The device will integrate GPS coordinates to track the location of particle collection. Additionally, weather services may be incorporated to gather data related to weather conditions during sampling.

4. Implement a sticky tape recorder: The device will utilize a continuous tape recorder with a sticky surface to collect microparticles. A potential method for achieving stickiness is using UV-curable nail polish, which provides flexibility, stickiness, and transparency when dry.

5. Build a functional prototype: The project aims to build a functional demonstrator prototype that showcases the capabilities of the continuous sample recorder. This prototype can be used to validate the concept and gather feedback for further improvements.

## Background

The continuous sample recorder project is built upon an existing prototype that resembles an ESP32 controlling the 28byj-48 motor with the ULN2003 driver. This prototype serves as the foundation for the development of the cassette-derived device. Additionally, future plans involve integrating the device with a UC2 microscope or other standards such as wellplate formats to enhance its versatility and compatibility with different analysis techniques.

By leveraging the existing prototype and building upon it, the continuous sample recorder project aims to create a practical solution for monitoring and analyzing airborne microparticles. The project encourages collaboration and welcomes contributions from the community to collectively address the issue of microplastic pollution and its impact on the environment.

Please refer to the project's GitHub repository for more detailed information, including instructions, schematics, and code implementation. Feel free to contribute, provide feedback, and join the community effort to build a better understanding of microparticles and their distribution. Together, we can make a positive impact on environmental research and conservation.

## Current State: Building the Prototype



Transparent cassette from Thoman
![](./IMAGES/IMG_20230131_215132.jpg)

Current prototype based on an ESP32 with a 28byj stepper motor and a GPS module
![](./IMAGES/IMG_20230703_084535.jpg)

The tape can be "played" in one directon only
![](./IMAGES/IMG_20230703_084540.jpg)


## Current Results

### CAD

The Inventor DEsign Files can be found in the folder [INVENTOR](./INVENTOR)
The STL printing files can be found in the folder [STL](./STL)

### Images and Results

We have made significant progress in the development of the continuous sample recorder. Here are some of the current results we have achieved:

1. Transparent Tape Observation: We have observed transparent tape under a microscope, specifically using Thoman microscopy. This visualization helps us understand the characteristics of the tape and how particles may interact with it.

   ![Transparent Tape under a microscope](./IMAGES/2023-02-01-075829111.gif)

2. Particle Capture on Microscopy Slide: We have successfully captured particles trapped on a microscopy slide using the sample recorder. This demonstrates the device's ability to collect microscopic samples for further analysis.

   ![Capturing particles trapped on a microscopy slide](./IMAGES/2023-02-06-093656930.gif)

3. Microplastic Capture Attempt: We have also experimented with capturing microplastics using a cross-polarization microscopy scheme. This method helps in distinguishing microplastics from other particles based on their polarized light properties.

   ![Trying to capture microplastic using a cross-polarization microscopy scheme](./IMAGES/2023-02-06-094908047.gif)

4. UC2-Based Setup Example: We have an example setup based on UC2, where the cassette can be adjusted along one direction. However, the illumination and curing mechanisms are still missing in this setup.

   ![Example UC2-based setup](./IMAGES/VID_20230206_170533.gif)

### Setting up and Adapting

To set up and adapt the continuous sample recorder, follow these steps:

#### ESP32

1. Use the UC2-ESP32 repository available at: [https://github.com/youseetoo/uc2-esp32/](https://github.com/youseetoo/uc2-esp32/).

2. Modify the `UC2_CassetteRecorder` configuration in the `PinConfig.h` file. Set the configuration in the `static UC2_CassetteRecorder pinConfig;` line. You can define the appropriate pin configuration for your setup here.

3. Compile the code using platform iO in Visual studio code and upload it to the ESP32.

4. Connect the ULN2003 motor driver to the following pins on the ESP32:
   - ROTATOR_X_0: GPIO_NUM_13
   - ROTATOR_X_1: GPIO_NUM_14
   - ROTATOR_X_2: GPIO_NUM_12
   - ROTATOR_X_3: GPIO_NUM_27

#### Python

1. You can control the "rotator" using serial commands in Python. The following JSON command can be used to move the motor:
   ```json
   {
       "task": "/rotator_act",
       "motor": {
           "steppers": [
               {
                   "stepperid": 2,
                   "position": 10000,
                   "speed": 500,
                   "isabs": 0,
                   "isaccel": 0
               }
           ]
       }
   }
   ```
   This command adjusts the position of the motor.

2. You can also utilize the UC2-REST repository to control the rotator interface in Python. Here is an example script: [https://github.com/openUC2/UC2-REST/blob/master/uc2rest/TEST/TEST_ESP32_Serial.py#L23](https://github.com/openUC2/UC2-REST/blob/master/uc2rest/TEST/TEST_ESP32_Serial.py#L23). Additionally, the `rotator.py` file in the UC2-REST repository provides further functionality for controlling the rotator.

Please refer to the respective repositories for more detailed instructions and implementation details. Feel free to explore and adapt the continuous sample recorder to suit your specific requirements.

## Safety

Stay safe

## Challenge: Enhancements for the Continuous Sample Recorder

The continuous sample recorder project faces several challenges that need to be addressed for improved functionality and usability. Here are the main challenges along with proposed enhancements:

1. Particle Trapping on the Record: To improve the efficiency of particle trapping, consider optimizing the design of the trapping mechanism. Explore options such as incorporating a slit or mesh that can effectively capture particles while minimizing the risk of particles escaping during sample collection.

2. Automated Tape Unrolling and Rolling: Develop a motorized system that automates the tape unrolling and rolling process. This mechanism should precisely control the movement of the tape, ensuring consistent and reliable operation.

3. Timestamp Correlation with GPS Data: Integrate the GY-GPS6MV2 GPS Module to accurately track the location of particle collection. This module provides reliable GPS data that can be correlated with the timestamps of sample collection. Ensure proper synchronization between the GPS module and the device's internal clock to maintain accurate timing.

4. Automated Microscope Capture: Implement an automated system that captures the entire tape using a microscope. This can be achieved by developing a motorized stage or a tape transport mechanism that moves the tape systematically under the microscope. This automation simplifies the capturing process and ensures comprehensive analysis of the entire sample.

5. Automated Nail Polish Dispensing and Curing: Enhance the process of applying and curing the UV nail polish on the tape. Develop an automated mechanism that dispenses the nail polish uniformly onto the tape surface. Integrate UV LED modules that can be controlled to provide consistent and precise curing of the nail polish, ensuring optimal stickiness for effective particle collection.

6. Contrast Methods: Determine the most suitable contrast method for your specific requirements. Consider the advantages and limitations of different techniques such as brightfield, darkfield, and cross-polarization microscopy. Brightfield microscopy provides good overall visualization, while darkfield microscopy enhances the visibility of transparent particles. Cross-polarization microscopy helps in distinguishing polarized particles such as microplastics. Choose the contrast method that best suits your sample characteristics and objectives.

By addressing these challenges and implementing the proposed enhancements, the continuous sample recorder will become a more efficient and reliable device for collecting microscopic samples.

## Ressources


## License
