node{
   stage("ACM checkout"){
       git 'https://github.com/joshimahesh/sampleapp'
    }
    stage("Compile-Package"){
       def mvnHome = tool name: 'maven-3', type: 'maven'
     sh "${mvnHome}/bin/mvn package"
    }
 
}
