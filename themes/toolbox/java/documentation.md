# Javadoc

I could not find a good loking javadoc. I tried Doclava 
with some difficulties and UmlGraphDoc to generate some 
UML modeling from the code written.

## Doclava

is coming from google 

```xml
<configuration>
  <!--<aggregate>true</aggregate>-->
  <docfilessubdirs>true</docfilessubdirs>
  <show>private</show>
  <docletArtifact>
    <groupId>com.google.doclava</groupId>
    <artifactId>doclava</artifactId>
    <version>1.0.6</version>
  </docletArtifact>
  <doclet>com.google.doclava.Doclava</doclet>
  <bootclasspath>${sun.boot.class.path}</bootclasspath>
  <additionalparam>
    -quiet
    -federate JDK http://download.oracle.com/javase/6/docs/api/index.html?
    -federationxml JDK http://doclava.googlecode.com/svn/static/api/openjdk-6.xml
    -hdf project.name "CISE"
    -d target/apidocs
    -federate JDK http://download.oracle.com/javase/6/docs/api/index.html?
    -federationxml JDK http://doclava.googlecode.com/svn/static/api/openjdk-6.xml
  </additionalparam>
  <useStandardDocletOptions>false</useStandardDocletOptions>
  <additionalJOption>-J-Xmx1024m</additionalJOption>
</configuration>
```

## UmlGraphDoc

```xml
<!-- create an appropriate javadoc -->
<plugin>
  <artifactId>maven-javadoc-plugin</artifactId>
  <version>2.7</version>
  <configuration>
    <!--<stylesheetfile>${basedir}/src/javadoc/stylesheet.css-->
    <!--</stylesheetfile>-->
    <javadocDirectory>${main.basedir}/src/javadoc</javadocDirectory>
    <docfilessubdirs>true</docfilessubdirs>
    <aggregate>true</aggregate>
    <show>private</show>
    <doclet>org.umlgraph.doclet.UmlGraphDoc</doclet>
    <docletArtifact>
      <groupId>org.umlgraph</groupId>
      <artifactId>umlgraph</artifactId>
      <version>5.6.6</version>
    </docletArtifact>
    <additionalparam>
        -inferrel
        -attributes
        -types
        -visibility
        -quiet
        -hide java.*
        -collpackages java.util.*
        -qualify
        -postfixpackage
      <!-- -nodefontsize 9-->
      <!-- -nodefontpackagesize 7-->
        -bgcolor white
        -edgecolor "#A0A0A4"
        -edgefontname "Helvetica"
        -nodefontname "Helvetica"
        -nodefontabstractname "Helvetica"
        -nodefontclassabstractname "Helvetica"
        -nodefontclassname "Helvetica"
        -nodefontpackagename "Helvetica"
        -nodefonttagname "Helvetica"
        -edgefontcolor "#A0A0A4"
        -nodefontcolor "#A0A0A4"
        -edgefontsize 9
        -nodefontclasssize 9
        -nodefontpackagesize 9
        -nodefontsize 9
        -nodefonttagsize 9
        -nodefillcolor "white"
      <!-- -collapsible-->
      <!-- -useimports-->
      <!-- -apidocmap-->
      <!-- -hdf project.name "${project.name}" -d ${project.build.directory}/apidocs-->
    </additionalparam>
  </configuration>
</plugin>

```
