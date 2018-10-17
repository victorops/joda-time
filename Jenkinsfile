def executeMaven(buildCommand) {
    withMaven(
        // Maven installation declared in the Jenkins "Global Tool Configuration"
        maven: 'M3',
        // Maven settings.xml file defined with the Jenkins Config File Provider Plugin
        // Maven settings and global settings can also be defined in Jenkins Global Tools Configuration
        mavenSettingsConfig: 'maven-global-settings-xml-96ab007b-1034-4027-a8a5-6e0de13af319',
        mavenLocalRepo: '.repository') {

        ansiColor('xterm') {
            sh "mvn ${buildCommand}"
        }
    }
}

pipeline {
  agent any

  stages {
    stage('Clean') {
        steps {
            executeMaven("clean")
        }
    }
    stage('Compile') {
        steps {
            executeMaven("compile")
        }
    }
    stage('Test') {
        steps {
            executeMaven("test")
        }
    }
    stage('Release') {
        steps {
            executeSbt("deploy")
        }
    }
  }
}
