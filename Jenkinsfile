pipeline {
    agent { label 'linux'  }
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Virtual Environment') {
            steps {
                sh "virtualenv --no-site-packages my_env"

                sh """#!/usr/bin/env bash
                source my_env/bin/activate
                pip install -r requirements.txt
                """
            }
        }
        stage('Unit Tests') {
            steps {
                sleep 20
                sh """#!/usr/bin/env bash
                source my_env/bin/activate
                python -m pytest --junitxml=build/reports/unittests.xml test
                """
                junit 'build/reports/**/*.xml'
            }
        }
    }
}
