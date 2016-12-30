# Introduction
This tutorial follows [this](https://developer.salesforce.com/docs/atlas.en-us.api_asynch.meta/api_asynch/asynch_api_quickstart_requests_intro.htm) using curl. Please refer to UpdateBatchResultsTest() for a detailed bulk Insert, query and update C# example

## Log In Using the SOAP API
```curl https://test.salesforce.com/services/Soap/u/38.0 -H "Content-Type: text/xml; charset=UTF-8" -H "SOAPAction: login" -d @login.txt```

Response:
```
<?xml version="1.0" encoding="UTF-8"?>
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns="urn:partner.soap.sforce.com" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
   <soapenv:Body>
      <loginResponse>
         <result>
            <metadataServerUrl>https://eci--Full1.cs25.my.salesforce.com/services/Soap/m/38.0/00D1b000000CxK4</metadataServerUrl>
            <passwordExpired>false</passwordExpired>
            <sandbox>true</sandbox>
            <serverUrl>https://eci--Full1.cs25.my.salesforce.com/services/Soap/u/38.0/00D1b000000CxK4</serverUrl>
            <sessionId>00D1b000000CxK4!AQkAQGz9a9Q073CcULwOBTvCq_Vl6Zx7US2jZh2iC6yH.LxTmouqvkUBiFoDiRuZMq1iJ84d.Y4DHXSXqLYLNcadAIML2U1W</sessionId>
            <userId>00530000000cCZ3AAM</userId>
            <userInfo>
               <accessibilityMode>false</accessibilityMode>
               <currencySymbol xsi:nil="true" />
               <orgAttachmentFileSizeLimit>10485760</orgAttachmentFileSizeLimit>
               <orgDefaultCurrencyIsoCode xsi:nil="true" />
               <orgDefaultCurrencyLocale xsi:nil="true" />
               <orgDisallowHtmlAttachments>false</orgDisallowHtmlAttachments>
               <orgHasPersonAccounts>false</orgHasPersonAccounts>
               <organizationId>00D1b000000CxK4EAK</organizationId>
               <organizationMultiCurrency>true</organizationMultiCurrency>
               <organizationName>ECI Consulting</organizationName>
               <profileId>00e40000000wxkMAAQ</profileId>
               <roleId>00E40000000sk6yEAA</roleId>
               <sessionSecondsValid>28800</sessionSecondsValid>
               <userDefaultCurrencyIsoCode>USD</userDefaultCurrencyIsoCode>
               <userEmail>appservices@eci.com</userEmail>
               <userFullName>App Services</userFullName>
               <userId>00530000000cCZ3AAM</userId>
               <userLanguage>en_US</userLanguage>
               <userLocale>en_US</userLocale>
               <userName>appservices@eci.com.full1</userName>
               <userTimeZone>America/New_York</userTimeZone>
               <userType>Standard</userType>
               <userUiSkin>Theme3</userUiSkin>
            </userInfo>
         </result>
      </loginResponse>
   </soapenv:Body>
</soapenv:Envelope>
```

## Create a Job command
```curl https://eci--full1.cs25.my.salesforce.com/services/async/38.0/job -H "X-SFDC-Session: 00D1b000000CxK4!AQkAQGz9a9Q073CcULwOBTvCq_Vl6Zx7US2jZh2iC6yH.LxTmouqvkUBiFoDiRuZMq1iJ84d.Y4DHXSXqLYLNcadAIML2U1W" -H "Content-Type: application/xml; charset=UTF-8" -d @job.txt```

Response:
```
<?xml version="1.0" encoding="UTF-8"?><jobInfo
   xmlns="http://www.force.com/2009/06/asyncapi/dataload">
 <id>7501b000000PMh7AAG</id>
 <operation>update</operation>
 <object>Account</object>
 <createdById>00530000000cCZ3AAM</createdById>
 <createdDate>2016-12-29T17:11:20.000Z</createdDate>
 <systemModstamp>2016-12-29T17:11:20.000Z</systemModstamp>
 <state>Open</state>
 <concurrencyMode>Parallel</concurrencyMode>
 <contentType>CSV</contentType>
 <numberBatchesQueued>0</numberBatchesQueued>
 <numberBatchesInProgress>0</numberBatchesInProgress>
 	
 <numberBatchesFailed>0</numberBatchesFailed>
 <numberBatchesTotal>0</numberBatchesTotal>
 <numberRecordsProcessed>0</numberRecordsProcessed>
 <numberRetries>0</numberRetries>
 <apiVersion>38.0</apiVersion>
 <numberRecordsFailed>0</numberRecordsFailed>
 <totalProcessingTime>0</totalProcessingTime>
 <apiActiveProcessingTime>0</apiActiveProcessingTime>
 <apexProcessingTime>0</apexProcessingTime>
</jobInfo>
```

## Add a Batch to the Job command
```curl https://eci--full1.cs25.my.salesforce.com/services/async/38.0/job/7501b000000PMh7AAG/batch -H "X-SFDC-Session: 00D1b000000CxK4!AQkAQGz9a9Q073CcULwOBTvCq_Vl6Zx7US2jZh2iC6yH.LxTmouqvkUBiFoDiRuZMq1iJ84d.Y4DHXSXqLYLNcadAIML2U1W" -H "Content-Type: text/csv; charset=UTF-8" --data-binary @data.csv```

Response:
```
<?xml version="1.0" encoding="UTF-8"?><batchInfo
   xmlns="http://www.force.com/2009/06/asyncapi/dataload">
 <id>7511b000000QeA8AAK</id>
 <jobId>7501b000000PMh7AAG</jobId>
 <state>Queued</state>
 <createdDate>2016-12-29T18:42:58.000Z</createdDate>
 <systemModstamp>2016-12-29T18:42:58.000Z</systemModstamp>
 <numberRecordsProcessed>0</numberRecordsProcessed>
 <numberRecordsFailed>0</numberRecordsFailed>
 <totalProcessingTime>0</totalProcessingTime>
 <apiActiveProcessingTime>0</apiActiveProcessingTime>
 <apexProcessingTime>0</apexProcessingTime>
</batchInfo>
```

## Close the Job command
```curl https://eci--full1.cs25.my.salesforce.com/services/async/38.0/job/7501b000000PMh7AAG -H "X-SFDC-Session: 00D1b000000CxK4!AQkAQGz9a9Q073CcULwOBTvCq_Vl6Zx7US2jZh2iC6yH.LxTmouqvkUBiFoDiRuZMq1iJ84d.Y4DHXSXqLYLNcadAIML2U1W" -H "Content-Type: application/xml; charset=UTF-8" -d @close_job.txt```

Response:
```
<?xml version="1.0" encoding="UTF-8"?><jobInfo
   xmlns="http://www.force.com/2009/06/asyncapi/dataload">
 <id>7501b000000PMh7AAG</id>
 <operation>update</operation>
 <object>Account</object>
 <createdById>00530000000cCZ3AAM</createdById>
 <createdDate>2016-12-29T17:11:20.000Z</createdDate>
 <systemModstamp>2016-12-29T17:11:20.000Z</systemModstamp>
 <state>Closed</state>
 <concurrencyMode>Parallel</concurrencyMode>
 <contentType>CSV</contentType>
 <numberBatchesQueued>0</numberBatchesQueued>
 <numberBatchesInProgress>0</numberBatchesInProgress>
 <numberBatchesCompleted>1</numberBatchesCompleted>
 <numberBatchesFailed>0</numberBatchesFailed>
 <numberBatchesTotal>1</numberBatchesTotal>
 <numberRecordsProcessed>3</numberRecordsProcessed>
 <numberRetries>0</numberRetries>
 <apiVersion>38.0</apiVersion>
 <numberRecordsFailed>0</numberRecordsFailed>
 <totalProcessingTime>695</totalProcessingTime>
 <apiActiveProcessingTime>519</apiActiveProcessingTime>
 <apexProcessingTime>276</apexProcessingTime>
</jobInfo>
```

## Check Batch Status command
```curl https://eci--full1.cs25.my.salesforce.com/services/async/38.0/job/7501b000000PMh7AAG/batch/7511b000000QeA8AAK -H "X-SFDC-Session: 00D1b000000CxK4!AQkAQGz9a9Q073CcULwOBTvCq_Vl6Zx7US2jZh2iC6yH.LxTmouqvkUBiFoDiRuZMq1iJ84d.Y4DHXSXqLYLNcadAIML2U1W"```

Response:
```
<?xml version="1.0" encoding="UTF-8"?><batchInfo
   xmlns="http://www.force.com/2009/06/asyncapi/dataload">
 <id>7511b000000QeA8AAK</id>
 <jobId>7501b000000PMh7AAG</jobId>
 <state>Completed</state>
 <createdDate>2016-12-29T18:42:58.000Z</createdDate>
 <systemModstamp>2016-12-29T18:42:59.000Z</systemModstamp>
 <numberRecordsProcessed>3</numberRecordsProcessed>
 <numberRecordsFailed>0</numberRecordsFailed>
 <totalProcessingTime>695</totalProcessingTime>
 <apiActiveProcessingTime>519</apiActiveProcessingTime>
 <apexProcessingTime>276</apexProcessingTime>
</batchInfo>
```

### login.txt
Change the username and password accordingly
```
<?xml version="1.0" encoding="utf-8" ?>
<env:Envelope xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:env="http://schemas.xmlsoap.org/soap/envelope/">
<env:Body>
	<n1:login xmlns:n1="urn:partner.soap.sforce.com">
	<n1:username>your username</n1:username>
	<n1:password>your password</n1:password>
	</n1:login>
</env:Body>
</env:Envelope>
```

### job.txt
This is an *update* job
```
<?xml version="1.0" encoding="UTF-8"?>
<jobInfo xmlns="http://www.force.com/2009/06/asyncapi/dataload">
    <operation>update</operation>
    <object>Account</object>
    <contentType>CSV</contentType>
</jobInfo>
```

### data.csv
Updates the Account website
```
Id,Website
0011b000004xkwTAAQ,"www.somerandomesite123.com"
0011b000004xmNWAAY,"www.somerandomesite123.com"
0011b000004xkeaAAA,"www.somerandomesite123.com"
```

### close_job.txt
```
<?xml version="1.0" encoding="UTF-8"?>
<jobInfo xmlns="http://www.force.com/2009/06/asyncapi/dataload">
  <state>Closed</state>
</jobInfo>
```