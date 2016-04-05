# README Maven

###Basic Commands – apigee.options

#####Configure, package, import, deploy, and test bundle (default validate apigee.option) – Creates new revision

```mvn install -Ptest -Dusername=your-username -Dpassword=your-password -Dorg=your-org-name```

#####Configure, package, import, override, deploy, and test bundle (default validate apigee.option) – Overrides current revision

```mvn install -Ptest -Dusername=your-username -Dpassword=your-password -Dorg=your-org-name -Doptions=validate,update```

#####Delete current bundle deployed

```mvn install -Ptest -Dusername=your-username -Dpassword=your-password -Dorg=your-org-name -Doptions=clean```

```mvn install -Ptest -Dusername=your-username -Dpassword=your-password -Dorg=your-org-name -Doptions=inactive```

#####Configure and package bundle. Does not import

```mvn package -Ptest -Dusername=$ae_username -Dpassword=$ae_password -Dorg=your-org-name```

#####Run tests only

```mvn jmeter:jmeter -Ptest -Dusername=your-username -Dpassword=your-password -Dorg=your-org-name -DtestData=forecastapi_test.csv -DthreadNum=5 -DrampUpPeriodSecs=5 -DloopCount=2```


###The following are available options:
a. clean - This will delete the last deployed revision in an environment.

b. validate - This will validate a bundle before importing. Thus if you want strict validation then its required.

c. inactive - This will just import the bundle without activating the bundle.

d. override - This is used for seamless deployment. This must be supplied with apigee.override.delay parameter. The apigee.override.delay expects delay to be given in seconds.

e. force - This will recheck the un deployment of bundle before proceeding further deployment.

f. update - This will update the deployed revision. This is similar to import with validation but no new revision is created. If there any errors in the bundle, error is thrown and the existing bundle is left intact. In case the revision they are trying to update is deployed, it will internally trigger undeployment and deployment. It is completely in the background and not visible in the response. It is advised not to update the deployed revision. (UI could show a warning or something in this case).

## More Documentation
* [Apigee Maven Plugin on Git](https://github.com/apigee/apigee-deploy-maven-plugin)


