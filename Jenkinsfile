node {
    docker.image('maven:3.9.6').inside('-u root --volume jenkins-data:/var/jenkins_home') {
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