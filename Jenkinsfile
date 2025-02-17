pipeline{
    agent any;
    environment{
        BUCKET = 'utkarsh-22122-bucket'
        PATTERN = 'build/*'
    }

    tools {nodejs 'node'} 

    stages{
        stage('Initialize'){
            steps {
                sh '''
                    npm install
                '''
            }
        }

        stage('Unit Tests') {
            steps {
                sh '''
                    npm run test -- --watchAll=false
                '''
            }
        }

        stage('Build') {
            steps {
                sh '''
                    npm run build
                '''
            }
        }

        stage('Upload to s3 bucket'){
            steps{
                    s3Upload consoleLogLevel: 'INFO',
                    dontSetBuildResultOnFailure: false, 
                    dontWaitForConcurrentBuildCompletion: false, 
                    entries: [
                            [bucket: '22122-utkarsh-bucket',
                            excludedFile: '',
                            flatten: false, 
                            gzipFiles: false, 
                            keepForever: false, 
                            managedArtifacts: false, 
                            noUploadOnFailure: false, 
                            selectedRegion: 'us-east-1', 
                            showDirectlyInBrowser: false, 
                            sourceFile: ' build/*', 
                            storageClass: 'STANDARD', 
                            uploadFromSlave: false, 
                            useServerSideEncryption: false]], 
                            pluginFailureResultConstraint: 'FAILURE', 
                            profileName: '22122-utkarsh-jenkins', 
                            userMetadata: [[key: 'Name', value: '22122-utkarsh-bucket']]
                }
        }
    }
}
