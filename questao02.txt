#!/bin/bash

# Checando se o pacote mpg123 está instalado no sistema
if [ "$(which mpg123)" = "" ];then
        echo "Você não possui o mpg123 instalado"
        echo "Instalando o mpg123..."
        $(sleep 2)
        $(sudo apt-get install mpg123)
fi

# Iniciando loop
while true
do
        echo "Verificando conexão com a internet..."
        # Armazenando saída do comando ping que informa quantos pacotes foram recebidos com sucesso
        RESULTADO=$(ping -c 2 google.com | egrep received | awk -F " " '{print $4}')
        # Usando if para checar: Caso o número de pacotes recebidos sejam 0, o computador não está devidamente conectado com a rede.
        if [ "$RESULTADO" = 0 ];then
                echo "Sem internet"
                # $(mpg123 musica.mp3)
                # Essa parte eu comentei pois eu uso o wsl no windows e não consegui baixar um arquivo mp3 pra executá-lo aqui
                # No entanto, caso eu tivesse conseguido, a forma como o audio seria reproduzido seria com o comando acima.
        else
                # Se não, então a internet provavelmente está funcionando normalmente.
                echo "Internet está funcionando!"
        fi
        # Esperando 30 segundos para a próxima verificação.
        echo -e "Esperando 30 segundos para verificar novamente... \n"
        sleep 30
done