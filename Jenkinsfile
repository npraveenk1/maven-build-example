#!/usr/bin/env groovy

pipeline {
    agent any
    stages {
        stage('Pre Build') {
            def causes = currentBuild.rawBuild.getCauses()
            def specificCause = currentBuild.rawBuild.getCause(hudson.model.Cause$UserIdCause)
            sh 'echo "Hello World" : ${specificCause} '
        }
        stage('Build') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
         stage "Create build output"
            // Make the output directory.
            sh "mkdir -p output"

            // Write an useful file, which is needed to be archived.
            writeFile file: "output/usefulfile.txt", text: "This file is useful, need to archive it."

            // Write an useless file, which is not needed to be archived.
            writeFile file: "output/uselessfile.md", text: "This file is useless, no need to archive it."

           stage "Archive build output"
    
            // Archive the build output artifacts.
            archiveArtifacts artifacts: 'output/*.txt', excludes: 'output/*.md'
            
        }
    }
}
