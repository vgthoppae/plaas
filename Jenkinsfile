node {
	echo "App being built is ${AppName}"

	def appname = "${AppName}".toLowerCase()

	cleanup()

	stage "Checkout Pipeline code"

  checkoutPipelineCode()

	def app = getAppMetadata(appname)
	
	echo "Working on app ${app.name}"

  echoCurrentDirAndContents()

  stage "Checkout App code"
	checkoutAppCode(app)
	echoCurrentDirAndContents()

	stage "Create AWS Stack"
	createAWSStack(app)
}

def getAppMetadata(appname) {
  def appMetadata = readYaml file: 'app-metadata/cheddar-params.yml'
  return appMetadata.app;
}

def cleanup() {
	echo "Clean up the current working directory"
	sh 'rm -rf ./*'
}

def checkoutPipelineCode() {
	echo "Checking out pipeline code..."
	checkout scm
	echo "Pipeline code Checkout completed..."
}

def checkoutAppCode(app) {
	echo "Checking out app code..."
	checkout ([$class: 'GitSCM', 
    branches: [[name: '*/vt-plaas']], 
    doGenerateSubmoduleConfigurations: false, 
    extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'appcode']], 
    submoduleCfg: [], 
    userRemoteConfigs: [[url: "${app.gitrepo}"]]
])
	echo "App code Checkout completed..."
}

def echoCurrentDirAndContents() {
	dirlist = sh (
		script: 'ls -l',
		returnStdout: true)
	currentdir = sh (
		script: 'pwd',
		returnStdout: true)

	echo "$dirlist"
	echo "$currentdir"
}

def createAWSStack(app) {
	sh "ansible-playbook cfstack-play.yml --extra-vars '@./appcode/deployment/params.yml' --extra-vars '@./app-metadata/${app.name}-params.yml'"
}