pipeline {
    agent 'Win037'

    stages {
        stage('Экспорт конфигурации из EDT в XML') {
            steps {
                timestamps {
                    cmd("ring edt workspace export --workspace-location C:\\Jenkins\\workspace\н\EDT --project C:\\Jenkins\\workspace\\EDT\\edt_test --configuration-files C:\\Jenkins\\workspace\\EDT\\edt-export")
                }
            }
        }
    }
}

def cmd(command){
    if(isUnix()) {
        sh "${command}"
    } else {
        bat "chcp 65001\n${command}"
    }
}
