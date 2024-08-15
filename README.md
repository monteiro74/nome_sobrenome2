# nome_sobrenome2
meu repositorio de engenharia de software

Sistema para a clinica veterinária .....
Autor: Emiliano S. Monteiro


---
# 1. Descrição do sistema

Nome da clínica: cachorro amarelo.

1. Uma clínica veterinária atende apenas os animais: gatos e cachorros. 
2. Os clientes devem fazer um cadastro de si e dos animais. 
3. Os clientes devem informar as condições nas quais os animais chegam. 
4. Os clientes devem informar o tipo de ração que o animal come. 
5. O cliente deve informar hábitos do animal. 
6. Para cada animal é possível que mais de um veterinário o atenda. 
7. Os animais podem chegar e serem atendidos de acordo com uma agenda do dia. 
8. Cada animal atendido receberá uma ficha e um prontuário. 
9. Outros donos podem querer marcar horários de atendimento futuro. 
10. O atendimento gera uma receita para o animal. 
11. Quando um cliente chega na clínica veterinária ele é atendido por um atendente. 
12. O atendente deve verificar se existe agenda disponível com um veterinário. 
13. O atendente deve colocar o cliente e seu animal na fila de espera, se for o caso. 
14. O atendente deve levar o cliente e o animal até o veterinário. 
15. O veterinário deve realizar uma entrevista com o dono do animal. 
16. O resultado da entrevista deve ir para um formulário. 
17. O veterinário deverá examinar o animal e anotar em prontuário(ficha) suas observações. 
18. Dependendo da situação do animal este receberá uma receita.
19. A cobrança é registrada no contas a pagar.
20. A secretária é responsável pelo contas a pagar.
21. A clinica aceita vários de pagamento, como: cartão de crédito, pix e dinheiro.
22. A clinica tem animais para adoção em exposição.
22. A clinica trabalho em regime de plantão.
23. A clinica tem uma loja de produtos para cães e gatos.
24. A clinica tem um hotel para cães.

.
---
# 2. Diagrama do banco de dados


```mermaid
erDiagram
    CLIENTE {
        int id_cliente PK
        string nome
        string endereco
        string telefone
        string email
    }

    ANIMAL {
        int id_animal PK
        string nome
        string especie
        string raca
        int idade
        string condicao_chegada
        string tipo_racao
        string habitos
        int id_cliente FK
    }

    VETERINARIO {
        int id_veterinario PK
        string nome
        string especialidade
        string telefone
    }

    AGENDA {
        int id_agenda PK
        datetime data_hora
        int id_animal FK
        int id_veterinario FK
    }

    PRONTUARIO {
        int id_prontuario PK
        int id_animal FK
        string observacoes
    }

    RECEITA {
        int id_receita PK
        int id_animal FK
        string descricao
        datetime data_emissao
    }

    ATENDENTE {
        int id_atendente PK
        string nome
        string telefone
    }

    CONTAS_PAGAR {
        int id_contas_pagar PK
        decimal valor
        datetime data_pagamento
        string forma_pagamento
        int id_cliente FK
    }

    ANIMAIS_ADOCAO {
        int id_animal_adocao PK
        string nome
        string especie
        string raca
        int idade
    }

    PRODUTO {
        int id_produto PK
        string nome
        decimal preco
    }

    HOTEL {
        int id_hotel PK
        string nome
        int id_animal FK
    }

    CLIENTE ||--o{ ANIMAL : "possui"
    ANIMAL ||--o{ AGENDA : "agendado_para"
    VETERINARIO ||--o{ AGENDA : "atende"
    ANIMAL ||--o{ PRONTUARIO : "possui"
    ANIMAL ||--o{ RECEITA : "recebe"
    ATENDENTE ||--o{ CONTAS_PAGAR : "processa"
    CLIENTE ||--o{ CONTAS_PAGAR : "realiza"
    ANIMAL }|..|{ VETERINARIO : "atendido_por"
    ANIMAIS_ADOCAO }|--|{ CLIENTE : "adotado_por"
    CLIENTE ||--o{ HOTEL : "hospeda"
    PRODUTO ||--o{ HOTEL : "oferece"
```


# 3. Diagrama de casos de uso


![https://github.com/monteiro74/nome_sobrenome2/blob/main/penguin.png](https://github.com/monteiro74/nome_sobrenome2/blob/main/penguin.png)



# 4. Principais telas do sistema



# 5. Arquitetura do sistema


## 5.1. System Context (C4Context)

```mermaid
graph TD
    Cliente -->|Interage com| SistemaClinicaVeterinaria
    Veterinario -->|Acessa dados e atualiza| SistemaClinicaVeterinaria
    Atendente -->|Gerencia a fila e agenda| SistemaClinicaVeterinaria
    Gerente -->|Consulta relatórios| SistemaClinicaVeterinaria
    Secretaria -->|Gerencia contas| SistemaClinicaVeterinaria
    SubSistemaFinanceiro -->|Interage com| SistemaClinicaVeterinaria
    SubSistemaAgenda -->|Interage com| SistemaClinicaVeterinaria

    SistemaClinicaVeterinaria["Sistema da Clínica Veterinária"] -->|Registra Pagamentos| SubSistemaFinanceiro
    SistemaClinicaVeterinaria -->|Verifica Disponibilidade| SubSistemaAgenda

    
```

## 5.2. Container diagram (C4Container)


```mermaid
graph TD
    subgraph WebServer
        AplicacaoAtendente["Aplicação do Atendente"]
        AplicacaoVeterinario["Aplicação do Veterinário"]
        AplicacaoGerente["Aplicação do Gerente"]
    end

    subgraph BancoDeDados
        BDAnimais["BD de Animais"]
        BDClientes["BD de Clientes"]
        BDAgendamentos["BD de Agendamentos"]
        BDProntuarios["BD de Prontuários"]
        BDProdutos["BD de Produtos"]
        BDPagamentos["BD de Pagamentos"]
    end

    AplicacaoAtendente -->|Consulta e Atualiza| BDClientes
    AplicacaoAtendente -->|Consulta| BDAgendamentos
    AplicacaoAtendente -->|Atualiza| BDAnimais

    AplicacaoVeterinario -->|Consulta| BDAnimais
    AplicacaoVeterinario -->|Atualiza| BDProntuarios

    AplicacaoGerente -->|Consulta| BDPagamentos
    AplicacaoGerente -->|Consulta| BDClientes
    AplicacaoGerente -->|Consulta| BDAnimais
    AplicacaoGerente -->|Consulta| BDProdutos

    BDClientes --> BDAnimais
    BDAgendamentos --> BDAnimais

```

## 5.3. Component diagram (C4Component)


```

```



