# api-proxies-via-maven
Demonstration of Apigee API proxies managed, configured and tested using Apigeetool, Maven and Github.

## APIs Examples
* forecastapi (Original API proxy example, modified to use new weather API backend).

## Getting Started
- [ ] [Sign up for an Apigee Account!](https://accounts.apigee.com/accounts/sign_up). Not required if already provided.
- [ ] [Sign up for GitHub account and install Git](https://github.com). Not required if already provided.

- [ ] [Download and install Maven 3.0.*](http://maven.apache.org/download.cgi)
- [ ] [Install Apigeetool](https://github.com/apigee/apigeetool-node) ```npm install -g apigeetool```

- [ ] Clone this repo https://github.com/kurtkanaskie/api-proxies-via-maven
- [ ] ```cd forecastapi``` 
- [ ] Execute ```mvn install -Ptest -Dusername={your-username} -Dpassword={your-password} -Dorg={your-org-name}```

If everything ran OK, you will see BUILD SUCCESS message at the end of the output, after lots of info on the first run.

If the tests don't run correctly check the files in the tests directory for your API endpoints.

Next steps, See [README-maven](https://github.com/kurtkanaskie/api-proxies-via-maven/README-maven.md) for more details.

## Use Cases

### UI driven changes in Apigee Management Console
As an API developer, I made changes to my apiproxy in Management Console and I want to save my changes to GitHub.

- Changes
	* Manual changes in Management Console (with our without a new revision)
- Update local repository
	* Create a GitHub branch ```git branch ...```
	* Fetch the proxy ```apigeetool fetchproxy -u your-username -o your-org -n forecastapi -r 1 -f apiproxy-changed.zip```
	* Unzip and compare changes ```sdiff apiproxy apiproxy-changed```
- Test the changes
	- Test the changes ```mvn jmeter:jmeter ...```
	- Deploy any additional changes to Apigee ```mvn install or update ...```
- Update Git repository
	Commit the changes ```git commit -am ...; git push```

### Code driven changes in local repository
As an API developer, I made changes to my apiproxy in my local repository and in GitHub and I want to move into Apigee.
- [ ] Create a GitHub branch ```git branch ...```
- [ ] Make changes to the proxy and test ```mvn jmeter:jmeter ...```
- [ ] Test the changes ```mvn jmeter:jmeter ...```


## More Documentation
* [Apigee Maven Plugin on Git](https://github.com/apigee/apigee-deploy-maven-plugin)


