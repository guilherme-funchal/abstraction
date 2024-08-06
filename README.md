# ERC4337 Example Project


## Overview
- **EntryPoint**: Gerencia as operações.
- **AccountFactory**: Cria novas contas.
- **Paymaster**: Define que paga as transações
- **SimpleAccount**: Estrutura básica de criação de contas
- **ExampleContract**: ERC721 token
- **ExampleContract2**: ERC20 token

## Requisites

- Defina `.env` define chave primaria e URL do Hardhat


## Passos pra execução
Siga estas etapas para implantar contratos e executar transações:

### 1. Publique o EntryPoint
Este script implanta o contrato EntryPoint, que é central para gerenciar operações de usuário conforme o padrão ERC4337. Ele aguarda a implantação e registra o endereço onde o EntryPoint é implantado.

`npx hardhat run --network localhost ./scripts/deploy_EntryPoint.js`

### 2. Publique o AccountFactory
Este script implanta o contrato AccountFactory. O AccountFactory é responsável por criar novas contas baseadas em contratos inteligentes. Ele pega o endereço do EntryPoint implantado anteriormente como um parâmetro.

`npx hardhat run --network localhost ./scripts/deploy_AccountFactory.js`

### 3. Publique o Paymaster
Este script implanta o contrato Paymaster, que cobre taxas de transação para SimpleAccounts criadas a partir do AccountFactory especificado. O endereço EntryPoint e o endereço AccountFactory são passados ​​como parâmetros para o Paymaster.

`npx hardhat run --network localhost ./scripts/deploy_Paymaster.js`

### 4. Get Sender Address 
Este script cria uma carteira Externally Owned Account (EOA). A carteira EOA é crítica porque assina as transações SimpleAccount na rede e fornece uma camada de controle e segurança para as operações do usuário. Além disso, este script determina o endereço de implantação do contrato SimpleAccount, que incorpora uma estrutura de conta fundamental para usuários dentro do protocolo ERC4337.

`npx hardhat run --network localhost ./scripts/getSenderAddress.js`

### 5. Deploy ExampleContract
Este script implementa o ExampleContract, um contrato de token ERC721 simples. Este contrato é usado para cunhar tokens nesta demonstração.

`npx hardhat run --network localhost ./scripts/deploy_ExampleContract.js`

### 6. Deploy ExampleContract2
Este script implementa o ExampleContract, um contrato de token ERC20 simples. Este contrato é usado para cunhar tokens nesta demonstração.

`npx hardhat run --network localhost ./scripts/deploy_ExampleContract2.js`

Este script é responsável por financiar as contas necessárias para habilitar as Operações do Usuário. Ele deposita fundos no contrato EntryPoint para o Paymaster. Isso garante que o Paymaster tenha saldo suficiente para cobrir as taxas de transação para carteiras criadas a partir da AccountFactory especificada. Além disso, o script financia a carteira EOA (Externally Owned Account) que possui a SimpleAccount.

`npx hardhat run --network localhost ./scripts/depositFunds.js`

### 7. Enviar operação do usuário exemplo 1 ERC721
Este script executa uma operação do usuário interagindo com os seguintes contratos: EntryPoint, Paymaster, SimpleAccount e ExampleContract. Ele prepara e envia uma transação para o contrato EntryPoint, que normalmente envolve uma chamada de função como safeMint do ExampleContract, usando o SimpleAccount do usuário.
A transação é patrocinada pelo Paymaster, que cobre as taxas de transação, usando os fundos depositados anteriormente.

`npx hardhat run --network localhost ./scripts/sendUserOp.js`

### 7. Enviar operação do usuário exemplo 2 ERC20
Este script executa uma operação do usuário interagindo com os seguintes contratos: EntryPoint, Paymaster, SimpleAccount e ExampleContract. Ele prepara e envia uma transação para o contrato EntryPoint, que normalmente envolve uma chamada de função como safeMint do ExampleContract, usando o SimpleAccount do usuário.
A transação é patrocinada pelo Paymaster, que cobre as taxas de transação, usando os fundos depositados anteriormente.

`npx hardhat run --network localhost ./scripts/sendUserOp2.js`

### 8. Script teste 1
 Este script verifica os resultados da operação anterior. Ele consulta o ExampleContract para o tokenId mais recente e o saldo de token do SimpleAccount, verificando o sucesso da operação de cunhagem.

`npx hardhat run --network mumbai ./scripts/test.js`

### 8.  Script teste 2
 Este script verifica os resultados da operação anterior. Ele consulta o ExampleContract para o tokenId mais recente e o saldo de token do SimpleAccount, verificando o sucesso da operação de cunhagem.

`npx hardhat run --network mumbai ./scripts/test2.js`

## Configuração
- `hardhat.config.js`: Configuração hardhat
- `addressesConfig.js`: Configuração dos endereços de todos os contratos e contas
- `.env`: Contas e chaves de deploy dos contratos no Hardhat

