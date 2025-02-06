node {
    stage('Checkout') {
        // Tambahkan stage checkout
        checkout scm
    }
    docker.image('maven:3.9.6').inside('-u root -v /var/jenkins_home/.m2:/root/.m2') {
        env.MAVEN_OPTS = '-Dmaven.repo.local=/root/.m2/repository'
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