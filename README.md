# api-proxies-via-maven
Demonstration of Apigee API proxies managed, configured and tested using Apigeetool, Maven and Github.

## APIs Examples
* forecastapi (Weather API proxy, modified to use new backend URL).
* backend-analytics (Node.js API proxy showing example of how to create custom analytics).

## Getting Started
- [Sign up for an Apigee Account!](https://accounts.apigee.com/accounts/sign_up). If not already.
- [Sign up for GitHub account and install Git](https://github.com). If not already.

- [Download and install Maven 3.0.*](http://maven.apache.org/download.cgi)
- [Install Apigeetool](https://github.com/apigee/apigeetool-node) ```npm install -g apigeetool```

- Clone this repo https://github.com/kurtkanaskie/api-proxies-via-maven
- ```cd forecastapi``` and execute ```mvn install -P test -Dusername={your-un} -Dpassword={your-pw} -Dorg={your-org-name}```

If everything ran OK, you will see BUILD SUCCESS message at the end of the output, after lots of info on the first run.

If the tests don't run correctly check the files in the tests directory for your API endpoints.

Next steps, See [README-maven](https://github.com/kurtkanaskie/api-proxies-via-maven/blob/master/README-maven.md) for more command details.

## Use Cases

### UI driven changes in Apigee Management Console
As an API developer, I made changes to my apiproxy in Management Console and I want to save my changes to GitHub.

- Changes
	* Manual changes in Management Console (with our without a new revision)
- Test the changes
	* Test the changes ```mvn jmeter:jmeter ...```
	* Deploy any additional changes to Apigee ```mvn install or update ...```
- Update local repository
	* Create a GitHub branch ```git branch ...```
	* Fetch the proxy ```apigeetool fetchproxy -u your-un -o your-org -n forecastapi -r 1 -f apiproxy-changed.zip```
	* Unzip and compare changes ```sdiff apiproxy apiproxy-changed```
- Update Git repository
	* Commit the changes ```git commit -am ...; git push```

### Code driven changes in local repository
As an API developer, I want to make changes to my apiproxy in my local repository and GitHub and then move into Apigee.
- Create a GitHub branch ```git branch branchname ...; git checkout branchname```
- Make changes to the proxy and deploy ```mvn install -P test ...```
- Make additional test cases and test ```mvn jmeter:jmeter ...```
- Commit to Github ```git commit ...; git push```
- Merck with master ``` git checkout master; git merge branchame```


##Some Maven Commands – apigee.options

#####Configure, package, import, deploy, and test bundle (default validate apigee.option) – Creates new revision

```mvn install -P test -Dusername=your-username -Dpassword=your-password -Dorg=your-org-name``` (these can be configured in shared_pom.xml)

#####Configure, package, import, override, deploy, and test bundle (default validate apigee.option) – Overrides current revision

```mvn install -P test -Doptions=validate,update```

#####Delete current bundle deployed

```mvn install -P test -Doptions=clean```

```mvn install -P test -Doptions=inactive```

#####Configure and package bundle. Does not import

```mvn package -P test```

#####Run tests only

```mvn jmeter:jmeter -P test -name -DtestData=forecastapi_test.csv -DthreadNum=5 -DrampUpPeriodSecs=5 -DloopCount=2```


###The following are available options:
a. clean - This will delete the last deployed revision in an environment.
b. validate - This will validate a bundle before importing. Thus if you want strict validation then its required.
c. inactive - This will just import the bundle without activating the bundle.
d. override - This is used for seamless deployment. This must be supplied with apigee.override.delay parameter. The apigee.override.delay expects delay to be given in seconds.
e. force - This will recheck the un deployment of bundle before proceeding further deployment.
f. update - This will update the deployed revision. This is similar to import with validation but no new revision is created. If there any errors in the bundle, error is thrown and the existing bundle is left intact. In case the revision they are trying to update is deployed, it will internally trigger undeployment and deployment. It is completely in the background and not visible in the response. It is advised not to update the deployed revision. (UI could show a warning or something in this case).

## More Documentation
* [Apigee Maven Plugin on Git](https://github.com/apigee/apigee-deploy-maven-plugin)


