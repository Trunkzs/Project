pipeline {
  agent any
  stages {
    stage('Copy Repo from Jenkins to Jmeter'){
        steps{
            sh 'docker cp /$WORKSPACE/ jmeter-master:/opt/github '
        }
    }
    stage('Run Jmeter test') {
      steps {
        sh 'docker exec jmeter-master bash -c "$JMETER -n -t /opt/github/$JOB_NAME/SummaryReport.jmx -l /opt/result/TestResult-$BUILD_NUMBER.csv -e -o /opt/reports/$BUILD_NUMBER -R172.27.0.3"'   
    }
    }
    stage('Copy HTML from Jmeter to Jenkins'){
       steps{
        sh 'docker cp jmeter-master:/opt/reports/$BUILD_NUMBER /opt/reports/$BUILD_NUMBER'
        }
    }
 }
 post {
        success {
                slackSend "Build deployed successfully - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
            }
        failure {
                slackSend failOnError:true message:"Build failed  - ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)"
            }
        always {  
            publishHTML target: [
                reportName: 'HTML Reports',
                reportDir: '/opt/reports/$BUILD_NUMBER',
                reportFiles: 'index.html', 
                reportTitles: 'Jmeter-report', 
                keepAll: true,
                alwaysLinkToLastBuild: true,
                allowMissing: false
            ]  
        }
}

}
