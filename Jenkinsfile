
pipeline {
    agent any
    stages {
        stage("checkout") {
            steps {
            sh "ls"
            git branch:'main', url: 'https://github.com/devopstg76/course3-jenkins-gs-spring-petclinic.git'
            sh "ls"
            }
        }
        stage("build") {
            steps {
                sh "./mvnw package"
            }
        }

        stage("capture") {
            steps {
            archiveArtifacts '**/target/*.jar'
            jacoco()
            junit '**/target/surefire-reports/TEST*.xml'
            }
        }
    }

    post {
        always {
            emailext body: "${env.BUILD_URL}\n${currentBuild.absoluteUrl}",
                to: 'titi@foo.bar',
                recipientProviders: [previous()],
                subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]"
        }
    }
}
