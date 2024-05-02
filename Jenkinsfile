// any jenkins pipeline starts with pipeline statement
pipeline {
  // agent specifies where the pipeline will be executed
  agent any
  // stages block contains all the stages in the pipeline
  stages {
    // jenkins stage to clean up the workspace, because when jenkins runs the job it creates a folder
    // better to put in the beginning otherwise if the job fails, the workspace won't be cleaned up
    stage("Clean Up"){
      steps {
        deleteDir() // deletes the workspace
      }
    }
    // stage to clone the repository
    stage("Clone Repo"){
      steps {
        // run bash shell
        sh "git clone https://github.com/jenkins-docs/simple-java-maven-app.git"
      }
    }
    // stage to build
    stage("Build"){
      steps {
        // each steps reverts back to the original workspace
        // change directory to the cloned repository
        // we don't use cd because it's persistent and every step will be inside that directory
        dir("simple-java-maven-app"){
          // the following builds java file and cleans libraries/binaries that may have been created before
          sh "mvn clean package"
        }
      }
    }
    stage("Test"){
      steps {
        dir("simple-java-maven-app"){
          // run tests
          sh "mvn test"
        }
      }
    }
  }
}