node {
    docker.image('maven:3.9.6').inside('-u root -v jenkins-data:/var/jenkins_home ') {
        stage('Build') {
            sh 'mvn -B -DskipTests clean package -X'
        }
        stage('Test') {
            checkout scm
            sh 'mvn test'
            junit 'target/surefire-reports/*.xml'
        }
    }
}