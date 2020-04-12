pipeline {
    agent {
        label 'test-node-a'
    }
    triggers {
        pollSCM('H/2 * * * *')
    }
    stages {
        stage('Run a docker') { 
            steps {
                sh '''uptime''' 
            }
        }
	stage('Mster in environment') {
		when {
			branch 'master'
		}
		steps {
			sh '''free -m'''
		}
	}
        stage('Test-t in environment') { 
            when {
			branch 'test-t'
            }
            steps {
                sh '''echo `pwd;ifconfig|grep -Po '(?<=inet )[0-9.]+(?=  netmask)' |grep  -v '127.0.0.1'`;python setup.py install; ls -l''' 
            }
        }
        stage('echo a message') { 
            steps {
                sh 'echo 567890xxxx >> /tmp/t.log' 
            }
        }

        stage('Parallel............') {
    		parallel {
        		stage('Parallel a stage first') {
				steps {
                    			echo 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx11--------'
				}
        		}

			stage('Paralle a stage second') {
				steps {
					echo 'yyyyyyyyyyyyyyyyyyyyyyyyy'
				}
        		}
			stage('Another...') {
				stages {
					stage('another stage') {
						steps {
							echo 'zzzzzzzzzzzzzzzzzz'
						}
					}
        			}
			}
    		} 
	}



    }






    post {
	failure {
			emailext(subject: '[Failed to build]',body: '$DEFAULT_CONTENT',to: 'qichuan.zhang@qq.com')
		}
	}
}
