pipeline {
    agent {
        label 'Win037'
    }    

    stages {
        stage('Подготовка каталогов') {
            steps {
                timestamps {
                    //cleanWs()
                    //cmd("mkdir C:\\Jenkins\\workspace\\EDT\\edt-base")
                    //cmd("mkdir C:\\Jenkins\\workspace\\EDT\\edt-cf")
                    //cmd("mkdir C:\\Jenkins\\workspace\\EDT\\edt-export")
                }
            }
        }

        stage('Экспорт конфигурации из EDT в XML') {
            steps {
                timestamps {
                    cmd("ring edt workspace export --workspace-location C:\\Jenkins\\workspace\\EDT --project C:\\Jenkins\\workspace\\EDT\\edt_test --configuration-files D:\\Jenkins\\workspace\\edt-export")
                }
            }
        }

        stage('Создаем пустую файловую базу данных') {
            steps {
                timestamps {
                    cmd("${env:PathOf1C} CREATEINFOBASE File=${env:EDTBase}")
                }
            }
        }

        stage('Загружаем xml файлы в конфигурацию') {
            steps {
                timestamps {
                    script {
                        extraPath = "/LoadConfigFromFiles ${env:EDTExport} /UpdateDBCfg"
                    }
                    cmd("${env:PathOf1C} DESIGNER /F ${env:EDTBase} ${extraPath}")
                }
            }
        }

        stage('Выгрузка конфигурации в файл') {
            steps {
                timestamps {
                    cmd("${env:PathOf1C} DESIGNER /F D:\\Jenkins\\workspace\\edt-base /DumpCfg D:\\Jenkins\\workspace\\edt-cf\1cv8.cf")
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
