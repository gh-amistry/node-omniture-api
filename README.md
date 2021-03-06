# node-omniture-api
An extremely simple library for making calls to api.omniture.com (v1.4).

For a fuller set of features, check out the excellent [nomniture](https://github.com/imartingraham/nomniture).

## Installation

```
npm install node-omniture-api --save
```

## Usage

```node
var OmnitureAPI = require('node-omniture-api')
var omniture = new OmnitureAPI(%USER_NAME%,%SHARED_SECRET%);
 
//Basic request to fetch page views
var requestData = {
	"reportDescription":{
		"reportSuiteID":"%REPORT_SUITE_ID%"
	}
}    

omniture.queueAndFetchReport(requestData,function(success,data) {
	if ( success ) {
		console.log(data);
	} else {
		console.error(data);
	}
});
```

## Getting started with Omniture's API

The required Username and Shared Secret can be found under [Account Info](https://sc.omniture.com/p/suite/1.3/index.html?a=User.GetAccountInfo)

To get started with the API, head over to Adobe's [API Explorer](https://marketing.adobe.com/developer/api-explorer)


## Methods

All `callbacks` are passed a `success` boolean and a `data` JSON object.

#### queueAndFetchReport( requestData , callback )

Most likely, you'll use this library to run reports and pull traffic numbers for your website. The way Omniture works is that reports must first be queued and then run at a later time (usually within a few seconds.) Complex reports may take several seconds to complete, so this function handles queuing and waiting for completion all in one go.

#### fetchReport( reportId , callback )

Use fetchReport if you already have the ID of a report that has already been queued. This function will recursively call itself until the report is ready.

#### makeRequest( endpoint , data , callback )

Make a general request to the Omniture API using an arbitrary endpoint (e.g. `'Report.Get'`). Learn more about the specifics of what you can call over at the [API Explorer](https://marketing.adobe.com/developer/api-explorer).