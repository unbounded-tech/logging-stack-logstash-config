pipeline {
  agent {
    label "prod"
  }
  stages {
    stage("create") {
      when {
        branch "master"
      }
      steps {
        sh "docker config create logstash.conf logstash.conf"
      }
    }
  }
  post {
    always {
      sh "docker system prune -f"
    }
    failure {
      slackSend(
        color: "danger",
        message: "${env.JOB_NAME} failed: ${env.RUN_DISPLAY_URL}"
      )
    }
    success {
      slackSend(
        color: "good",
        message: "${env.JOB_NAME} succeeded: ${env.RUN_DISPLAY_URL}"
      )
    }
  }
}