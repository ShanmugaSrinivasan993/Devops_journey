pipeline{
  agent any
  environment{
    NEW_VERSION='1.3.0'
    SERVER_CREDENTIALS= credentials('server-credentials') //this is the 'id' name that we give when we create credentials in jenkins
  }
  stages{
    stage("Build"){
      // we can set conditions for stages to execute
      when{
        expression{
          //this stage will execute only if branch name is dev and if any code changes occur in github
          BRANCH_NAME== 'dev' //&& CODE_CHANGES==true
        }
      }
      steps{
        echo "I am in Build job"
        echo "Version is ${NEW_VERSION}"
      }
    }
    stage("Test"){
      when{
        expression{
          //this stage will execute only if branch name is main or dev
          BRANCH_NAME== 'dev' || BRANCH_NAME=='main'
        }
      }
      steps{
        echo "I am in Test job"
      }
    }
    stage("Deploy"){
      steps{
        echo "I am in Deploy job"
        sh "some script ${USER} ${PWD}"
        // or you can use this credentials in another way
        withCredentials([
          usernamePassword(credentials: "server-credentials", usernameVariable: USER, passwordVariable: PWD)
        ]){
          sh "some script ${SERVER_CREDENTIALS}"
        }
      }
    }
  }
  // post attribute in Jenkinsfile
  post{
    //this will execute some kind of logic after all the stages are done.
    always{
      //logic will execute whether build succeeds or fails.
    }
    success{
      //logic will execute only if build is success
    }
    failure{
      //logic will execute if build fails
    }
  }
}
