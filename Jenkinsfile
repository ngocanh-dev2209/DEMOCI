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
                bat 'dotnet restore WebBanHang.csproj'
            }
        }

        stage('Build') {
            steps {
                echo 'Đang biên dịch ứng dụng (Build Release)...'
                bat 'dotnet build WebBanHang.csproj --configuration Release'
            }
        }

        stage('Test') {
            steps {
                echo 'Đang chạy Unit Test...'
                bat 'dotnet test WebBanHang.csproj --no-restore'
            }
        }
    }

    post {
        success {
            echo 'Quy trình CI đã chạy thành công tất cả các giai đoạn!'
        }
        failure {
            echo 'Quy trình CI thất bại tại bước Build hoặc Test. Dừng quy trình, không triển khai lên IIS.'
        }
    }
}