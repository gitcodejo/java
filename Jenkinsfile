pipeline {

agent any

stages {

stage('Git checkout') {

steps {

 git 'https://github.com/gitcodejo/java.git'

}

}

stage('unit testing') {

steps {

 sh 'mvn test'

}

}


stage('integration testing') {

steps {

 sh 'mvn verify -DskipUnitTests'

}

}

stage('maavan build') {

steps {

sh 'mvn clean install'

}

}

stage('static code analysis') {

steps {
    script{
      withSonarQubeEnv(credentialsId: 'sonar-api') {
        sh 'mvn clean package sonar:sonar'
}


}

}
}

stage('Quality Gate Status') {

steps {

  script{

    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'

  }

}

}

stage('nexus repo creation') {

steps {

script {
def readPomVer = readMavenPom file: 'pom.xml'
nexusArtifactUploader artifacts: 

    [
         [artifactId: 'springboot', 
         classifier: '', 
         file: 'target/Uber.jar', 
         type: 'jar'
         ]
    ], 
         credentialsId: 'nexuspass', 
         groupId: 'com.example', 
         nexusUrl: '15.206.185.162:8081', 
         nexusVersion: 'nexus3', 
         protocol: 'http', 
         repository: 'demoapp-relaease', 
         version: "${readPomVer.version}"

    
}

}

}

}

}