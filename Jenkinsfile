// 需要在jenkins的Credentials设置中配置jenkins-harbor-creds、jenkins-k8s-config参数
//  git describe --tags展示当前分支的最近的tag
// cut -d: -f 1 /etc/passwd > /tmp/users 
//   -d用来定义分隔符，默认为tab键，-f表示需要取得哪个字段
pipeline {
    agent { label 'jnpl_docker_java' }

    stages {

        stage('Docker Build 构建。。。。。') {

            steps {
                  echo 'maven build 。。。。。start'
            }
         }

          stage('depley  构建。。。。。') {

                steps {
                      echo 'maven build 。。。。。start'
                }
          }

    }


}
