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
                    archiveArtifacts artifacts: 'build/**' // 将构建输出的'build'目录作为工件保存
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy'
                sshagent(credentials: ['jenkins']) {
                    echo 'Logining ==========================Deploy Source'
                    sh 'ssh lyx@192.168.227.128 "ls -l /"'
                }
            }
        }
    }
}
