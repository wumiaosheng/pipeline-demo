// 需要在jenkins的Credentials设置中配置jenkins-harbor-creds、jenkins-k8s-config参数
//  git describe --tags展示当前分支的最近的tag
// cut -d: -f 1 /etc/passwd > /tmp/users 
//   -d用来定义分隔符，默认为tab键，-f表示需要取得哪个字段
pipeline {
    agent any
    environment {
        HARBOR_CREDS = credentials('jenkins-harbor-creds')
        // K8S_CONFIG = credentials('jenkins-k8s-config')
        GIT_TAG = sh(returnStdout: true,script: 'git describe --tags').trim()
    }
    parameters {
        string(name: 'HARBOR_HOST', defaultValue: '10.8.255.249', description: 'harbor仓库地址')
        string(name: 'DOCKER_IMAGE', defaultValue: 'tssp/pipeline-demo', description: 'docker镜像名')
        string(name: 'APP_NAME', defaultValue: 'pipeline-demo', description: 'k8s中标签名')
        string(name: 'K8S_NAMESPACE', defaultValue: 'demo', description: 'k8s的namespace名称')
    }
    stages {
        stage('Maven Build') {
            print("maven build 。。。。。start")
            when { expression { env.GIT_TAG != null } }
            agent {
                docker {
                    image 'maven:3-jdk-8-alpine'
                    args '-v $HOME/.m2:/root/.m2'
                }
            }
            steps {
                sh 'mvn clean package -Dfile.encoding=UTF-8 -DskipTests=true'
                stash includes: 'target/*.jar', name: 'app'
            }

             print("maven build 。。。。。end")

        }
    }
}
