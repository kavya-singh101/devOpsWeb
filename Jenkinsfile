pipeline{
    agent any
    tools{
        maven 'local_maven'
    }

    stage('Build'){
        steps{
            sh 'mvn clean package'
        }
        post{
            success{
                echo "Archiving the artifacts"
                archiveArtifacts artifacts: '**/target/*.war'
            }
        }
    }
    stage('Deploy to tomcat'){
        steps{
            deploy adapters: [tomcat9(credentialsId: 'kavya', path: '', url: 'http://15.206.151.1:8080')], contextPath: null, war: '**/*.war'
        }
    }
}
