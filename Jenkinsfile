node{
   
   stage("App Build started"){
      echo 'App build started..'
      git credentialsId: 'madhu-pk', url: 'https://github.com/kingsmen-sam/python-docker-app-openshifts'
      }
   
   stage('Docker Build') {
     def app = docker.build "manee2k6/py-spartans"
    }
   
   stage("Tag & Push image"){
      withDockerRegistry([credentialsId: 'dockerID',url: ""]) {
          sh 'docker tag manee2k6/py-spartans manee2k6/py-spartans:dev'
          sh 'docker push manee2k6/py-spartans:dev'
          sh 'docker push manee2k6/py-spartans:latest'
      }
    }
   
   stage("App deployment started"){
     sh 'oc login --token=CA2Orx-YEpEK3ovZX5G8N8rNQdAtZwjbUBqNgShQF7Q --server=https://api.us-west-1.starter.openshift-online.com:6443'
     sh 'oc project itrainspartans'
     sh 'oc new-app --name py-mani manee2k6/py-spartans' 
     sh 'oc expose svc py-mani' 
    }
   
    stage('App deployed to Openshift environment') {
     echo 'App deployed to Openshift environment..'
    }

  }
