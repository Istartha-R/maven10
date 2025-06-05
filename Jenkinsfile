pipeline {
    agent any

    environment {
        LANG = 'en_US.UTF-8'
        LC_ALL = 'en_US.UTF-8'
    }

    tools {
        maven 'maven'
        jdk 'jdk'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Istartha-R/maven10.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/MavenAnsibleWebApp.war', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    export LANG=en_US.UTF-8
                    export LC_ALL=en_US.UTF-8
                    ansible-playbook direct/playbook.yml -i direct/hosts.ini
                '''
            }
        }
    }
}
