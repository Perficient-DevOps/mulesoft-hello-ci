# Simple MuleSoft project

# Issues

 Having problem running `mvn package`

    [ERROR] Failed to execute goal on project hello-ci: Could not resolve dependencies for project com.mycompany:hello-ci:mule:1.0.0-SNAPSHOT: The following artifacts could not be resolved: com.mulesoft.muleesb:mule-core-ee:jar:3.9.0, com.mulesoft.muleesb.modules:mule-module-spring-config-ee:jar:3.9.0, com.mulesoft.muleesb.transports:mule-transport-jdbc-ee:jar:3.9.0, com.mulesoft.muleesb.transports:mule-transport-jms-ee:jar:3.9.0: Failure to find com.mulesoft.muleesb:mule-core-ee:jar:3.9.0 in http://repository.mulesoft.org/releases/ was cached in the local repository, resolution will not be reattempted until the update interval of mulesoft-releases has elapsed or updates are forced -> [Help 1]

# Setup work
 Need to configure Maven to resolve dependencies.

 * https://docs.mulesoft.com/mule-user-guide/v/3.6/configuring-maven-to-work-with-mule-esb
 * https://docs.mulesoft.com/mule-user-guide/v/3.6/mule-esb-plugin-for-maven
