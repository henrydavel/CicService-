# eoh_assessment
CicService for EOH-bit-platoon

https://github.com/henrydavel/eoh_assessment.git
# Wildfly:
Download Wildfly10 and replace the c:~ \wildfly-10.1.0.Final\standalone\configuration folder with the folder in configuration.zip
This should configure Wildfly and the default datasource

# Source:
Extract Cicservice.zip to a folder of your choice and make sure Wildfly is up and running.
From cmd-promt, run: mvn clean install wildfly:deploy 
Use wilfly:redeploy if already deployed
This should compile and download all the relevant libraries from your maven repo and deploy the .WAR to wildfly

# DB:
There is an import.sql that runs. Wildfly will by default load the script and create all relevant tables according to the @Entity in the relevant class
There are 2 tables, Cic and Customer
Cic: This will store all relevant details for each email being send. It will also contain an extra column that will store the person who has sent the mail.
Customer: this will store all the people/customers that has/will send an email. Did NOT have enough time to use this table though ie. getting all the emails/cic’s of a specific user

# Testing
You can add extra data to src\main\resources\import.sql and redeploy should you want to test with more than 2 entries.

To test the GET (/cic/{cicid}) goto:

http://127.0.0.1:8080/CicService/eoh/cicservice/cic/1 (0 or1 can be used as per default DB-entries after that the cicId’s should start from 10 as per the SequenceGenerator)

You should get a JSON reply something simmiliar to:
{"result":"{"cicId":1,"cicType":"EMAIL","subject":"I am your father..","body":"....Luke, together we can rule...","sourceSystem":"SYSTEM","cicTimestamp":"2018-01-02 03:42:30.136","cicCustomerID":2}"}

To test the POST (/cic}) run:
main.java.eoh.test.Test_POST.java
This will create a Cic and send it to the CicService to be persisted in the DB.
You should see the Cic being persisted as well as  well as confirmation in the output console

{"cicType":"EMAIL","subject":"I am your father..","body":"....Luke, together we can rule...","sourceSystem":"SYSTEM","cicTimestamp":"2018-01-02 03:54:02.713","cicCustomerID":2}

Output from Server .... 

Persisted CIC



