pipeline {
    agent any                       // 在任意可用代理上运行

    stages {
        stage('Pull Code') {        // 阶段1：拉取代码（Jenkins 自动完成）
            steps {
                echo 'Code pulled from GitHub'
            }
        }

        stage('Install Dependencies') {   // 阶段2：安装依赖
            steps {
                sh 'python3 -m pip install --user -r requirements.txt'
            }
        }

        stage('Test Run') {               // 阶段3：运行程序
            steps {
                sh 'python3 app.py'
            }
        }

        stage('Success Message') {        // 阶段4：成功提示
            steps {
                echo 'Pipeline executed successfully!'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Build succeeded! 🎉'
        }
        failure {
            echo 'Build failed. Please check the logs.'
        }
    }
}
