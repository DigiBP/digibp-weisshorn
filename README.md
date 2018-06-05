# DigiBP Group Weisshorm - Health Insurance Application

[![License](http://img.shields.io/:license-apache-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)
[![Deploy to Heroku](https://img.shields.io/badge/deploy%20to-Heroku-6762a6.svg?longCache=true)](https://heroku.com/deploy)

This README is used to document the project about the digitalization of a health insurance application process. 

To have a picture of the current situation, a high level AS-IS process is created with BPMN 2.0. Together with the decision table, this AS-IS process is allready executable but requires a lot of human interaction. To reduce human tasks, the process is then digitalized and every step of digitalization is documented (TO-BE Digitalized).

## AS-IS Highlevel Process
![](https://github.com/DigiBP/digibp-weisshorn/blob/master/Wiki/Process%20Model%20AS%20IS.jpeg)

This process starts when the customer sends the health insurance application by email or post. At the moment our health insurance company is only able to handle physical applications. After we received the application the customer agent checks by himself if it is complete. If the application is not complete furhter information must be requested, nomally via phone or email. When the application is complete the customer agent assesses every application based on the decision table. There are three input variables which are used to calculate the decision:

*Category

*Illness

*Risk

There are three possibilities after the assessment of the application is finished.

![](https://github.com/DigiBP/digibp-weisshorn/blob/master/Wiki/Decision%20Table%20AS%20IS.png?raw=true)

If there is no possibility for a contract with the customer, the customer gets informed about the rejected request. Different possibilities to inform the customer upon the rejected request are possible. The customer may be informed by e-mail, letter or other media. The process will end with the information which is sent to the customer.
The contract will be prepared if the assessment of the application was successful. This should be the most frequent path after the assessment. It is a critical success factor to keep the cases in the other two paths on a low level. The contract will be sent to the customer for verification and signing afterwards. Again there are different ways how this contract could be sent to the customer and signed by the customer. This could be traditional with a hard copy but could also be in an electronic format. The process will end with a signed contract.
It may be possible that an alternative contract version is required compared to the one which was initially requested by the customer. The alternative can be offered to the customer prior to the contract preparation. After that step the contract will be sent to the customer for signature as described above. The process again ends with a signed contract.

## TO-BE Digitalized Process
code to add images:
note, the image must be on the github repository
![AS-IS Process](https://github.com/DigiBP/digibp-weisshorn/blob/master/Wiki/20180602_115848.gif)


## Maintainer
- [Digitalisation of Business Processes](https://github.com/digibp)

## License

- [Apache License, Version 2.0](https://github.com/DigiBP/digibp-archetype-camunda-boot/blob/master/LICENSE)
