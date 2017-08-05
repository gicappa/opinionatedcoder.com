# General opinions

## IDE & Editors
## Application Structures
## Architectures
In this section I will present a bunch of architectures that can be built using chef over different server systems:
* AWS
* Digital Ocean
* Docker

## Hints & Snippets ToolBox
### GIT
#### Remove branches no longer on remote
```git gc --prune=now``` do the trick
```git fetch -p```
#### Rename a branch
````git branch -m <oldname> <newname>````

If you want to rename the current branch, you can simply do:

````git branch -m <newname>````

#### Caching GIT credential for https access
```git config --global credential.helper osxkeychain```
or for linux
```git config --global credential.helper "cache --timeout=3600"```

http://stackoverflow.com/questions/5343068/is-there-a-way-to-skip-password-typing-when-using-https-github

#### Checking the tracking between 
```git branch -vv```

# SysAdmin
## iotop 
http://www.cyberciti.biz/hardware/linux-iotop-simple-top-like-io-monitor/

# Opening a HTTP server on the curren directory
python -m SimpleHTTPServer

# Maven 
## Create a local repository where to store an artifact without using artifactory
Add this lines to the ```pom.xml``` of the artifact to be exported 
```xml
  <distributionManagement>

    <!-- Publish versioned releases here -->
    <repository>
      <id>local-repo-r</id>
      <name>my releases</name>
      <url>file://${project.basedir}/local-repo/releases</url>
    </repository>

    <!-- Publish snapshots here -->
    <snapshotRepository>
      <id>local-repo</id>
      <name>my snapshots</name>
      <url>file://${project.basedir}/local-repo/snapshots</url>
    </snapshotRepository>

  </distributionManagement>
```
and launch ```mvn deploy```. Than copy the directory local-repo that has been created in the project where you need the exported jar. In the ```pom.xml``` of the client of the jar add the following lines:
```xml
<repositories>
    <repository>
      <id>local-repo</id>
      <url>file://${main.basedir}/local-repo/snapshots</url>
      <snapshots>
        <enabled>true</enabled>
      </snapshots>
      <releases>
        <enabled>false</enabled>
      </releases>
    </repository>
    
    <repository>
      <id>local-repo-r</id>
      <url>file://${main.basedir}/local-repo/releases</url>
      <snapshots>
        <enabled>false</enabled>
      </snapshots>
      <releases>
        <enabled>true</enabled>
      </releases>
    </repository>
  </repositories>
```

# Drafts
## Evolution of the coding by intention
When coding just create the interface of what is needed and create and shape the methods while using them. After the interface is fitting the needs just add the desired behavior.

## Coding hints 
When working with classes belonging to some external libraries or I/O related details is always necessary to challeng the abstraction already present and their shape and protocol. The risk is always to create some procedural code. BTW Is better to create some procedural code if we are unsure about the abstraction and create the abstraction in a secod time when the behavior of the class is well defined.
