node {
    stage('Checkout') {
        // Tambahkan stage checkout
        checkout scm
    }
    docker.image('maven:3.9.6').inside('-u root -v /var/jenkins_home/.m2:/root/.m2') {
        // env.MAVEN_OPTS = '-Dmaven.repo.local=/root/.m2/repository'
        environment {
            JAVA_CREDS = credentials('private-key-aws-java-app')
        }

        stage('Build') {
            // sh 'pwd'
            // sh 'ls -lah'
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Test') {
            sh 'mvn test'
        }
        stage('Manual Approval'){
            input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
        }
        stage("deploy"){
            sh 'echo "Deploying to server"'
            withCredentials([sshUserPrivateKey(credentialsId: 'private-key-aws-java-app', keyFileVariable: 'privateKey')]) {
                sh 'apt-get update && apt-get -y install openssh-client'
                sh 'scp -o StrictHostKeyChecking=no -i $privateKey target/*.jar ubuntu@ec2-18-139-95-243.ap-southeast-1.compute.amazonaws.com:/home/ubuntu/simple-java-maven-app'
                sh 'ssh -o StrictHostKeyChecking=no -i $privateKey ubuntu@ec2-18-139-95-243.ap-southeast-1.compute.amazonaws.com java -jar /home/ubuntu/simple-java-maven-app/*.jar'
                sleep (time: 60, unit: 'SECONDS');
                echo 'Deployed'
            }
            // }
        }

    }
}