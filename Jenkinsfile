pipeline {
  agent any
  stages {
    stage('clean') {
      steps {
        sh 'mvn clean'
      }
    }
    stage('build') {
      steps {
        sh 'mvn install'
      }
    }
    stage('Tag Master') {
      when {
        branch 'master'
      }
      steps {
        sh '`git describe --tags --abbrev=0 | awk -F. \'{$NF+=1; OFS="."; print $0}\'`'
        sh 'NEW_VERSION=`git describe --tags --abbrev=0 | awk -F. \'{$NF+=1; OFS="."; print $0}\'`'
        sh 'echo new version $NEW_VERSION'
        sh 'git tag -a $NEW_VERSION -m "new release"'
        sh 'git push origin $NEW_VERSION'
      }
    }
  }
}
