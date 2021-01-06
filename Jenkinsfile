pipeline {
    agent any

    stages{
		stage('Checkout'){
			steps {
			checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'dheerajgit', url: 'https://github.com/djg2018/jenkins-static-s3-deploy.git']]])
			}
		}
        stage('deploy to S3'){
            steps{
                bat 'aws s3 cp public/index.html s3://jenkinstoawsdeployment'
                bat 'aws s3api put-object-acl --bucket jenkinstoawsdeployment --key index.html --acl public-read'
                bat 'aws s3 cp public/error.html s3://jenkinstoawsdeployment'
                bat 'aws s3api put-object-acl --bucket jenkinstoawsdeployment --key error.html --acl public-read'
            }
        }
    }
    post{
        always{
            cleanWs disableDeferredWipeout: true, deleteDirs: true
        }
    }

}
