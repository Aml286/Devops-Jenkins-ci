pipeline {
    agent any

    tools {
        maven "MAVEN3"
        jdk   "OracleJDK8"
    }

    environment {
        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "172.31.30.137:8081"
        NEXUS_USER = "admin"
        SNAP_REPO = "vprofile-snapshot"
        NEXUS_GRP_REPO = "vpro-maven-group"
        NEXUS_REPOSITORY = "vprofile-release"
        NEXUS_REPO_ID = "vprofile-release"
        NEXUS_CREDENTIAL_ID = "nexuslogin"
        ARTVERSION = "${env.BUILD_ID}"
    }

    stages {
        stage('BUILD') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }
    }

    post {
        success {
            echo 'Now Archiving...'
            archiveArtifacts artifacts: '**/target/*.war'
        }
    }
}

