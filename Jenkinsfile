pipeline {
    agent any
    tools { nodejs 'nodejs:latest' } // 使用别名 'nodejs:latest' 指定Node.js版本22.4.1

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                withEnv(["PATH+NODEJS=${tool 'nodejs:latest'}"]) {
                    sh 'node -v'
                }
            }
        }
    }
}
