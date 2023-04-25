pipeline {
    agent any
    stages {
        stage('Remove stale branches') {
            steps {
                // Clone the GitHub repository
                git url: 'https://github.com/Technicalcourses2021/webapp.git', credentialsId: 'github-creds'

                // Get a list of all branches and remove any that haven't been updated in the last 30 days
                sh "git branch -r --merged | egrep -v '(^\\*|master|develop)' | sed 's/origin\\///' | xargs -n 1 git show-ref --heads -- | sort -rn | grep -v 'develop' | grep -v 'master' | while read rev ref; do if test `git log -1 --date=short --pretty=format:%ad $rev | xargs -I{} date -d {} +%s` -lt `date -d '30 days ago' +%s`; then git push origin :$ref; fi; done"

                // Push the changes to the GitHub repository
                git push origin --tags --delete --prune
            }
        }
    }
    post {
        success {
            echo 'All stale branches have been removed from the GitHub repository'
        }
        failure {
            echo 'Failed to remove stale branches from the GitHub repository'
        }
    }
}
