# 📋 README - Sistema de Ordens de Serviço para Oficinas

Um sistema simples para gerenciar ordens de serviço (OS) em oficinas mecânicas, com cadastro de clientes, veículos, equipes, mecânicos e itens (mãos de obra e peças).

## 🚀 Visão Geral

O sistema permite:<br>

- Cadastrar clientes e veículos.<br>
- Criar ordens de serviço (OS) para consertos/revisões.<br>
- Associar equipes de mecânicos à OS.<br>
- Calcular valores com base em itens (mão-de-obra ou peças).<br>
- Obter solicitação do cliente para executar serviços.<br>

## 🗃️ Estrutura do Banco

**Tabelas Principais**

- Cliente : Dados dos clientes (nome, telefone).
- Veículo : Veículos dos clientes (marca, modelo, placa).
- Item : Itens usados ​​nos serviços (mão-de-obra ou peças, com valor unitário).
- Ordem de Serviço : Detalhes do OS (dados, status, valor, solicitação).
- Equipe e Mecânico : Equipes e mecânicos responsáveis ​​pelo OS.
  
<details> <summary>📑 Ver Todas as Tabelas e Atributos</summary>
  
**Cliente**
- idCliente INT (PK)
- nome VARCHAR(45)<br>
- telefone VARCHAR(45)<br>
  
**Veículo**
- idVeículo INT (PK)
- marca VARCHAR(45)
- modelo VARCHAR(45)
- placa VARCHAR(45)
- cliente_idCliente INT (FK)

**Item**
- idServiço INT (PK)
- descrição VARCHAR(45)
- tipo ENUM('mão_de_obra', 'peça')
- valor_unitário DECIMAL

**Ordem de Serviço**
- idOrdem_de_Serviço INT (PK)<br>
- data_entrada DATA
- data_conclusao DATA
- estado VARCHAR(45)
- autorização TINYINT
- valor DECIMAL
- veículo_idVeículo INT (FK)
- equipe_idEquipe INT (FK)

**Ordem_de_Serviço_tem_Item**
- ordem_de_serviço_idOrdem_de_Serviço INT (FK)
- item_idServiço INT (FK)
- quantidade INT
- valor_total DECIMAL

**Equipe**
- idEquipe INT (PK)
- nome VARCHAR(45)

**Mecânico**
- idMecânico INT (PK)
- nome VARCHAR(45)
- endereço VARCHAR(45)
- Especialidade VARCHAR(45)

**Equipe_tem_Mecânico**
- equipe_idEquipe INT (FK)
- mecânico_idMecânico INT (FK)
</details>

## 🔗 Relacionamentos
- Cliente ↔ Veículo : 1 cliente tem vários veículos.
- Veículo ↔ Ordem de Serviço : 1 veículo pode ter vários sistemas operacionais.
- Equipe ↔ Ordem de Serviço : 1 equipe pode gerenciar vários sistemas operacionais.
- Ordem de Serviço ↔ Item : Uma OS pode incluir vários itens (via Ordem_de_Serviço_has_Item ).
- Equipe ↔ Mecânico : Uma equipe tem vários mecânicos (via Equipe_has_Mecânico ).

🛠️ Como funciona?
<details> <summary>📖 Exemplo Prático</summary>
  
**Cenário :** João leva seu Ford Fiesta (placa ABC-1234) para uma troca de óleo. A "Equipe A" cria um SO com:<br>

- Mão-de-obra: Troca de óleo (50,00).
- Peças: 2 filtros de óleo (30,00 cada).

**Dados :**<br>
- Cliente : João (id: 1).
- Veículo : Ford Fiesta (id:1).
- Ordem de Serviço : OS #1, valor total: 110,00 (50,00 + 2×30,00), status: Concluída, autorizada.
- Item : Troca de óleo (mão-de-obra, 50,00), Filtro de óleo (peça, 30,00).
</detalhes>

