pipeline {
    agent {
        label 'Win037'
    }    

    stages {
        stage('Экспорт конфигурации из EDT в XML') {
            steps {
                timestamps {
                    cmd("ring edt workspace export --workspace-location C:\\Jenkins\\workspace\\EDT --project C:\\Jenkins\\workspace\\EDT\\edt_test --configuration-files C:\\Jenkins\\workspace\\EDT\\edt-export")
                }
            }
        }

        stage('Создаем пустую файловую базу данных') {
            steps {
                timestamps {
                    cmd("${env:PathOf1C} CREATEINFOBASE File=C:\\Jenkins\\workspace\\EDT\\edt-base")
                }
            }
        }

        stage('Загружаем xml файлы в конфигурацию') {
            steps {
                timestamps {
                    cmd("${env:PathOf1C} DESIGNER /F C:\\Jenkins\\workspace\\EDT\\edt-base /LoadConfigFromFiles C:\\Jenkins\\workspace\\EDT\\edt-export /UpdateDBCfg")
                }
            }
        }

        stage('Выгрузка конфигурации в файл') {
            steps {
                timestamps {
                    cmd("${env:PathOf1C} DESIGNER /F C:\\Jenkins\\workspace\\EDT\\edt-base /DumpCfg C:\\Jenkins\\workspace\\EDT\\edt-cf\1cv8.cf")
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
