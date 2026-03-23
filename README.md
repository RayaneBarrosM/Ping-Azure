# Ping-Azure
- Conta Azure for studants
# Passo a Passo
## 1. Criando a primeira VM
- Grupo de recursos: Criar novo → Ping
- Nome: Maquina1
- Região: centralus (ou southcentralus)
- Opções de disponibilidade: Nenhuma
- Zona de disponibilidade: Nenhuma (não selecione)
- Imagem: Ubuntu Server 24.04 LTS - x64 Gen2
- Tamanho: Standard_D2s_v3 ⬅️ USE ESTE
- Autenticação: Senha
- Usuário: azureuser
- Senha: (crie uma senha forte com 12+ caracteres, maiúscula, minúscula, número e símbolo)

### 1.1 Redes:
- Rede virtual: Criar nova
| Nome | MaquinasPing_RV |
| Intervalo de endereços | 10.0.0.0/16 |
| Sub-rede | 10.0.0.0/24 |
- IP público: Maquina1-ip
- Portas de entrada: SSH (22) e HTTPS (443)
- Grupo de segurança de rede: Básico
- Excluir IP público quando a VM for excluída: Sim
- Load Balancer: Nenhum

## 2.Criando a segunda maquina
- No portal Azure, clique em **"Criar recurso"** → **"Máquina Virtual"**
- Na aba **Básico**:
    - **Grupo de recursos**: Selecione `Ping` (já existente)
    - **Nome**: `Maquina2`
    - **Região**: O campo pode aparecer desabilitado ou já preenchido com `centralus` automaticamente. Se estiver desabilitado, está correto!
    - **Opções de disponibilidade**: `Nenhuma`
    - **Zona de disponibilidade**: `Nenhuma`
    - **Imagem**: `Ubuntu Server 24.04 LTS - x64 Gen2`
    - **Tamanho**: `Standard_D2s_v3`
    - **Autenticação**: `Senha`
    - **Usuário**: `azureuser` (mesmo da VM1)
    - **Senha**: (a mesma senha da VM1)
      
### 2.2 Na aba **Redes**
- **Rede virtual**: Selecione `MaquinasPing_RV` (já criada)
- **Sub-rede**: Selecione `subnet01` (ou `default`, `10.0.0.0/24`)
- **IP público**:  `Maquina2-ip`
- **Portas de entrada**: Marque `SSH (22)` e `HTTPS (443)`
- **Grupo de segurança de rede**: `Básico`
- Clique em **Revisar + criar** e depois em **Criar**

## 3. Fazendo o Ping

### **1. Liberar ICMP em ambas as VMs**

- vá para a aba maquina virtual e clique em uma das maquinas
- desça a té a seção redes
- Lá estará o ip da sua máquina
  ![image.png](attachment:68d69fda-56f7-4b2e-8fc7-0cb351e58836:image.png)
  
- No menu lateral clique em Rede → configurações de rede
- Localize o grupo de segurança de rede
- Clique no nome
- Va em configurações → Regras de entrada → Adicionar
  
  ![image.png](attachment:41496023-0289-4985-a57f-5de8c16cc89c:image.png)
  
**Preencha os campos**
  
| **Campo** | **Valor** |
| --- | --- |
| Origem | `Qualquer` |
| Intervalos de porta de origem | `*` |
| Destino | `Qualquer` |
| Intervalos de porta de destino | `*` |
| Protocolo |  ICMPv4 |
| Ação | `Permitir` |
| Prioridade | Digite **`300`** |
| Nome | Digite **`Permitir-Ping`** |

- Clique em **"Adicionar"**
