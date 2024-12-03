pipeline {
    agent any

    stages {
        stage('Snyk Open Source Scan - SCA') {
            steps {
                sh 'ls'
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    snykSecurity additionalArguments: '', 
                                 failOnIssues: true, 
                                 failOnError: true, 
                                 monitorProjectOnBuild: true, 
                                 severity: 'critical', 
                                 projectName: '${JOB_NAME}',
                                 snykInstallation: 'snyk@latest', 
                                 snykTokenId: 'snyk-api-token'
                }
            }
        }

        stage('Snyk Code Scan - SAST') {
            steps {
                sh 'ls'
                snykSecurity additionalArguments: '--code', 
                             failOnIssues: false, 
                             failOnError: true, 
                             monitorProjectOnBuild: true, 
                             projectName: '${JOB_NAME}',
                             snykInstallation: 'snyk@latest', 
                             snykTokenId: 'snyk-api-token'
            }
        }
    }
}
