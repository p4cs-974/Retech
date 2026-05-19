# ♻️ Retech - Sistema de Gerenciamento de Descarte Tecnológico

## 📌 Sobre o Projeto
O **Retech** é uma **aplicação desktop** focada na gestão do ciclo de vida de ativos de TI. Este projeto acadêmico nasceu da necessidade de aplicar boas práticas de gerenciamento de infraestrutura, garantindo que o fluxo de equipamentos — desde o inventário até o descarte ou redirecionamento — seja rastreável, seguro e organizado.

A ferramenta foi idealizada para otimizar a rotina de suporte e a resolução de demandas relacionadas à substituição de peças, controle de sucata e envio de equipamentos para manutenção ou descarte ecológico. Por ser um aplicativo instalado localmente, funciona sem depender de um navegador ou de conexão constante com a internet.

## ⚙️ Arquitetura e Funcionalidades

O sistema foi estruturado de forma modular, dividindo as responsabilidades em diferentes fluxos operacionais:

### 👤 1. Controle de Acesso e Usuários (CRUD)
A segurança e a identificação de quem realiza as movimentações são fundamentais na gestão de ativos.
* **Create:** Tela de cadastro de novos técnicos/usuários com validação para evitar CPFs duplicados.
* **Read:** Sistema de login seguro que valida as credenciais e inicia a sessão no aplicativo.
* **Update:** Painel "Meu Perfil", onde o usuário logado pode atualizar suas informações pessoais e alterar sua senha.
* **Delete:** Opção de exclusão permanente da própria conta do sistema.
* **Recuperação:** Fluxo "Esqueci minha senha" para redefinição segura de acesso.

### 📦 2. Gestão de Inventário
Uma visão centralizada de todos os dispositivos disponíveis sob controle da equipe.
* Listagem dinâmica de equipamentos cadastrados.
* Identificação detalhada do estado do item (Novo, Seminovo, Usado, Com Defeito, Sucata).
* Exclusão de registros do banco de dados local com confirmação de segurança.

### ♻️ 3. Fluxo de Descarte e Saídas
O *core* do sistema, focado na movimentação e no fim do ciclo de vida dos ativos.
* **Entrada para Descarte:** Registro detalhado contendo o tipo de produto, quantidade, estado de conservação e o motivo técnico da baixa.
* **Saída de Itens:** Interface de seleção múltipla (checkbox) para despachar equipamentos do inventário para locais de destino (ex: centros de reciclagem, assistência técnica ou outras unidades).
* **Histórico (Audit Log):** Log completo de todos os itens movimentados, registrando a data e o destino, com a funcionalidade de estornar (retornar) o item para o inventário principal caso o envio seja cancelado.

## 💻 Tecnologias e Técnicas Utilizadas

O Retech é desenvolvido como um aplicativo desktop multiplataforma com **.NET MAUI**, com foco em performance e excelente UI/UX. O alvo principal é o **Windows**, mas a stack permite executar e testar também no **macOS (Mac Catalyst)**.

* **C# / .NET:** Linguagem e plataforma base da aplicação, com a lógica de negócio organizada em camadas.
* **.NET MAUI:** Framework de UI multiplataforma que constrói um único projeto para Windows e macOS, com componentes nativos de cada sistema.
* **XAML:** Definição declarativa das telas e dos layouts, com data binding para atualização dinâmica das informações.
* **Padrão MVVM:** Separação entre a camada visual (Views), o estado/lógica de apresentação (ViewModels) e os dados (Models), facilitando manutenção e testes.
* **Persistência Local:** Armazenamento dos dados (usuários, inventário, histórico) em banco local no dispositivo — por exemplo SQLite — garantindo que as informações permaneçam disponíveis offline.
* **Notificações Customizadas (Toast):** Sistema próprio de alertas visuais assíncronos, mantendo a consistência da interface em vez dos diálogos padrão do sistema operacional.

## 🚀 Como Executar

Pré-requisitos: [.NET SDK](https://dotnet.microsoft.com/download) com a workload do MAUI instalada (`dotnet workload install maui`).

```bash
# Restaurar dependências
dotnet restore

# Executar no Windows
dotnet build -t:Run -f net8.0-windows10.0.19041.0

# Executar no macOS (Mac Catalyst)
dotnet build -t:Run -f net8.0-maccatalyst
```
