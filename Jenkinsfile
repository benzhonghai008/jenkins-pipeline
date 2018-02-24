pipeline {
    agent {
        label 'salve'
    }

    stages {

        stages ('Checkout') {
            steps {
                // checkout code from gitlab repository
                checkout([$class: 'GitSCM', branches: [[name: '$gitbranch']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'gitlab', name: 'origin', refspec: '+refs/heads/*:refs/remotes/origin/*', url: 'http://pangu.bldz.com:10081/business-service/mall-basic-soa.git']]])


            }
        }
        stage ('Build') {
            steps {
                sh 'mvn clean package -Dmaven.test.skip=true' 
            }
         
        }
        stage ('test') {
            steps {
                echo 'mvn test'
            }
            post {
                success {
                    echo 'target/surefire-reports/test.xml'
                }
            }
        }

    }

}
