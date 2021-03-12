pipeline {
  agent {
    label "linux-slave"
  }
  triggers {
    githubPush()
  }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
