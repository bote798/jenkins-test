pipeline {
    agent any

    stages {
        stage('Pull Code') {
            steps {
                echo 'Code pulled from GitHub'
            }
        }

        stage('Setup Python Environment') {
            steps {
                sh '''
                    # 检查并安装 python3-pip（如果缺失）
                    if ! command -v pip3 > /dev/null 2>&1; then
                        echo "pip3 not found, installing..."
                        sudo apt update
                        sudo apt install python3-pip -y
                    else
                        echo "pip3 already installed"
                    fi

                    # 创建虚拟环境（如果不存在）
                    if [ ! -d "venv" ]; then
                        echo "Creating Python virtual environment..."
                        python3 -m venv venv
                    else
                        echo "Virtual environment already exists"
                    fi

                    # 激活虚拟环境并升级 pip
                    . venv/bin/activate
                    pip install --upgrade pip

                    # 安装项目依赖
                    if [ -f "requirements.txt" ]; then
                        echo "Installing dependencies from requirements.txt"
                        pip install -r requirements.txt
                    else
                        echo "No requirements.txt found, skipping dependency installation"
                    fi
                '''
            }
        }

        stage('Test Run') {
            steps {
                sh '''
                    # 激活虚拟环境并运行程序
                    . venv/bin/activate
                    python3 app.py
                '''
            }
        }

        stage('Success Message') {
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
