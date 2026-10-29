pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Restore') {
            steps {
                echo 'Đang khôi phục các NuGet packages...'
                bat 'dotnet restore WebBanHang/WebBanHang.csproj'
            }
        }

        stage('Build') {
            steps {
                echo 'Đang biên dịch ứng dụng (Build Release)...'
                bat 'dotnet build WebBanHang/WebBanHang.csproj --configuration Release --no-restore'
            }
        }

        stage('Test') {
            steps {
                echo 'Đang chạy Unit Test...'
                bat 'dotnet test WebBanHang/WebBanHang.csproj --no-build --configuration Release'
            }
        }
    }
    
    post {
        failure {
            echo 'Quy trình CI thất bại tại bước Build hoặc Test! Dừng quy trình, không triển khai lên IIS.'
        }
    }
}