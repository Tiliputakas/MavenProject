pipeline {
    agent any
    
    tools {
        maven 'localMaven'
    }
    
    stages {
        stage ('package - Checkout') {
 	        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/Tiliputakas/MavenProject.git']]]) 
	    }
        
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
            
            post {
                echo 'archive de los artefactos'
                archiveArtifacts artifacs: '**/target/*.war'
            }
        }
        
        stage('Deploy to stagging') {
            steps {
                build jobs: deployStaging
            }
        }
    }
}
