# Example apiproxy backend-analytics

###Download API proxy

#####Management API 
* curl -X GET -u username:password "https://api.enterprise.apigee.com/v1/o/ORG/apis"
* curl -X GET -u username:password "https://api.enterprise.apigee.com/v1/o/ORG/apis/backend-analytics"
* curl -X GET -u username:password "https://api.enterprise.apigee.com/v1/o/ORG/apis/backend-analytics/revisions"
* curl -X GET -u username:password "https://api.enterprise.apigee.com/v1/o/ORG/apis/backend-analytics/revisions/2"
* curl -X GET -u username:password "https://api.enterprise.apigee.com/v1/o/ORG/apis/backend-analytics/revisions/2?format=bundle" -o backend-analytics.zip

#####Apigeetool
```apigeetool fetchproxy -u {{UN}} -p {{PW}} -o {{ORG}} -n backend-analytics -r {{REV}}```

#####Maven
Download the API bundle, as per above.

* ```mvn install -P test -Dusername=your.name@email.com -Dpassword=secret-value``` (install and test)
* ```mvn deploy -P test -Dusername=your.name@email.com -Dpassword=secret-value``` (just deploy)
* ```mvn jmeter:jmeter -P test -DtestData=backend-analytics_test.csv -DthreadNum=5 -DrampUpPeriodSecs=5 -DloopCount=2``` (test in test)
* ```mvn jmeter:jmeter -P prod -DtestData=backend-analytics_prod.csv -DthreadNum=5 -DrampUpPeriodSecs=5 -DloopCount=2``` (test in prod)
* ```mvn deploy -P prod (deploy - seems to work but throws error)
* ```mvn install -P prod -Doptions=inactive

###To test node locally
* ```cd apiproxy/resources/node```
* Update/install node modules ```npm install```
* Invoke with ```ENV=local node api.js```
