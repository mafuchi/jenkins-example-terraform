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
        untar file: './Kikicam.tar' dir: 'Kikicam_01'
        }  
    }
    stage ('tar cats') {
	steps { 
        tar file : 'Kikicam_1.tar' dir : 'Kikicam_01'	compress : true
      }  
    }
    stage ('un-tar more cats') {
	steps {
        untar file: 'Kikicam_1.tar'
      }  
    }
    stage ('tar more cats') {
	steps {
        tar file : 'Kikicam_2.tar' dir : 'Kikicam_01' compress : true	
      }  
    }
        stage ('test cat tar') {
	steps {
        tar file: 'Kikicam_2.tar' dir: 'Kikicam_02' test : true	
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
