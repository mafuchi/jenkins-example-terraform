abcs = ['kittens', 'bunnies', 'hamsters']
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
      }
    }
	stage('Spike 1: loop of echo statements') {
		steps {
        echo_all(abcs)
	  }
    }
    stage('Spike 2: loop of sh commands') {
		steps {
        loop_of_sh(abcs)
      }
    }
    stage('Spike 3: loop with preceding SH') {
		steps {
        loop_with_preceding_sh(abcs)
      }
    }
    stage('Spike 4: traditional for loop') {
		steps {
        traditional_int_for_loop(abcs)
      }
	}
	}
  }
  post {
    always {
      cleanWs()
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
// echoes everything as expected
