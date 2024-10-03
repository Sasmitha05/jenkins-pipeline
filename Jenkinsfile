pipeline {
    agent any
    
    environment {
        NODEJS_HOME = tool name: 'NodeJS', type: 'NodeJSInstallation'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }
    
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-username/ci-cd-sample-app.git'  // Replace this with your repository URL
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh 'npm install'  // Installs the Node.js dependencies
            }
        }
        
        stage('Run Tests') {
            steps {
                echo 'Running Tests...'
                // Replace the echo with your test command, e.g., 'npm test'
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'npm run build'  // Builds the application (if applicable)
            }
        }
        
        stage('Deploy to AWS Ubuntu Server') {
            steps {
                echo 'Deploying application to AWS Ubuntu server...'
               
                // Ensure that Jenkins can SSH into your AWS Ubuntu instance.
                // This will copy your application to the /var/www/myapp directory on your AWS Ubuntu server.
                // Replace "ubuntu" with the correct username, typically "ubuntu" for AWS EC2 Ubuntu AMIs.

                sh '''
                scp -o StrictHostKeyChecking=no -r ./ ubuntu@13.60.243.140:/var/www/myapp
                ssh ubuntu@13.60.243.140 'pm2 restart myapp || pm2 start /var/www/myapp/index.js --name myapp'
                '''
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
