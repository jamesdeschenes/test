pipeline {
    agent { label 'linux'  }
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Virtual Environment') {
            steps {
                sh "pipenv sync"
                sh "pipenv clean"
            }
        }
        stage('Unit Tests') {
            steps {
                sleep 20
                sh "pipenv run python -m pytest --cov --cov-report xml:build/reports/cov.xml --junitxml=build/reports/tests.xml"
                junit 'build/reports/tests.xml'
                cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'build/reports/cov.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
            }
        }
    }
}
