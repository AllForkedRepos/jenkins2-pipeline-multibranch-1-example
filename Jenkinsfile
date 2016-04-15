#!groovy



properties([
    [$class: 'BuildDiscarderProperty', strategy: [$class: 'LogRotator', artifactDaysToKeepStr: '', artifactNumToKeepStr: '1', daysToKeepStr: '', numToKeepStr: '']]
  ])

node {
    wrap([$class: 'TimestamperBuildWrapper']) {

        stage 'Workspace'

        pwd()
        echo 'Cleaning...'
        deleteDir()

        stage 'Source'

        echo 'Retrieving source...'
        checkout scm


        stage 'Setup'
 
        echo 'Setting environment...'
 

        stage 'Dependencies'

        echo 'Retrieving dependencies...'
        bat ''' if not exist deps mkdir deps '''
        bat ''' echo some-dependency-content-perhaps-binary-somedep-1220 > deps\\somedep-1.22.0.dep.txt '''
        bat ''' echo some-dependency-content-perhaps-binary-otherdep-421132 > deps\\otherdep-4.2.113-2.dep.txt '''
        bat ''' time /t && ping 127.0.0.1 -n 6 -w 10 2>nul >nul && time /t '''


        stage 'Fingerperinting'

        echo 'Fingerprinting dependencies...'
        step([$class: 'ArtifactArchiver', artifacts: 'deps/**/*', fingerprint: true])


        stage 'Build'

        echo 'Building...'
        timeout(time: 30, unit: 'SECONDS') {
            bat ''' for /L %%i in (1, 1, 4) do ( echo "Compile file %%i" && ping 127.0.0.1 -n %%i -w 10 ) '''
        }


        stage 'Unit tests'

        echo 'Performing unit tests...'


        stage 'Pack'

        echo 'Packaging...'


        stage 'Extended tests'

        echo 'Performing extended testing...'


        stage 'Artifact'

        echo 'Storing build artifacts...'

    }
}