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
        stage('Test'){
            steps{
                sh 'npm test'
            }
        }
        stage('Deployment To Render'){
            steps{
                httpRequest httpMode: 'POST', responseHandle: 'NONE', url: 'https://api.render.com/deploy/srv-cfpo1uo2i3mo4bs53egg?key=7yLWt6KRymc', wrapAsMultipart: false
                echo 'Deployment Successful'
                slackSend channel: 'tyler_ip1', message: "For the ${env.JOB_NAME} build ${env.BUILD_ID}  Site is live at https://galleryip1.onrender.com"
            }
        } 
    }
    post{
        failure{
            emailext to: 'tyler.okelo@student.moringaschool.com',
            subject: "Jenkins build: ${env.JOB_NAME} Failure", 
            body: "The current build ${currentBuild.currentResult} has failed. More Information can be found here: ${env.BUILD_URL}"
        }
    }
}
