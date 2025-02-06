node {
    docker.image('maven:3.9.6').inside('-u root -v /var/jenkins_home:jenkins-data') {
        stage('Build') {
            sh 'pwd'
            sh 'ls -lah'
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Test') {
            sh 'mvn test'
        }
    }
}