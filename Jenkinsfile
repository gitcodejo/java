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


}

}