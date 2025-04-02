pipeline {
    agent none  // Define agents per stage

    tools {
        maven 'mymaven'
    }

    stages {
        stage('Build on Dev Server') {
            agent { label 'DevServer' }  // Run on Development Slave
            steps {
                echo "Building project on DevServer..."
                sh 'mvn clean install'
            }
        }

        stage('Test on Dev Server') {
            agent { label 'DevServer' }  // Run tests on Development Slave
            steps {
                echo "Running tests on DevServer..."
                sh 'mvn test'
            }
        }

        stage('Deploy on Production Server') {
            agent { label 'ProdServer' }  // Run on Production Slave
            steps {
                echo "Deploying application on ProdServer..."
                sh 'mvn deploy'
            }
        }
    }
}
