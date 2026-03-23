# Ping-Azure
- Conta Azure for studants
# Passo a Passo
## 1. Criar MV
- Ir em Maquinas Virtuais -> Criar
- Crie um novo grupo de recursos chamado `Ping`
- Escolha a região East US e Zona auto-selecionada
- Utilize o zona de disponibilidadee mantenha em apenas uma zona
- Tamanho recomendado `Standart_FX2mds_v2`
- Tipo de autentição `Senha`
- portas selecionadas -> ssh(22), HTTPS(443)
  1.1 Redes
  Na aba Rede, ainda na criação da maquina virtual
  - Rede vitual crie um novo grupo de rede/Rede virtual
    |Nome| MaquinasPing_RV|
    |Intervalo de endereços|10.0.0.0/16|
    |sub-rede | 10.0.0.0/24|
    - Clique em `OK`
  
  - IP publico: Maquina1-ip
  - Grupo de sg: Básico
  - Permitir portas selecionadas(443 e 22)
  - Excluir IP publico quando a VM for excluida
  - Load Balancer: Nenhum
