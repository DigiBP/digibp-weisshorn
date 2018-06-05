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
![](https://github.com/DigiBP/digibp-weisshorn/blob/master/Wiki/Process%20Model_v1-9-Health%20Insurance%20Application.jpeg?raw=true)

1.	The customer opens the google form link https://docs.google.com/forms/d/e/1FAIpQLSd4OtjgHhR-bNpov0TNpOeCzjLxJA_8aA0OUY9xv4d1wJtGcA/viewform and fills out the application form. By pressing the send button, it will be sent via Integromat (HTTP) to the digibp herokuapp with all relevant variables. 
2.	Integromat sends an email to the health insurance applicant where the email must be verified.
3.	Now Camunda executes the decision table “Assess the application”. The decision table uses different input variables from the form ( e.g. HIV, cancer, age). According to the variable there are three possible outputs:
•	Reject
•	Accept
•	Offer Alternative
The application will only be accepted if the applicant is younger than 65 years. If the applicant is over 65 years, the application will be always rejected. In some cases, it would also be possible to offer an alternative (according to variables Medicines, Treatment, Planned Treatment, Illness, Addiction, Cancer, CancerType, HIV, Disability).
4.	If the application has been accepted Integromat will create and send an offer to the applicant via email. The applicant has to confirm the offer with a google form. <br>
a.	As soon as we get the confirmation we store the decision in the google sheet. <br>
b.	The next decision checks if the customer sent the confirmation. If it has been accepted, a contract will be sent from Integromat via email to the applicant including a google form to sign the contract. If the offer has not been accepted the process would end here.<br>
c.	As soon as the contract is signed it will be stored in the google sheet and the process ends.<br>
5.	If the application has been selected for an alternative offer the back office analyzes the individual form fields. This part of the process is not digitalized and will be performed manually by the health insurance company.<br>
a.	If there are unfilled form fields the medical status will be clarified by the customer agent. When the information is available and alternative offer will be created.<br>
b.	If the application is complete an alternative offer can be created by the customer agent. <br>
c.	Integromat will create and send an offer to the applicant via email. The applicant has to confirm the offer with a google form.<br>
d.	As soon as we get the confirmation we store the decision in the google sheet. <br>
e.	The next decision checks if the customer sent the confirmation. If it has been accepted, a contract will be sent from Integromat via email to the applicant including a google form to sign the contract. If the offer has not been accepted the process would end here.<br>
f.	As soon as the contract is signed it will be stored in the google sheet and the process ends.<br>
6.	If the application is rejected Integromat will send a rejection email to the applicant and the process ends here.<br>




code to add images:
note, the image must be on the github repository
![AS-IS Process](https://github.com/DigiBP/digibp-weisshorn/blob/master/Wiki/20180602_115848.gif)


## Maintainer
- [Digitalisation of Business Processes](https://github.com/digibp)

## License

- [Apache License, Version 2.0](https://github.com/DigiBP/digibp-archetype-camunda-boot/blob/master/LICENSE)
