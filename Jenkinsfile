node {
  try{
    stage 'checkout project'
    checkout scm

    stage 'check env'
    sh "mvn -v"
    sh "java -version"

    stage 'test'
    sh "mvn test"

    stage 'package'
    sh "mvn package"

    stage 'Artifact'
    step([$class: 'ArtifactArchiver', artifacts: '**/target/*.jar', fingerprint: true])

    stage('Deploy') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' (1)
              }
            }
            steps {
                sh 'make publish'
            }
        }
    }

  }catch(e){
    throw e;
  }
}
