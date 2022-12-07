pipeline {
    agent any
    environment {
      PROJECT_NAME = "Apache2"
      OWNER_NAME   = "Oleksii Bozhchenko"
    }

    stages {
        stage('Stage1-Install') {
            steps {
                echo "===== Start of Stage Build ====="
                sh '''
                sudo apt update
                sudo apt -y install apache2
                sudo systemctl enable apache2
                sudo systemctl restart apache2
                '''
                echo "===== End of Stage Build ====="
            }
        }
        stage('Stage2-Test') {
            steps {
                echo "===== Start of Stage Test ====="
                sh '''
                sudo systemctl status apache2 | grep "(running)"
                curl -s --head  --request GET localhost > null
                sudo cat /var/log/apache2/access.log | grep "[^4-5][0-9][0-9]" > null
                '''
                echo "===== End of Stage Test ====="
            }
        }
        stage('Stage3-Conclusion') {
            steps {
                echo "Installation project ${PROJECT_NAME} finished"
                echo "Owner is ${OWNER_NAME}"
            }
        }	
    }
}
