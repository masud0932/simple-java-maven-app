pipeline {
    agent any
    
    tools {
      maven 'mymaven'
    }

    parameters {
      choice choices: ['dev', 'prod'], name: 'select_environment'
 }


    stages {
        stage('Checkout Code') {
            agent { label 'Built-In Node' }  // Runs on Master
            steps {
                echo "Checking out code on master node..."
                checkout scm
            }
        }

        stage('Build on Slave') {
            agent { label 'DevServer' }  // Runs on a specific slave
            steps {
                echo "Building the project on slave node..."
                sh 'mvn clean install'
            }
        }

        stage('Test on Another Slave') {
            agent { label 'ProdServer' }  // Runs on a different slave
            steps {
                echo "Running tests on a dedicated test slave..."
                sh 'mvn test'
            }
        }

        stage('Deploy on Master') {
            agent { label 'Built-In Node' }  // Runs on Master
            steps {
                echo "Deploying application from master..."
                sh 'mvn deploy'
            }
        }
    }
}
