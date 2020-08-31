# versionador-jenkins
Esse Projeto é para salvar arquivos fora do espaço de construção. 

Onde podemos recuperá-los depois de fazer outros build’s. 
Você pode limpar seu espaço de trabalho, executar outras compilações e o arquivo arquivado estará seguro. 
Após outro build, seu arquivo é substituído ou pode ser removido. 

Com este projeto todo build feito, é gerado um arquivo e salvo, caso seu nova versão apresente algum 'BUG', será fácil fazer um Roolback!


Vamos adicionar vários arquivos de uma mesma extensão, em uma pasta específica:
No exemplo abaixo a pasta é 'todos' e a extensão .js

# archiveArtifacts artefatos: 'todos / *. js'

Podemos usar também o método abaixo, para salvar apenas se for um build bem-sucedido.

# archiveArtifacts artefatos: 'todos.js', onlyIfSuccessful: true

Exemplo no pipeline:

A compilação criará um arquivo chamado generatedFile.txt e, após o bulid, o arquivará apenas se for bem-sucedido.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
pipeline { 
    agent any         stage 
    
    { 
stage ('Download') { 
            steps { 
                sh 'echo "artifact file"> generatedFile.txt' 
            } 
        } 
    } 
    post { 
        always { 
            archiveArtifacts artifacts: 'generatedFile.txt', onlyIfSuccessful: true 
        } 
    } 
 } 
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



