# DigiBP Group Weisshorn - Health Insurance Application

[![License](http://img.shields.io/:license-apache-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)
[![Deploy to Heroku](https://img.shields.io/badge/deploy%20to-Heroku-6762a6.svg?longCache=true)](https://heroku.com/deploy)

This README is used to document the project about the digitalization of a health insurance application process. 

To have a picture of the current situation, a high level AS-IS process is created with BPMN 2.0. Together with the decision table, this AS-IS process is allready executable but requires a lot of human interaction. To reduce human tasks, the process is then digitalized and every step of digitalization is documented (TO-BE Digitalized).

## AS-IS Highlevel Process
![](https://github.com/DigiBP/digibp-weisshorn/blob/master/Wiki/Process%20Model_v1-6-Health%20Insurance%20Application.jpeg?raw=true)

1.	The customer sends us a physical application form via post office. The customer agents check the application for completeness. If the form is not complete additional information will be requested. Otherwise the application will be assessed by back office.
2.	Now the back office executes the decision table “Assess the application” manually. The decision table uses different input variables from the form ( e.g. HIV, cancer, age). According to the variable there are three possible outputs: <br>
•	Reject <br>
•	Accept <br>
•	Offer Alternative <br>
The application will only be accepted if the applicant is younger than 65 years. If the applicant is over 65 years, the application will be always rejected. In some cases, it would also be possible to offer an alternative (according to variables Medicines, Treatment, Planned Treatment, Illness, Addiction, Cancer, CancerType, HIV, Disability).
3.	If the application has been accepted the back office creates an offer. <br>
a.	The offer is sent to the applicant by the customer agent. <br>
b.	As soon as we receive the decision from the applicant, the customer and the decision is added to the Customer Database (MS Access). <br>
c.	If the customer rejects the offer the process will end. <br>
d.	If the customer accepts the offer the back office prepares the contract. <br>
e.	The contract is sent by customer agent <br>
f.	Wait until the contract is signed and store contract information in Customer Database (MS Acess). If after 13 days no answer from  the customer is available the process ends. <br>
4.	If the application has been selected for an alternative offer the back office analyzes the individual form fields. <br>
a.	If there are unfilled form fields the medical status will be clarified by the customer agent. When the information is available and alternative offer will be created. <br>
b.	If the application is complete an alternative offer can be created by the back office. <br>
c.	The offer is sent to the applicant by the customer agent. <br> 
d.	As soon as we receive the decision from the applicant, the customer and the decision is added to the Customer Database (MS Access). <br>
e.	If the customer rejects the offer the process will end. <br>
f.	If the customer accepts the offer the back office prepares the contract. <br>
g.	The contract is sent by customer agent <br> 
h.	Wait until the contract is signed and store contract information in Customer Database (MS Access). If after 13 days no answer from  the customer is available the process ends. <br>
5.	If the application is rejected the customer agent will send a rejection letter to the applicant and the process ends here.

## Decision Table
The decision table "Assess The Application" uses the process variables createt either manually (AS-IS process) or automatically by the submitted Application Form (To-Be process). There is no modification needed to prepare the decision table for the automated process. 
<br>
By submitting the application form, the applicant submittes 13 variables. Following approach helped to keep the table as small as possible:
<br>

• identify easiest solutions: 13 time "No" = "Accept", Age >= 65 = "Reject".<br>
• identify solutions with the least combination possibilities: If the five variables "Repudiation",	"Cancellation",	"Unable to Work",	"Cancer" or	"HIV" consists a "No" the application is rejected. Consequently, the other eight variables build the combinations for "Offer Alternative", which means there are more possible combinations (2 times 2^7).<br>
• Model the easiest and the most combinations on top of the decision table. For the eight variables use one row with possible hits "Yes" or "No".<br>
• Model the 32 rows for "Reject" below.<br>
• Set the hit policy to "First".<br>
<br>
By applying this approach, every possible combination is covered.
<br>
<br>
No picture is shared within this readme, as the table contains 13 inputs with 32 rows. Please follow the link to the dmn and boolean truth table for further studies: <br> <br>
dmn: digibp-weisshorn/src/main/resources/modelling/Decicion Table_v1-6_Application Assessment.dmn <br>
truth table: digibp-weisshorn/To-Be Process/ Decicion Table_v1-4_Application Assessment.xlsx 
<br><br>

## TO-BE Digitalized Process
![](https://github.com/DigiBP/digibp-weisshorn/blob/master/Wiki/Process%20Model_v1-9-Health%20Insurance%20Application.jpeg?raw=true)

1.	The customer opens the google form link https://docs.google.com/forms/d/e/1FAIpQLSd4OtjgHhR-bNpov0TNpOeCzjLxJA_8aA0OUY9xv4d1wJtGcA/viewform and fills out the application form. By pressing the send button, it will be sent via Integromat (HTTP) to the digibp herokuapp with all relevant variables. 
2.	Integromat sends an email to the health insurance applicant where the email must be verified.
3.	Now Camunda executes the decision table “Assess the application”. The decision table uses different input variables from the form ( e.g. HIV, cancer, age). According to the variable there are three possible outputs: <br>
•	Reject <br>
•	Accept <br>
•	Offer Alternative <br>
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

## Integrations

## Database

## Live Presentation
Following gif illustrates the running process:
![Running Process](https://github.com/DigiBP/digibp-weisshorn/blob/master/Wiki/Process Run.gif)

Whereas the gif below shows the integrations and the database:
![Running Process](https://github.com/DigiBP/digibp-weisshorn/blob/master/Wiki/Integromat.gif)


## Maintainer
- [Digitalisation of Business Processes](https://github.com/digibp)

## License

- [Apache License, Version 2.0](https://github.com/DigiBP/digibp-archetype-camunda-boot/blob/master/LICENSE)
