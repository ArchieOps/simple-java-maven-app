node {
    docker.image('maven:3.9.6').inside('-u root -v /root/.m2:/root/.m2') {
        stage('Build') {
            sh 'pwd'
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Test') {
            sh 'mvn test'
        }
    }
}