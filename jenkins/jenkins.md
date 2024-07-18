# Jenkins Cheatsheet

## Jenkins Scripting

For each, navigate to `http://<jenkins-url>/sript` and run script

### Print Jenkins Plugins

```groovy
def pluginList = new ArrayList(Jenkins.instance.pluginManager.plugins)
pluginList.sort { it.getShortName().toLowerCase() }.each {
    plugin -> 
    println ("${plugin.getShortName()}-_-${plugin.getVersion()}")
}
return true
```

### Print Jenkins Credentials

```groovy
def CREDENTIAL_ID = "credential_id" // Place Credential ID Here
def creds = com.cloudbees.plugins.credentials.CredentialsProvider.lookupCredentials(
  com.cloudbees.plugins.credentials.common.IdCredentials.class,
  Jenkins.instance,
  null,
  null
);
for (c in creds) {
  if (c.id == CREDENTIAL_ID) {
    c.properties.each { prop, val ->
      // Ignore certain properties
      if (prop in ["class", "descriptor", "scope", "privateKeySource"]) return
      if (c.hasProperty(prop)) { println (prop + ": " + val) }
    }
  }
}
return true
```

### Get All Jobs

```groovy
Jenkins.instance.getAllItems(AbstractItem.class).each {
    // Filter out jobs within multibranch pipelines
    if (it.parent && it.parent.class != org.jenkinsci.plugins.workflow.multibranch.WorkflowMultiBranchProject && it.class != hudson.maven.MavenModule) {
        println it.fullName
    }
};
return true
```

### Disable All Jobs in Folder

```groovy
def jenkins = Jenkins.getInstance()
def folder = jenkins.getItemByFullName("folder_name/subfolder_name")
def jobs =  folder.getAllJobs()

jobs.each { job ->
  job.setDisabled(true)
  println "${job.name} Disable Status: ${job.isDisabled()}"
}
return true
```

### Move Single Item

```groovy
def jenkins = Jenkins.getInstance()
def source = jenkins.getItemByFullName("folder_name/job_or_folder_name")
def destination = jenkins.getItemByFullName("folder_name/subfolder_name")

println "Moving '$source.name' to '$destination.name'"
Items.move(source, destination)
return true
```

### Move All Jobs in Folder

```groovy
def jenkins = Jenkins.getInstance()
def folder = jenkins.getItemByFullName("folder_name/subfolder_name")
def new_folder = jenkins.getItemByFullName("folder_name/subfolder_name")
def jobs =  folder.getAllJobs()

jobs.each { job ->
  println "Moving '$job.name' to '$new_folder.name'"
  Items.move(job, new_folder)
}
return true
```

### Search Folders

From [https://stackoverflow.com/questions/39406546/how-to-move-jenkins-job-to-sub-folder](https://stackoverflow.com/questions/39406546/how-to-move-jenkins-job-to-sub-folder)

```groovy
def FOLDER_NAME = '<An existing destination folder>'
def JOB_REGEX = '<A regex to find your jobs>'

import jenkins.*
import jenkins.model.*
import hudson.*
import hudson.model.*

jenkins = Jenkins.instance

def folder = jenkins.getItemByFullName(FOLDER_NAME)
if (folder == null) {
  println "ERROR: Folder '$FOLDER_NAME' not found"
  return
}

// Find jobs in main folder
def found = jenkins.items.grep { it.name =~ "${JOB_REGEX}" }
println "Searching main folder : $found"

// Find jobs in other subfolders
jenkins.items.grep { it instanceof com.cloudbees.hudson.plugins.folder.Folder }.each { subfolder -> 
  if(!subfolder.getName().equals(FOLDER_NAME))
  {
    println "Searching folder '$subfolder.name'"
    subfolder.getItems().grep { it.name =~ "${JOB_REGEX}" }.each { job ->
      println "Found $job.name"
      found.add(job);
    }
  }
}

// Move them
found.each { job ->
  println "Moving '$job.name' to '$folder.name'"
  Items.move(job, folder)
}
return true
```
