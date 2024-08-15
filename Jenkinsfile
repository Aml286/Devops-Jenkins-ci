def COLOR_MAP = [
    'SUCCESS': 'good',
    'FAILURE': 'danger',
]

pipeline {
    agent any

    tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
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
        ARTVERSION = "${env.BUILD_ID}-${env.BUILD_TIMESTAMP}"
        NEXUS_IP = "172.31.30.137"
        NEXUS_PORT = "8081"
        SONARSERVER = "sonarserver"
        SONARSCANNER = "sonarscanner"
    }

    stages {
        stage('BUILD') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('UNIT TEST') {
            steps {
                sh 'mvn -s settings.xml test'
            }
        }

        stage('CODE ANALYSIS WITH CHECKSTYLE') {
            steps {
                sh 'mvn -s settings.xml checkstyle:checkstyle'
            }
            post {
                success {
                    echo 'Generated Analysis Result'
                }
            }
        }

        stage('CODE ANALYSIS with SONARQUBE') {
            environment {
                scannerHome = tool 'SONARSCANNER'
            }

            steps {
                withSonarQubeEnv('sonarserver') {
                    sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                        -Dsonar.projectName=vprofile-repo \
                        -Dsonar.projectVersion=1.0 \
                        -Dsonar.sources=src/ \
                        -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                        -Dsonar.junit.reportsPath=target/surefire-reports/ \
                        -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                        -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
                }
            }
        }

        stage('Sonarqube Quality Gate') {
           steps {
              timeout(time: 1, unit: 'HOURS') {
               waitForQualityGate abortPipeline: true
              }
            }
        }

        stage('Publish to Nexus Repository Manager') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: "${NEXUS_VERSION}",
                    protocol: "${NEXUS_PROTOCOL}",
                    nexusUrl: "${NEXUS_URL}",
                    groupId: "QA",
                    version: "${ARTVERSION}",
                    repository: "${NEXUS_REPOSITORY}",
                    credentialsId: "${NEXUS_CREDENTIAL_ID}",
                    artifacts: [
                        [artifactId: 'vproapp',
                         classifier: '',
                         file: 'target/vprofile-v2.war',
                         type: 'war']
                    ]
                )
            }
        }
    }

    post {
        always {
            echo 'slack notifications'
            slackSend(
                channel: '#jenkinscicd',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\nMore info at: ${env.BUILD_URL}"
            )
        }
    }
}

