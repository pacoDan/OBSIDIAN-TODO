-
```Jenkinsfile
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-repo/spring-boot-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                // Deploy to Tomcat
                deployToTomcat()
            }
        }
    }

    post {
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}

def deployToTomcat() {
    // Add your deployment logic here, e.g., using SCP or the Deploy to Container plugin
    sh 'scp target/your-app.jar user@your-tomcat-server:/path/to/deploy'
}
```

