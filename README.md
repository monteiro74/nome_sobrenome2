# nome_sobrenome2
meu repositorio de engenharia de software

Sistema para a clinica veterinária .....
Autor: Emiliano S. Monteiro

# 1. Descrição do sistema

Sistema para clinica veterinária...

Nome da clínica:

# 2. Diagrama do banco de dados

Colocar aqui o diagrama de banco...


```mermaid
erDiagram
    CLIENTE {
        int ID_Cliente PK
        string Nome
        string Endereco
        string Telefone
        string Email
    }

    ANIMAL {
        int ID_Animal PK
        string Nome
        string Especie
        string Raca
        int Idade
        string Condicao
        string Tipo_Racao
        string Habitos
        int ID_Cliente FK
    }

    VETERINARIO {
        int ID_Veterinario PK
        string Nome
        string Especialidade
    }

    ATENDIMENTO {
        int ID_Atendimento PK
        datetime Data_Hora
        int ID_Animal FK
        int ID_Veterinario FK
        string Receita
        string Observacoes
        int ID_Agenda FK
    }

    AGENDA {
        int ID_Agenda PK
        date Data
        time Horario
        boolean Disponivel
        int ID_Veterinario FK
    }

    CLIENTE ||--o{ ANIMAL : "possui"
    ANIMAL ||--o{ ATENDIMENTO : "é atendido"
    VETERINARIO ||--o{ ATENDIMENTO : "realiza"
    VETERINARIO ||--o{ AGENDA : "tem"
    AGENDA ||--o{ ATENDIMENTO : "agendado para"

```

# 3. Diagrama de casos de uso

Colocar aqui o diagrama de casos de uso...

![]()

# 4. Principais telas do sistema


![]()

# 5. Arquitetura do sistema


![]()

....