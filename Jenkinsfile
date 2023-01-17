abcs = ['kittens', 'bunnies', 'hamsters', 'elepahnts', 'cute dogs']
pipeline {
  agent { label 'linux'}
  options {
    skipDefaultCheckout(true)
    timestamps () 
  }
  stages{
    stage('clean workspace') {
      steps {
        cleanWs()
      }
    }
    stage('checkout') {
      steps {
        checkout scm
      }
    }
    stage('terraform') {
      steps {
        sh './terraformw apply -auto-approve -no-color'
	sleep 30 // seconds
      }
    }
    stage('Spike 1: loop of echo statements') {
	steps {
        echo_all(abcs)
	sleep 30 // seconds
      }
    }
    stage('Spike 2: loop of sh commands') {
	steps {
        loop_of_sh(abcs)
	sleep 30 // seconds
      }
    }
    stage('Spike 3: loop with preceding SH') {
	steps {
        loop_with_preceding_sh(abcs)
	sleep 30 // seconds
      }
    }
    stage('Spike 4: traditional for loop') {
	steps {
        traditional_int_for_loop(abcs)
	sleep 30 // seconds
      }
    }
    stage ('list cats') {
	steps {
        sh 'ls'	
        }  
    }
	  stage ('un-tar cats') {
	steps {
        sh 'tar -xzvf Kikicam.tar'	
        }  
    }
    stage ('tar cats') {
	steps {
        sh 'tar -cfz Kikicam_1.tar ./Kikicam_01'	
      }  
    }
    stage ('un-tar more cats') {
	steps {
        sh 'tar -xzvf Kikicam_1.tar'
      }  
    }
    stage ('tar more cats') {
	steps {
        sh 'tar -cfz Kikicam_2.tar ./Kikicam_01'	
      }  
    }
  }
  post {
    always {
      cleanWs()
    }
  }
}


@NonCPS // has to be NonCPS or the build breaks on the call to .each
def echo_all(list) {
    list.each { item ->
        echo "I love ${item}"
    }
}
// outputs all items as expected

@NonCPS
def loop_of_sh(list) {
    list.each { item ->
        sh "echo I may really love ${item}"
    }
}
// outputs only the first item

@NonCPS
def loop_with_preceding_sh(list) {
    sh "echo Going to echo a list"
    list.each { item ->
        sh "echo I love so many ${item}"
    }
}
// outputs only the "Going to echo a list" bit

//No NonCPS required
def traditional_int_for_loop(list) {
    sh "echo Going to echo a list"
    for (int i = 0; i < list.size(); i++) {
        sh "echo I love ${list[i]}"
    }
}
