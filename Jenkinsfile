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
            // withCredentials([sshUserPrivateKey(credentialsId: 'private-key-aws-java-app', keyFileVariable: 'privateKey')]) {
                // sh 'echo $privateKey > key.pem'
                // sh 'cat key.pem'
                // sh 'chmod 600 key.pem'
                // sh 'scp -o StrictHostKeyChecking=no -i key.pem target/*.jar ec2-user@ec2-3-1-84-79.ap-southeast-1.compute.amazonaws.com:/home/ec2-user/ismple-java-maven-app'
                // sh 'ssh -o StrictHostKeyChecking=no -i key.pem ec2-user ec2-user@ec2-3-1-84-79.ap-southeast-1.compute.amazonaws.com java -jar /home/ec2-user/simple-java-maven-app/*.jar'
                // sleep (time: 60, unit: 'SECONDS');
                // sh 'rm -rf key.pem'
                // echo 'Deployed'
                // sh "echo $privateKey"
                sh 'apt-get update && apt-get -y install openssh-client'
                //SCP to server deployment
                sh 'scp -i ${JAVA_CREDS_KEY} target/*.jar ec2-user@ec2-3-1-84-79.ap-southeast-1.compute.amazonaws.com:/home/ec2-user/simple-java-maven-app'

                //SSH to server deployment
                sh 'ssh -o StrictHostKeyChecking=no -i ${JAVA_CREDS_KEY}  ec2-user@ec2-3-1-84-79.ap-southeast-1.compute.amazonaws.com java -jar /home/ec2-user/simple-java-maven-app/*.jar'

                // sh 'scp -o StrictHostKeyChecking=no -i ${JAVA_CREDS_KEY} target/*.jar ec2-user@ec2-3-1-84-79.ap-southeast-1.compute.amazonaws.com:/home/ec2-user/simple-java-maven-app'
                // sh 'ssh -o StrictHostKeyChecking=no -i ${JAVA_CREDS_KEY}  ec2-user@ec2-3-1-84-79.ap-southeast-1.compute.amazonaws.com java -jar /home/ec2-user/simple-java-maven-app/*.jar'
                sleep (time: 60, unit: 'SECONDS');
                echo 'Deployed'
            // }
        }

    }
}