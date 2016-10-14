#!/usr/bin/groovy 

node { 
    def workspace = pwd()
    stage "Download"
    git "https://github.com/frznlogic/iptables-tutorial.git"
    sh "make clean"
}

node {
    stage "Images"
    sh "make -j12 index"
    sh "make -j12 images"
}

parallel 'pdf': {
    stage('PDF') {
        node {
            sh "cd ${workspace} && make pdf"
        }
    }
},
'html': {
    stage('HTML') {
        node {
            sh "cd ${workspace} && make html"
        }
    }
},
'src': {
    stage('src') {
        node {
            sh "cd ${workspace} && make src"
        }
    }
},
'ps': {
    stage('PS') {
        node {
            sh "cd ${workspace} && make ps"
        }
    }
}

parallel 'spanish': {
    stage('Spanish') {
        node {
            sh "cd ${workspace} && make spanish"
        }
    }
},
'portuguese': {
    stage('Portuguese') {
        node {
            sh "cd ${workspace} && make portuguese"
        }
    }
}

node {
    stage 'site'
    sh "cd ${workspace} && make site"
}

