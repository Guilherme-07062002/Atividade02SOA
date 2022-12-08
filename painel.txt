#/bin/bash¨
echo -e "######################################### Painel do Sistema ########################################################"
echo "# "
echo "# Nome do usuário logado:                 $USER"
echo "# Tempo de funcionamento do sistema:      $(uptime -p | sed 's/minutes/minutos/' |  sed 's/hours/horas/' | sed 's/hour/hora/' | sed 's/day/dia/' | sed 's/days/dias/' | cut -c 4-)"
echo "# Quantidade de usuários logados:         $(who | wc -l)"
echo "# Marca/modelo da CPU:                    $(lscpu | grep 'Model name' | cut -c 34-)       Modelo: $(lscpu | grep Model: | awk -F " " '{print $2}')"
echo "# Maior Velocidade do processador:        $(lscpu | grep 'CPU MHz' | cut -c 34-) MHz"
echo "# Quantidade Memória:                     $(free | egrep Mem | awk -F" " '{print $2}') Mb"
echo "# Memória em uso em MB:           $(free | egrep Mem | awk -F" " '{print $3}') Mb"
echo "# Memória livre:                  $(free | egrep Mem | awk -F" " '{print $4}') Mb"
echo "# Placas de rede:                         $(ip link show | egrep ^[1-9] | awk -F ":" '{print $2}' > interfaces.txt) $(for i in `< interfaces.txt`; do echo -n ${i}" | ";done; echo "")"

echo "# Trafego placa de rede entrada:"

echo "#  $(cat /proc/net/dev | sed  1,2d | grep [1-9] | awk -F " " '{print $1,$2}') bytes"

echo "# Trafego placa de rede saida:"

echo "#  $(cat /proc/net/dev | sed  1,2d | grep [1-9] | awk -F " " '{print $1,$10}') bytes"

echo "# $(date +'Data:          %d/%m/%Y') "
echo "# $(date +'A hora atual é:        %T')"
echo "# "
echo -e "####################################################################################################################\n"