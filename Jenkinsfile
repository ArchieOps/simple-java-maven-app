//Test cronjob build
node {
    docker.image('maven:3.9.2').inside('-u root -v /root/.m2:/root/.m2') {
        stage('Build') {
            sh 'ls -la'
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Test') {
            checkout scm
            sh 'mvn test'
            junit 'target/surefire-reports/*.xml'
        }
    }
}