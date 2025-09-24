# Sandbox Granular e Transparente

## Visão Geral
O **Sandbox Granular e Transparente** é uma ferramenta inovadora para executar aplicativos desktop (.desktop ou executáveis) em ambientes isolados (sandbox) no Linux (Ubuntu LTS 24.04) e, futuramente, Windows (10/11 Pro+). Inspirada em permissões de apps móveis, permite aos usuários clicar com o botão direito em um aplicativo e selecionar "Executar em Sandbox", definindo permissões granulares para pastas, rede, hardware, etc., via uma interface intuitiva. Utiliza tecnologias como Bubblewrap/Firejail (Linux) e Windows Sandbox/AppContainers (Windows), garantindo proteção contra malwares e vulnerabilidades.

### Objetivos
- **Segurança**: Isolar aplicativos com permissões mínimas, aplicando OWASP Top 10, NIST AI RMF, GDPR/LGPD.
- **Usabilidade**: Interface amigável para não-técnicos, com logs transparentes de acessos.
- **Escalabilidade**: Arquitetura modular para suportar Linux e Windows.

### Escopo
- **Fase 1 (Linux)**: Integração com Nautilus, GUI de permissões, sandboxing com Bubblewrap/Firejail.
- **Fase 2 (Windows)**: Expansão para Explorador de Arquivos, usando Windows Sandbox/Sandboxie.
- **Exclusões**: Não inclui macOS ou sandboxing proprietário.

## Estrutura do Projeto
```
/sandbox-tool
├── .github/workflows/       # Pipelines CI/CD (linting, scans de segurança)
├── src/                     # Código-fonte
│   ├── linux/              # Módulos Linux (ex.: wrapper Bubblewrap)
│   ├── windows/            # Stubs para Windows
│   ├── common/             # Cross-platform (ex.: GUI, logging)
├── tests/                   # Testes unitários/integração
├── docs/                    # Documentação (setup, conformidade)
├── .gitignore               # Exclui segredos, venv, etc.
├── .gitattributes           # Configs Git (ex.: normalização EOL)
├── README.md                # Este arquivo
└── requirements.txt         # Dependências Python
```

## Pré-requisitos
- **SO**: Ubuntu 24.04 LTS (foco inicial); Windows 10/11 Pro+ (futuro).
- **Ferramentas**: 
  - Python 3.10+
  - Bubblewrap, Firejail (Linux)
  - PyGObject (GUI Gtk) ou PyQt (fallback cross-platform)
  - Git, pip, virtualenv
- **Segurança**: GPG para commits assinados; Dependabot para scans de vulnerabilidades.

## Setup do Ambiente
1. Clone o repositório:
   ```bash
   git clone https://github.com/felipepizetta/sandbox-tool.git
   cd sandbox-tool
   ```
2. Crie e ative um ambiente virtual:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```
3. Instale dependências:
   ```bash
   pip install -r requirements.txt
   ```
4. Instale ferramentas Linux:
   ```bash
   sudo apt update
   sudo apt install bubblewrap firejail
   ```
5. Configure Git para commits assinados:
   ```bash
   git config --global user.signingkey <sua-chave-GPG>
   git config --global commit.gpgsign true
   ```

## Desenvolvimento
- **Metodologia**: Scrum (sprints de 2 semanas) com elementos Waterfall na expansão Windows.
- **Branches Git**:
  - `main`: Versão estável.
  - `develop`: Integração de features.
  - `setup/sprint0-environment`: Setup inicial (este sprint).
- **Segurança**:
  - OWASP Top 10: Aplicado em configs e código (ex.: evitar hardcoding).
  - GDPR/LGPD: Logs sem PII; consentimento planejado para GUI.
  - Hardening: CI/CD com scans SAST (flake8, CodeQL); Dependabot ativo.

## Como Contribuir
1. Crie uma feature branch: `git checkout -b feature/<sprintX-nome-tarefa>`.
2. Commit com mensagens claras: `git commit -S -m "feat: descrição da tarefa"`.
3. Abra PR para `develop` com revisão obrigatória.
4. Siga o DoD: Código testado, scans SAST, conformidade.

## Conformidade
- **OWASP Top 10**: Proteção contra injeções, broken access control, etc.
- **NIST AI RMF**: Riscos mapeados para futuras features de IA (ex.: detecção de ameaças).
- **GDPR/LGPD**: Logs auditáveis sem dados pessoais; plano de consentimento.

## Contato
- **Issues**: Reporte bugs ou sugestões no GitHub Issues.
- **Dúvidas**: felipepizetta@icloud.com