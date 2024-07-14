pipeline {
    agent any
    tools { nodejs 'nodejs:latest' } // 假设你已经配置了Node.js工具别名

    stages {
        stage('Prepare') {
            steps {
                echo 'Preparing environment'
                withEnv(["PATH+NODEJS=${tool 'nodejs:latest'}"]) {
                    sh 'npm install' // 或使用 'npm install' 如果你没有package-lock.json或yarn.lock
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building React application'
                withEnv(["PATH+NODEJS=${tool 'nodejs:latest'}"]) {
                    sh 'npm run build'
                }
            }
            post {
                success {
                    archiveArtifacts artifacts: 'dist/**' // 将构建输出的'build'目录作为工件保存
                }
            }
        }
    }
    post {
        always {
            // cleanWs() // 清理工作空间，可选，根据实际情况决定是否需要
        }
    }
}
