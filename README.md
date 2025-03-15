# 📌 Sistema de Agendamento de Atendimento de Saúde

<p> Somos a SAAS (Sistema de Agendamento de Atendimento de Saúde), uma startup de tecnologia focada em soluções digitais para a área da saúde. Nosso objetivo é simplificar o agendamento e o atendimento médico, oferecendo praticidade para pacientes e eficiência para profissionais da saúde.

Em construção...</p>

# Requisitos Funcionais 
**Paciente**
- RF1 - O sistema deve permitir o cadastro de pacientes.
- RF2 - O sistema deve permitir o login de pacientes.
- RF3 - O sistema deve permitir a redefinição de senha.
- RF4 - O sistema deve permitir o agendamento de consultas, escolhendo especialidade, horário e localidade.
- RF5 - O sistema deve permitir o agendamento de exames, escolhendo horário e localidade.
- RF6 - O sistema deve permitir a visualização de resultados de consultas, exames e laudos médicos.
- RF7 - O sistema deve permitir o acesso ao próprio prontuário.
- RF8 - O sistema deve permitir a consulta de CPF de pacientes cadastrados, exibindo informações relevantes.
- RF9 - O sistema deve permitir a atualização de dados pessoais.

**Profissional de Saúde**
- RF10 - O sistema deve permitir o login de profissionais de saúde.
- RF11 - O sistema deve permitir a redefinição de senha.
- RF12 - O sistema deve permitir a atualização de dados pessoais.
- RF13 - O sistema deve permitir o acesso ao prontuário dos pacientes.
- RF14 - O sistema deve permitir a consulta de CPF de pacientes cadastrados.

**Funcionalidades Restritas a Médicos**
- RF15 - O sistema deve permitir a prescrição de medicamentos.
- RF16 - O sistema deve permitir a adição de documentos, como atestados.
- RF17 - O sistema deve permitir o registro de anamnese do paciente.
- RF18 - O sistema deve permitir a solicitação de exames.

**Unidades de Saúde**
- RF19 - O sistema deve permitir o cadastro de Unidades Básicas de Saúde, clínicas e hospitais.
- RF20 - O sistema deve permitir a gestão do cadastro de profissionais de saúde.
- RF21 - O sistema deve permitir o login da unidade de saúde.
- RF22 - O sistema deve permitir a redefinição de senha da unidade de saúde.
- RF23 - O sistema deve permitir a atualização dos dados institucionais da unidade de saúde.

# Requisitos Não Funcionais
- RNF01 - O sistema deve responder rapidamente em operações de agendamento, exames e outras interações.
- RNF02 - O sistema deve garantir proteção de dados conforme a LGPD.
- RNF03 - O sistema deve possuir uma interface intuitiva e acessível.
- RNF04 - O sistema deve permitir autenticação segura e redefinição de senha.
- RNF05 - O sistema deve oferecer suporte a integrações com APIs de terceiros.

# 🚀 Tecnologias Utilizadas
- Frontend: HTML,CSS, Javascript React
- Backend: Java (Spring Boot)
- Banco de Dados: MySQL
- Notificações: SMS/WhatsApp
- Docker

# 📑 Modelo Entidade de Relacionamento (EER)

```mermaid
erDiagram
    paciente {
        BINARY id_paciente
        STRING nome
        STRING cpf
        STRING email
        STRING senha
        DATE data_nascimento
        ENUM genero
        STRING telefone
        STRING grau_instrucao
        BOOLEAN notificacoes_ativadas
    }

    unidade_de_saude {
        BINARY id_unidade_de_saude
        STRING nome
        STRING profissao
        ENUM tipo
        STRING cnpj
        STRING registro_sanitario
        TEXT descricao
    }

    profissional_de_saude {
        BINARY id_profissional_de_saude
        STRING nome
        STRING cpf
        STRING email
        STRING telefone
        STRING codigo_acesso
        STRING senha_hash
        BINARY unidade_de_saude_id
    }

    agendamento {
        BINARY id_agendamento
        DATETIME data_hora
        BINARY paciente_id
        BINARY profissional_id
        BINARY unidade_de_saude_id
        ENUM status
    }

    exame {
        BINARY id_exame
        TEXT descricao
        ENUM status
        BINARY paciente_id
        BINARY profissional_id
        BINARY agendamento_id
    }

    resultado_exame {
        BINARY id_resultado
        BINARY exame_id
        BLOB resultado
        TIMESTAMP data_resultado
    }

    prontuario {
        BINARY id_prontuario
        BINARY paciente_id
        BINARY profissional_id
        TEXT descricao
        TEXT alergia
        ENUM tipo_sanguineo
        TEXT doenca_cronica
        TIMESTAMP ultima_atualizacao
    }

    medicamento {
        INT id_medicamento
        STRING nome
        BINARY paciente_id
        BINARY profissional_id
        BINARY agendamento_id
    }

    notificacao {
        BINARY id_notificacao
        BINARY paciente_id
        ENUM tipo
        DATETIME data_envio
        ENUM status
    }

    endereco {
        BINARY id_endereco
        STRING rua
        STRING numero
        STRING bairro
        STRING cidade
        STRING uf
        STRING cep
        BINARY paciente_id
        BINARY unidade_de_saude_id
    }

    log_acesso {
        BINARY id_log
        BINARY profissional_id
        BINARY paciente_id
        TIMESTAMP data_hora
        ENUM acao
    }

    disponibilidade {
        BINARY id_disponibilidade
        BINARY profissional_id
        BINARY unidade_de_saude_id
        ENUM dia_semana
        TIME horario_inicio
        TIME horario_fim
    }

    paciente ||--o{ agendamento : "faz"
    paciente ||--o{ exame : "realiza"
    paciente ||--o{ prontuario : "possui"
    paciente ||--o{ notificacao : "recebe"
    paciente ||--o{ endereco : "possui"
    paciente ||--o{ medicamento : "usa"
    profissional_de_saude ||--o{ agendamento : "atende"
    profissional_de_saude ||--o{ exame : "realiza"
    profissional_de_saude ||--o{ prontuario : "atualiza"
    profissional_de_saude ||--o{ log_acesso : "registra"
    profissional_de_saude ||--o{ disponibilidade : "tem"
    unidade_de_saude ||--o{ profissional_de_saude : "contrata"
    unidade_de_saude ||--o{ agendamento : "recebe"
    unidade_de_saude ||--o{ endereco : "possui"
    exame ||--o{ resultado_exame : "gera"
    agendamento ||--o{ exame : "agenda"
    agendamento ||--o{ medicamento : "prescreve"

```

# 📦 Instalação e Configuração
🔧 Pré-requisitos
Antes de começar, certifique-se de ter as seguintes ferramentas instaladas:
- Node.js
- Java JDK 21
- MySQL
- Docker

# 🎯 Passos para rodar o projeto🔹Backend (Java)
# Clone o repositório
```git
git clone https://github.com/SAS-Organizacao/SAS_BackEnd.git
```

# 🛠️ Endpoints da API
# 📌 Autenticação
<p>Em construção...</p>

# 📌 Agendamentos
<p>Em construção...</p>

# 📌 Prontuário
<p>Em construção...</p>


📩 Contato📧 Email: SAAS@gmail.com

# Integrantes
</tr>
  <tr align=center>
    <td>
      <a href="https://github.com/DGuabiraba">
        <img src="https://avatars.githubusercontent.com/u/81264511?v=4" height="200px" width="200px">
      </a>
    </td>
    <td>
      <a href="https://github.com/Gabrielteles001">
        <img src="https://avatars.githubusercontent.com/u/127240150?v=4" height="200px" width="200px">
      </a>
    </td>
    <td>
      <a href="https://github.com/WalterSantos08">
        <img src="https://avatars.githubusercontent.com/u/178443270?v=4" height="200px" width="200px">
      </a>
    </td>
    <td>
      <a href="https://github.com/LeonardoIrineu">
        <img src="https://avatars.githubusercontent.com/u/112736650?v=4" height="200px" width="200px">
      </a>
    </td>
    <td>
      <a href="https://github.com/dorotrodrigues">
        <img src="https://avatars.githubusercontent.com/u/111395320?v=4" height="200px" width="200px">
      </a>
    </td>
    <td>
      <a href="https://github.com/alvesrafaelaa">
        <img src="https://avatars.githubusercontent.com/u/192259118?v=4" height="200px" width="200px">
      </a>
    </td>
    <td>
      <a href="https://github.com/CeloDigital">
        <img src="https://avatars.githubusercontent.com/u/147448840?v=4" height="200px" width="200px">
      </a>
    </td>
     <td>
      <a href="https://github.com/mattheus536">
        <img src="https://avatars.githubusercontent.com/u/171884376?v=4" height="200px" width="200px">
      </a>
    </td>
    
    
