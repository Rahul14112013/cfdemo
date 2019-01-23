pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
       
        stage('Deploy - AWS') {
            steps {
                echo 'Deploying to AWS'
                pushToCloudFoundry(
                target: 'api.sys.pcf-demo.acarrigandemo.com',
                organization: 'Demo',
                cloudSpace: 'production',
                credentialsId: 'bbdeb748-1fea-4787-9ee0-033a83f5cab5',
                selfSigned: 'true',
                manifestChoice: [
                  appName: 'cfdemo',
                  appPath: 'target/gs-sts-cloud-foundry-deployment-0.1.0.jar',
                  instances: '1', 
                  memory: '1024',   
                  value: 'jenkinsConfig'
                ]
                )
            }
        }
        stage('Deploy - Azure') {
            steps {
                echo 'Deploying to Azure'
                pushToCloudFoundry(
                target: 'api.sys.west.azure.pcfninja.com',
                organization: 'Demo',
                cloudSpace: 'production',
                credentialsId: 'bd3443b3-9405-4584-9769-7eb9050fb244',
                selfSigned: 'true',
                manifestChoice: [
                  appName: 'cfdemo',
                  appPath: 'target/gs-sts-cloud-foundry-deployment-0.1.0.jar',
                  instances: '1', 
                  memory: '1024',
                  value: 'jenkinsConfig'
                ]
                )
            }
        }
    }
}
