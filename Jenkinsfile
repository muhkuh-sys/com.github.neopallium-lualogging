docker.image('jenkins-ubuntu-1604').inside {
	stage 'Clean before build'
	sh 'rm -rf .[^.] .??* *'

	stage 'Checkout'
	checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'SubmoduleOption', disableSubmodules: false, recursiveSubmodules: true, reference: '', trackingSubmodules: false]], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/muhkuh-sys/com.github.tieske.lua-date.git']]])

	stage 'Install Build requirements'
	sh 'sudo apt-get --quiet --assume-yes update'
	sh 'sudo apt-get --quiet --assume-yes install cmake3'

	stage 'Build'
	sh 'mkdir build'
	sh 'cd build && cmake ..'
	sh 'cd build && make package'

	stage 'Save Artifacts'
	archive 'build/ivy-*.xml,build/pom.xml,build/date-*.zip'

	stage 'Clean after build'
	sh 'rm -rf .[^.] .??* *'
}
