// 需要在jenkins的Credentials设置中配置jenkins-harbor-creds、jenkins-k8s-config参数
//  git describe --tags展示当前分支的最近的tag
// cut -d: -f 1 /etc/passwd > /tmp/users 
//   -d用来定义分隔符，默认为tab键，-f表示需要取得哪个字段
pipeline {
    agent any
    environment {
            HARBOR_CREDS = credentials('jenkins-harbor-creds')
            GIT_TAG = sh(returnStdout: true,script: 'git describe --tags').trim()
     }
    parameters {
        string(name: 'HARBOR_HOST', defaultValue: '10.88.210.155', description: 'harbor仓库地址')
        string(name: 'DOCKER_IMAGE', defaultValue: 'tssp/pipeline-demo', description: 'docker镜像名')
        string(name: 'APP_NAME', defaultValue: 'pipeline-demo', description: 'k8s中标签名')
    }
    stages {
        stage('Maven Build 构建。。') {
            when { expression { env.GIT_TAG != null } }
            steps {
                echo 'maven build 。。。。。start'
                sh 'mvn clean package -Dfile.encoding=UTF-8 -DskipTests=true'
                stash includes: 'target/*.jar', name: 'app'
                echo 'MAVEN build.......。。。。end'
            }
        }
        stage('Docker Build 构建。。。。。') {
            when {
                 allOf {
                       expression { env.GIT_TAG != null }
                   }
             }
            steps {
                  echo 'maven build 。。。。。start'
            }
         }

          stage('depley  构建。。。。。') {
              when {
                   allOf {
                         expression { env.GIT_TAG != null }
                     }
               }
                steps {
                      echo 'maven build 。。。。。start'
                }
          }

    }


}
