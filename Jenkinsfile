pipeline {
    agent any
    environment {
        BUILDBEN_HOST_URL = 'http://axxxxx531ff9a194eggfg4566-4556677.eu-central-1.elb.amazonaws.com:8080'
        BUILDBEN_S3_REGION = 'eu-central-1'
        BUILDBEN_S3_BUCKET_NAME = 'buildben-repo'
        BUILDBEN_S3_ACCESS_KEY_ID = 'buildben'
        BUILDBEN_S3_SECRET_ACCESS_KEY = 'buildben'
        BUILDBEN_MINIO_URL = 'http://44hfmdm123412csdfsdfsdsd-0090901.eu-central-1.elb.amazonaws.com:9000'
    }
    stages {
        stage('clean env') {
            steps {
                sh 'sudo rm -rf *'
            }
        }
        stage('checkout scm') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: BRANCH]], extensions: [], userRemoteConfigs: [[url: 'https://github.com/xxx/yyy.git']]])
            }
        }
        stage('download buildben') {
            steps {
                sh 'curl https://buildben-repo.s3.eu-central-1.amazonaws.com/agent -o buildben'
                sh 'chmod +x buildben'
            }
        }
   stage('test compile') {
            steps {
                sh './buildben mvn test-compile -B --errors -Dbuild.number=null -DskipTests=true --settings=settings.xml'
           }
        }
        stage('run tests') {
            steps {
                sh './buildben mvn surefire:test --settings=settings.xml'
            }
        }
    }
}
