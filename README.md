# BlueNRG-LP-HSE-CALIB-RTT
 
* The BlueNRG-LP-HSE-CALIB-RTT is an application example that allows the user to tune the High Speed External (HSE) crystal by adjusting 2 internal capacitors via J-Link RTT.
    * This application may be used to find the optimal HSE tune value for your PCB. This value can then be set with the CONFIG_HW_HSE_TUNE preprocessor symbol on your BlueNRG projects.
* The RF frequency is dependent on the HSE. Tuning of the HSE can be done by measuring the HSE clock or RF frequency.
* The HSE clock is output on the Microcontroller Clock Output (MCO) pin: PA11.
    * Use a frequency counter to measure the HSE frequency on the MCO pin.
* An RF tone at 2.402 GHz is started automatically at application start and after each change made to the HSE tune value.
    * A spectrum analyzer can be used to measure the tone peak, follow section 5.5 in [AN5503](https://www.st.com/resource/en/application_note/an5503-bringing-up-the-bluenrglp-bluenrglps-devices-stmicroelectronics.pdf) to configure the analyzer.
* This application example is based on the RCC_HSE_Calib application for the STM32WB55 found in the [X-CUBE-CLKTRIM](https://www.st.com/en/embedded-software/x-cube-clktrim.html) expansion package.

## Hardware Needed

* One [STEVAL-IDB011V2](https://www.st.com/en/evaluation-tools/steval-idb011v2.html) (BlueNRG-LP)

* One SEGGER [J-Link / J-Trace Debug Probe](https://www.segger.com/products/debug-trace-probes/)

* One Frequency Counter (Necessary for HSE Frequency Measurment)

* One Spectrum Analyzer (Necessary for RF Frequency Measurment)

## Software Needed

* Prebuilt firmware image: [BlueNRG-LP-HSE-CALIB-RTT.hex](/Binaries)

* [WISE Studio](https://www.st.com/en/embedded-software/stsw-wise-studio.html), [IAR EWARM](https://www.iar.com/products/architectures/arm/iar-embedded-workbench-for-arm/), or [Keil MDK-ARM](https://developer.arm.com/Tools%20and%20Software/Keil%20MDK) IDE

* [J-Link Software Pack](https://www.segger.com/downloads/jlink/)

## User Guide

1) Connect the J-Link Debug Probe to the EVAL board.

    ![RM_IMAGE_0](Utilities/Media/RM_IMAGE_0.png)

2) Flash the application firmware on to the board using one of the following options:

    a) Use [J-Flash LITE](https://www.segger.com/products/debug-probes/j-link/technology/flash-download/#:~:text=statistics%20upon%20success.-,J%2DFlash%20LITE,-J%2DFlash%20Lite) included with the [J-Link Software Pack](https://www.segger.com/downloads/jlink/) to download the hex file on to the board.

    ![RM_IMAGE_1](Utilities/Media/RM_IMAGE_1.png)

    b) Open your preferred IDE and build & run the project to download it on to the board.

    ![RM_IMAGE_2](Utilities/Media/RM_IMAGE_2.png)

3) Connect to one of the following devices to measure the HSE or RF frequency:

    a) HSE: Connect the MCO pin (PA11) and the GND pin to a frequency counter.

    ![RM_IMAGE_3](Utilities/Media/RM_IMAGE_3.png)

    b) RF: Connect the board to a spectrum analyzer directly with an SMA cable or wirelessly with RF antennas.

    > **Note:** The antennas should be placed closely together. Follow section 5.5 in [AN5503](https://www.st.com/resource/en/application_note/an5503-bringing-up-the-bluenrglp-bluenrglps-devices-stmicroelectronics.pdf) to configure the analyzer.

    ![RM_IMAGE_4](Utilities/Media/RM_IMAGE_4.png)

4) Open RTT Viewer from the [J-Link Software Pack](https://www.segger.com/downloads/jlink/) and connect to the EVAL board.

    ![RM_IMAGE_5](Utilities/Media/RM_IMAGE_5.png)

5) Once the application example has started, you will see an initial message.

    > **Note:** You may need to press the RESET button to start the application example.

    ![RM_IMAGE_6](Utilities/Media/RM_IMAGE_6.png)

6) Send '1' or '2' via J-Link RTT to change the HSE tune value (0 - 63).

    a) '1': increases the HSE tune value.

    ![RM_IMAGE_7](Utilities/Media/RM_IMAGE_7.png)

    b) '2': decreases the HSE tune value.

    ![RM_IMAGE_8](Utilities/Media/RM_IMAGE_8.png)

7) Tune the HSE until you see the following HSE or RF frequency frequency measurments.

    a) HSE Frequency: 32 MHz

    b) RF Frequency: 2.402 GHz

8) Take note of the optimal HSE tune value and set it using the CONFIG_HW_HSE_TUNE preprocessor symbol on your BlueNRG projects.

    > **Note:** The default CONFIG_HW_HSE_TUNE value is set to 32 for BlueNRG examples.

    ![RM_IMAGE_9](Utilities/Media/RM_IMAGE_9.png)

## Troubleshooting

**Caution** : Issues and the pull-requests are **not supported** to submit problems or suggestions related to the software delivered in this repository. The BlueNRG-LP-HSE-CALIB-RTT example is being delivered as-is, and not necessarily supported by ST.

**For any other question** related to the product, the hardware performance or characteristics, the tools, the environment, you can submit it to the **ST Community** on the STM32 MCUs related [page](https://community.st.com/s/topic/0TO0X000000BSqSWAW/stm32-mcus).