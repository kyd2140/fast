pipeline {
    agent any
    
  environment {
        TIME_ZONE = 'Asia/Seoul'
        
        // GitHub 계정정보. 본인껄로 넣으세요!!
        GIT_TARGET_BRANCH = 'main'
        GIT_REPOSITORY_URL = 'https://github.com/kyd2140/fast'
        GIT_CREDENTIONALS_ID = 'git_cre'


        // AWS ECR
        AWS_ECR_CREDENTIAL_ID = 'aws_cre'
        AWS_ECR_URI = '760135347993.dkr.ecr.ap-northeast-2.amazonaws.com'
        AWS_ECR_IMAGE_NAME = 'fast' // 레포지토리이름.
        AWS_REGION = 'ap-northeast-2'
        
    }

    stages {

        stage('1.init') {
            steps {
                echo 'init stage'
                deleteDir()
            }
        }

        stage('2.Cloning Repository') {
            steps {
                echo 'Cloning Repository'
                git branch: "${GIT_TARGET_BRANCH}",
                    credentialsId: "${GIT_CREDENTIONALS_ID}",
                    url: "${GIT_REPOSITORY_URL}"
            }
        }
        
        stage('3.Build Docker Image') {
            steps {
                script {
                    sh '''
                        docker build -t ${AWS_ECR_URI}/${AWS_ECR_IMAGE_NAME}:${BUILD_NUMBER} ./svelte
                        docker build -t ${AWS_ECR_URI}/${AWS_ECR_IMAGE_NAME}:latest ./svelte
                    '''
                }
                // 명령어가 많아질것같아서 스크립트 블록을 추가.
            }
        }

    }
}
