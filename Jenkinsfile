pipeline {
    agent { docker { image 'ruby:alpine' } }
	
    stages {
        stage('build') {
            steps {
                sh apk add --no-cache git
                // install required bundles
                sh 'bundle install'
                // build and run tests with coverage
                sh 'bundle exec rake build spec'
                // Archive the built artifacts
                archive (includes: 'pkg/*.gem')

                    // publish html
                publishHTML ([
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: 'coverage',
                    reportFiles: 'index.html',
                    reportName: "RCov Report"
                ])
            }
        }
    }
}
