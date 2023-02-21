pipeline{
    agent any
    tools{
            nodejs "NodeJS with npm"
    }
    stages{
        stage('Cloning Repository'){
            steps{
                git 'https://github.com/tyler-hera/gallery'
            }
        }
        stage('Software Check'){
            steps{
                sh 'npm install'
            }
        }
        stage('Build'){
             steps{
                 sh 'node server.js'
            }
        }
        stage('Deployment To Render'){
            steps{
                httpRequest httpMode: 'POST', responseHandle: 'NONE', url: 'https://api.render.com/deploy/srv-cfpo1uo2i3mo4bs53egg?key=7yLWt6KRymc', wrapAsMultipart: false
                echo 'Deployment To Render Successful'

            }
        }
    }
}
