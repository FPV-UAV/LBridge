# LBridge
LBridge - Read the Freestyle Libre sensor and send the BG readings to xDrip+ using the xBridge2 protocol

This project is is a modification/extension of the LimiTTer projekt from JoernL. The code is running on the LimiTTer hardware platform which is described in the LimiTTer project. It replaces the LimiTTer code and provide the same functionalities.

LBridge uses the xBridge2 protocol from the Wixel project / implementation of savek-cc. It improves the original LimiTTer in terms of

  - optimized battery usage
  - no missed BG readings
  - better BLE performance

LBridge is working with the great App xDrip+. You can find it here:

https://jamorham.github.io/#xdrip-plus

Click on "Download latest APK" or choose the "Nightly Snapshots" for the very latest ones.

Please note, that LBridge code for LimiTTer is NOT maintained by Abbott. It is an experimental DIY project. You will built your own individual LimiTTer. So you are responsible yourself for what you have built. This is not a medical device. Dont make any medical decisions based on the results as they can be wrong!

Files:

LBridge_RFduino_V09, 4.2.2018:
  - general code cleanup
  - full 8h backfilling (get missed readings from the Libre Sensor like LibreAlarm after missing sensor)
  - changed dead sensor detection
  - shadow FRAM mechanism from @UPetersen
  - switch off serial interface due ULP sleep phase for better power consumption, @Chaosbiber
  - xbridge2 queue extended to 12 h (store BG readings which cannot be transmitted to xDrip+, bulk tranfer after reconnect)
  - cycle time of 1 min after system start to get faster the inital 4 readings (@FPV-UAV)
  
  *** code was tested only with a dead sensor, be careful using it ***

LBridge_Arduino_170716_1950.ino: release candidate, please use the latest Arduino IDE to compile
  - improved BLE connectivity. This can cost more battery power under bad BLE conditions
  - default name set to "LimiTTer" to avoid hardware source changing to xbridge wixel in xDrip+ 
  - added detection of sensor lifetime. Automatic stop after 20880 operation (=14,5 days) or 5 identical glucose readings
  - added spike filter (set to +- 40 mg/dL)
  - added sensor lifetime display in xDrip+ (works on phone, not on SSW3)
  - NFC read code modified to avoid possible sensordeaths due to massive re-read tries of BM019
  - autocalibrate PWR DWN timer to get accurate 5 min spacing
  - increased queue depth for BG readings to 5h
  - bugfix for detecting dead sensors before end of lifetime
  
LBridge_RFduino_170729_1647.ino:
  - added Spike (> +-40) detection and removal for loop usage
  - added sensor shutdown detection. No new readings after 20880 min usage or 5 consequtive identical readings

Old files:

LBridge_RFduino_0627_1750.ino: work in progress
  - Lbridge code for RFduino or Simblee platform. Alpha release. Can be compiled for RFduino or Simblee platform. 
  - voltage range adjusted to display more correct percentage of remaining battery. Choose LimiTTer device in xDrip+ as hardware source.   - queue depth for 8 h of BG readings
  - stable operation of BM019 (special thanks to @bertrooode)
  - devider of raw BG readings by 8.5 
  - open issues: 
    - Operation together with SSW3
    - power savings for NFC.

Lbridge_R_170510_3.ino: 
  - tested with HM-11 (V547) and HM-17 (V117) 
  - improved timings to reduce battery consumption
  - fast handover between Wear Collection Service on Sony Smart Watch 3 and xDrip+.

LBridgev_PR_170311.ino: 
  - Improved HM-11 handling. I used this version the last 2 months without problems in my live system. Stable and reliable. 
  - provided in gitter discussion group as version 0316. Please refer to the chat protocols to get more details.

Lbridgev_PR_170302.ino: 
  - inital version provided in the LimiTTer gitter discussion group in march. Please refer to the chat protocols to get details on them.

