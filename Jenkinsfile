pipeline {
    agent any
    tools {
        maven 'maven3'
        jdk 'java17'
    }
    stages {
        
        stage('Download') {
            steps {
                echo 'Downloading from Git..'
                git branch: 'main', url: 'https://github.com/darjikhushi/maven-jenkins6.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Building war file..'
                sh 'mvn clean package'
            }
        }
        stage('Archive Artifacts') {
            steps {
                echo 'Archiving Arifacts....'
                archiveArtifacts artifacts: '**/*.war', followSymlinks: false

            }
        }
        stage('Call project ') {
            steps {
                echo 'Pulling deploy project....'
                build wait: false, job: 'pipeline-deploy-java'
            }
        }
    }
}
