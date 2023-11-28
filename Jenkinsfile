pipeline {
  agent any
  stages {
    stage('Copy Repo from Jenkins to Jmeter') {
      steps {
        sh 'docker cp /$WORKSPACE/ alpine:/opt/github '
      }
    }

    stage('Run Jmeter test') {
      steps {
        sh 'docker exec alpine bash -c "$JMETER -n -t /opt/github/$JOB_NAME/SummaryReport.jmx -l /opt/result/TestResult-$BUILD_NUMBER.csv -e -o /opt/reports/$BUILD_NUMBER -R172.27.0.3"'
      }
    }

    stage('Copy HTML from Jmeter to Jenkins') {
      steps {
        sh 'docker cp alpine:/opt/reports/$BUILD_NUMBER /opt/reports/$BUILD_NUMBER'
      }
    }

  }
  post {
    always {
      publishHTML(reportName: 'HTML Reports', reportDir: '/opt/reports/$BUILD_NUMBER', reportFiles: 'index.html', reportTitles: 'Jmeter-report', keepAll: true, alwaysLinkToLastBuild: true, allowMissing: false)
    }

  }
}