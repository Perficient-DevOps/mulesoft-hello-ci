# Simple MuleSoft project



# Setup work

Updated the `~/.m2/settings.xml` to include the mulesoft enterprise repository, which in this case you will need to enter your username and password from you mulesoft service account.

 * https://docs.mulesoft.com/mule-user-guide/v/3.6/configuring-maven-to-work-with-mule-esb

     <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                          https://maven.apache.org/xsd/settings-1.0.0.xsd">
      <servers>
        <server>
          <id>MuleRepository</id>
          <username>XXX</username>
          <password>YYY</password>
        </server>
      </servers>

      <profiles>
        <profile>
          <id>Mule</id>
          <activation>
            <activeByDefault>true</activeByDefault>
          </activation>
          <repositories>
            <repository>
              <id>MuleRepository</id>
              <name>MuleRepository</name>
              <url>https://repository.mulesoft.org/nexus-ee/content/repositories/releases-ee/</url>
              <layout>default</layout>
              <releases>
                <enabled>true</enabled>
              </releases>
              <snapshots>
                <enabled>true</enabled>
              </snapshots>
            </repository>
          </repositories>
        </profile>
      </profiles>

    </settings>



Configured Maven `pom.xml` to resolve dependencies as in the documentation:

 * https://docs.mulesoft.com/mule-user-guide/v/3.6/configuring-maven-to-work-with-mule-esb
 * https://docs.mulesoft.com/mule-user-guide/v/3.6/mule-esb-plugin-for-maven
