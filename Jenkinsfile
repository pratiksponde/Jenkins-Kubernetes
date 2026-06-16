pipeline {

    agent {

        label 'Node1'
    }
    stages{
        stage('Trivy FS Scan'){
            steps{
                sh 'trivy fs --exit-code 1 --severity HIGH,CRITICAL .'
            }
        }
    }
}
