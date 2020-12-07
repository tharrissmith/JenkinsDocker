def dockerImage;

node('docker'){
	stage('SCM'){
		checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/tharrissmith/JenkinsDocker']]]);
	}
	stage('build'){
		dockerImage = docker.build('tharrissmithco/agent-dnc:v$BUILD_NUMBER', './dotnetcore');
	}
	stage('push'){
		docker.withRegistry('', 'dockerhubcreds'){
			dockerImage.push();
		}
	}
}