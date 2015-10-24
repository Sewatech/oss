# What is the process to release on Maven Central ?

Before we can see the artifact on Maven Central, we have to release it to an
intermediate repository. The content of the artifact will be validated before
being uploaded to Maven Central.

The only repository supported is :

* https://oss.sonatype.org/

# Settings for Sonatype OSS repository

The credentials to the Sonatype staging and snapshot repositories have to be
declare in ~/.m2/settings.xml.

    <server>
      <id>sonatype-nexus-snapshots</id>
      <username>usertoken-name</username>
      <password>usertoken-password</password>
    </server>
    <server>
      <id>sonatype-nexus-staging</id>
      <username>usertoken-name</username>
      <password>usertoken-password</password>
    </server>

The credentials can be the Sonatype JIRA ones. It is safer to use a user token
from the Nexus profile.

# How to release on Sonatype OSS repository ?

Build and deploy the artifact, with the javadoc and the source code.
This is done in the _release_ profile :

    mvn clean deploy -Prelease

The artifact should be now in the staging repository. Close it and it will
enable the release button. Then click on release and the artifact should be
moved to the release repository and then to the Maven Central repository after
few minutes.

# References

* [Sonatype OSSRH Guide](http://central.sonatype.org/pages/ossrh-guide.html)
* [Sonatype OSSRH with Apache Maven](http://central.sonatype.org/pages/apache-maven.html)
