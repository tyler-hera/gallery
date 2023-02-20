pipeline{
    agent any
    tools{
            nodejs "NodeJS with npm"
    }
    stages{
        stage('Clone Repository'){
            steps{
                git 'https://github.com/tyler-hera/gallery'
            }
        }
        stage('Software Checkup'){
            steps{
                sh 'npm install'
            }
        }
        stage('Building Phase'){
            steps{
                sh 'node server.js'
            }
        }
        stage('Testing Phase'){
            steps{
                sh 'npm test'
            }
        }
        stage('Deploying To Render'){
            steps{
                httpRequest httpMode: 'POST', responseHandle: 'NONE', url: 'https://api.render.com/deploy/srv-cfpo1uo2i3mo4bs53egg?key=7yLWt6KRymc', wrapAsMultipart: false
                echo 'Deployment Successful'
            }
    }
    post{
        failure{
            emailext to: 'tyler.okelo@student.moringaschool.com',
                subject: 'Jenkins build:${currentBuild.currentResult}: ${env.JOB_NAME} Failure', 
                body: '${currentBuild.currentResult}: Job ${env.JOB_NAME} has and failed more Info can be found here: ${env.BUILD_URL}', 
        }
    }
}
