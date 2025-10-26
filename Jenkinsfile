pipeline {
    agent any

    environment {
        DOTNET_VERSION = '8.0.x'
    }

    triggers {
        pollSCM('* * * * *')
    }

    stages {
        stage('Checkout') {
            when { branch 'main' }
            steps {
                echo 'Извличане на кода от main клона...'
                checkout scm
            }
        }

        stage('Setup .NET') {
            when { branch 'main' }
            steps {
                echo "Проверка на .NET SDK версия"
                sh 'dotnet --version'
            }
        }

        stage('Restore dependencies') {
            when { branch 'main' }
            steps {
                echo 'Възстановяване на зависимости...'
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            when { branch 'main' }
            steps {
                echo 'Билд на приложението...'
                sh 'dotnet build --no-restore'
            }
        }

        stage('Test') {
            when { branch 'main' }
            steps {
                echo 'Изпълнение на всички тестове...'
                sh 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}
