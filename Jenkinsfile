//Test cronjob build
node {
    docker.image('maven:3.9.2').inside('-u root -v /root/.m2:/root/.m2') {
        stage('Build') {
            sh 'cd ..'
            sh 'mvn -B -DskipTests clean package'
        }
        stage('Test') {
            sh 'cd ..'
            checkout scm
            sh 'mvn test'
            junit 'target/surefire-reports/*.xml'
        }
    }
}