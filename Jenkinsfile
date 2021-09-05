import org.jenkinsci.plugins.pipeline.modeldefinition.Utils

def dev_server
def prod_server='coangha@192.168.56.101'
node {
    final scmVars = checkout(scm)
    def target = scmVars.GIT_BRANCH
    def tag = sh(returnStdout: true, script: "git tag --sort version:refname | tail -1").trim()
    def checkRelease = tag==~ /^release-version-*.*.*\w+/

    stage('Build') {
        if (target == 'origin/feature' || target == 'origin/develope' || checkRelease){
            echo 'Building on branch ' + target
        }
        else {
            echo 'skipping stage'
            Utils.markStageSkippedForConditional('Build')
        }
    }
    stage('Test') {
        if (target == 'origin/feature' || target == 'origin/develope' || checkRelease){
            echo 'Testing branch ' + target
        }
        else{
            echo 'skipping stage'
            Utils.markStageSkippedForConditional('Test')
        }
    }
    stage('Push'){

    }
    stage('Deploy on dev server'){
        if (target == 'origin/develope'){
            echo 'Deploy to dev server'
        }
        else{
            echo 'skipping stage'
            Utils.markStageSkippedForConditional('Deploy on dev server')
        }
    }
    stage('Deploy on production server'){
        if (target == 'origin/main' && checkRelease){
            echo 'Deploy to production server ' + prod_server
        }
        else {
            echo 'skipping stage'
            Utils.markStageSkippedForConditional('Deploy on production server')
        }
    }
}

                                            