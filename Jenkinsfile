pipeline {


    agent { label 'dotnet' } 

    triggers {
        pollSCM('* * * * *')

    
    }
    // tools {
    //     jdk 'JDK_17'
         
    // }

    stages { 
        stage('vcs') {
            steps {
                git url: 'https://github.com/divyakothuru311/nopcommerce.git',
                    branch: 'master'
            }
                
        }
        stage('build and package') {
           steps {
                rtDotnetResolver (
                    id : "divya",
                    serverId : "jfrogconnection",
                    repo : "nop-nuget-local"
                ) 
                rtDotnetRun (
                    args : "build src/NopCommerce.sln",
                    resolverId : "divya"
                )
                 rtPublishBuildInfo (
                    serverId: "jfrogconnection"
                 )
                 


           }
        }
         stage('results') {
            steps{
                archiveArtifacts artifacts: '**/*.dll'
            }
        }
    }
}