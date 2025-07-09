pipeline {
    agent any

    stages {
        stage('Download Archive') {
            steps {
                // Public sample .zip file with a JUnit XML report
                sh 'curl -L -o sample-tests.zip https://github.com/junit-team/junit5-samples/archive/refs/heads/main.zip'
            }
        }

        stage('Extract Archive') {
            steps {
                sh 'unzip -o sample-tests.zip -d extracted'
            }
        }

        stage('Simulate Test Results') {
            steps {
                // Create a dummy JUnit test result file for demo
                sh '''
                mkdir -p extracted/test-results
                cat <<EOF > extracted/test-results/sample.xml
                <testsuite tests="1">
                  <testcase classname="dummy.Class" name="testSuccess"/>
                </testsuite>
                EOF
                '''
            }
        }

        stage('Publish JUnit Results') {
            steps {
                junit 'extracted/test-results/*.xml'
            }
        }
    }
}
