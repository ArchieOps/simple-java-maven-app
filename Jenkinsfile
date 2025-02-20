node {
    stage('Checkout') {
        // Tambahkan stage checkout
        checkout scm
    }
    docker.image('maven:3.9.6').inside('-u root -v /var/jenkins_home/.m2:/root/.m2') {
        // env.MAVEN_OPTS = '-Dmaven.repo.local=/root/.m2/repository'
        stage('Build') {
            // sh 'pwd'
            // sh 'ls -lah'
            sh 'mvn -B -DskipTests clean package'
            withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'PASS', usernameVariable: 'USER')]){
                sh 'docker build -t archieops/my-private-repo .'
                sh "echo $PASS | docker login -u $USER --password-stdin"
                sh 'docker push archieops/my-private-repo'
            }
        }
        stage('Test') {
            sh 'mvn test'
        }
        stage('Manual Approval'){
            input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
        }
        stage("deploy"){
            sh './jenkins/scripts/deliver.sh'
            sleep time:1, unit:"MINUTES"
            echo 'Pipeline Succesfully Finished'
        }
    }
}