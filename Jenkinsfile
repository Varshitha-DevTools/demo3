pipeline {
    agent any

    stages {
        stage('Download Archive') {
            steps {
                sh '''
                    curl -o sample.zip https://github.com/junit-team/junit5-samples/archive/refs/heads/main.zip
                    unzip -o sample.zip -d extracted
                '''
            }
        }

        stage('Simulate Test Results') {
            steps {
                sh '''
                    mkdir -p extracted/test-results
                    cat <<EOF > extracted/test-results/sample.xml
                    <testsuite tests="1">
                      <testcase classname="demo.SampleTest" name="testExample"/>
                    </testsuite>
                    EOF
                '''
            }
        }

        stage('Archive Test Results') {
            steps {
                junit 'extracted/test-results/*.xml'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
