node {
    docker.image('maven:3.9.6').inside('-u root -v /var/jenkins_home/.m2:/root/.m2') {
        stage('Checkout') {
            // Tambahkan stage checkout
            checkout scm
        }
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