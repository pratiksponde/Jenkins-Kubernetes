pipeline {
    agent {
        label 'Node1'
    }
    tools{
        maven 'Maven'
    }
    environment {
        SONAR_IP = '100.53.3.163'
    }
    stages{
        stage('Trivy FS Scan'){
            steps{
                sh 'trivy fs --exit-code 1 --severity HIGH,CRITICAL .'
                }
            }
        stage('Build And Sonar'){
            steps{
                withCredentials([string(credentialsId: 'Sonar-Token', variable: 'SONAR_TOKEN')]) {
                    sh ''' mvn clean verify sonar:sonar \
                    -Dsonar.projectKey=Project1 \
                    -Dsonar.host.url="http://${SONAR_IP}:9000" \
                    -Dsonar.token="${SONAR_TOKEN}" \
                    -Dsonar.qualitygate.wait=true
                    ''' 
                }
            }
       
        }
    } 
}
