node {
    docker.image('maven:3.9.6').inside('-u root -v jenkins-data:/var/jenkins_home/') {
        stage('Build') {
            sh 'pwd'
            sh 'ls -lah'
            sh 'mvn -B -DskipTests clean package -X'
        }
        stage('Test') {
            sh 'mvn test'
        }
    }
}