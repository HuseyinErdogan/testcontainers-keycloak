def pod =
"""
apiVersion: v1
kind: Pod
metadata:
  labels:
    name: worker
spec:
  serviceAccountName: jenkins
  containers:
    - name: gradle
      image: gradle:7.2.0-jdk17
      resources:
        limits:
          memory: "750Mi"
        requests:
          cpu: "250m"
          memory: "750Mi"
      imagePullPolicy: Always
      tty: true
      command: ["cat"]
"""

pipeline {
    agent {
        kubernetes {
            yaml pod
        }
    }
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Test') {
            steps {
                container('gradle') {
                    script {
                        sh "java --version"
                        sh "gradle --version"
                    }
                }
            }
        }
    }
}
