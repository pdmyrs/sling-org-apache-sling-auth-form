# PDMYRS

How to run in AEM 6.4

## Login using We.Retail

###  1. After building, install the bundle using the Web Console (there’s no package)

###  2. Check the Sling Authenticator console
* Make sure the service is running on path '/'. 
* Use the ConfigMgr to change the service.ranking in the Sling Form Based Authentication Handler config to 200000. It now is the highest service running on path '/', so it will be the first Authenticator in line to handle requests.

### 3. Add sling source for running through the debugger

```	
<!-- Added by pdmyrs for sling auth debugging -->
	<dependency>
		<artifactId>org.apache.sling.auth.core</artifactId> 
		<version>1.4.2</version> 
		<groupId>org.apache.sling</groupId> 
		<scope>provided</scope> 
	</dependency>  
	

<!-- Added by pdmyrs for sling request debugging -->
    	<dependency>
    		<groupId>org.apache.sling</groupId>
    		<artifactId>org.apache.sling.engine</artifactId>
    		<version>2.6.12</version>
    		<scope>provided</scope>
    	</dependency>

<!-- Added by pdmyrs for sling resource debugging -->
<!-- <dependency>  -->
<!-- 	<groupId>org.apache.sling</groupId> -->
<!-- 	<artifactId>org.apache.sling.api</artifactId> -->
<!-- 	<version>2.16.4</version> -->
<!-- 	<scope>provided</scope> -->
<!-- </dependency>       -->
<dependency>
    <groupId>org.apache.sling</groupId>
    <artifactId>org.apache.sling.resourceresolver</artifactId>
    <version>1.5.34</version>
	<scope>provided</scope>
</dependency>
```
* In Eclipse, use the Maven > Add Source to pull in source files.
* Go to Maven Dependencies > org.apache.sling.auth.core.impl.SlingAuthenticator and set a breakpoint in the handleSecurity( ) method.
** Note: alternatively set a breakpoint in the org.apache.sling.auth.form.impl.FormAuthenticationHandler extractCredentials( ) method.

### 4. Use We.Retail signin page to login
```
http://localhost:4503/content/we-retail/us/en/community/signin.html 
```

* Step through the debugger to anaylize execution flow.



