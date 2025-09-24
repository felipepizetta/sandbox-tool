# Sandbox Granular e Transparente

## Visão Geral
O **Sandbox Granular e Transparente** é uma ferramenta para executar aplicativos desktop (.desktop ou executáveis) em ambientes isolados no Linux (Ubuntu LTS 24.04) e, futuramente, Windows (10/11 Pro+). Inspirada em permissões de apps móveis, permite clicar com o botão direito em um aplicativo, selecionar "Executar em Sandbox" e definir permissões granulares (pastas, rede, hardware) via interface intuitiva. Usa Bubblewrap/Firejail (Linux) e Windows Sandbox/AppContainers (Windows) para proteção contra malwares/vulnerabilidades.

### Objetivos
- **Segurança**: Isolar apps com permissões mínimas, seguindo OWASP Top 10, NIST AI RMF, GDPR/LGPD.
- **Usabilidade**: Interface simples para não-técnicos, com logs transparentes.
- **Escalabilidade**: Arquitetura modular para Linux e Windows.

### Escopo
- **Fase 1 (Linux)**: Integração com Nautilus, GUI de permissões, sandboxing com Bubblewrap/Firejail.
- **Fase 2 (Windows)**: Expansão para Explorador de Arquivos com Windows Sandbox/Sandboxie.
- **Exclusões**: Não suporta macOS ou sandboxing proprietário.

## Estrutura do Projeto
```
/sandbox-tool
├── .github/workflows/       # CI/CD (linting, scans de segurança, testes)
├── src/
│   ├── common/             # Cross-platform (ex.: sandbox base)
│   ├── linux/              # Módulos Linux
│   ├── windows/            # Stubs Windows
├── tests/                   # Testes unitários
├── docs/                    # Documentação
├── .gitignore               # Exclui segredos
├── .gitattributes           # Configs Git
├── README.md                # Este arquivo
└── requirements.txt         # Dependências
```

## Pré-requisitos
- **SO**: Ubuntu 24.04 LTS; Windows 10/11 Pro+ (futuro).
- **Ferramentas**: Python 3.10+, Bubblewrap, Firejail, PyGObject (ou PyQt5 como fallback), Git, pip, virtualenv.
- **Dependências do Sistema (Ubuntu)**:
  - `libcairo2-dev`, `libgirepository1.0-dev`, `gir1.2-gtk-3.0` (para PyGObject).
- **Segurança**: GPG para commits assinados; Dependabot para scans de vulnerabilidades.

## Setup do Ambiente
1. Clone o repositório:
   ```bash
   git clone https://github.com/felipepizetta/sandbox-tool.git
   cd sandbox-tool
   ```
2. Instale dependências do sistema (Ubuntu):
   ```bash
   sudo apt update
   sudo apt install -y bubblewrap firejail libcairo2-dev libgirepository1.0-dev gir1.2-gtk-3.0
   ```
3. Crie ambiente virtual:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```
4. Instale dependências Python:
   ```bash
   pip install -r requirements.txt
   ```
   **Nota**: Se PyGObject falhar, use PyQt5 como fallback (remova PyGObject e pycairo de requirements.txt).
5. Configure Git para commits assinados:
   ```bash
   git config --global user.signingkey <sua-chave-GPG>
   git config --global commit.gpgsign true
   ```

## Desenvolvimento
- **Metodologia**: Scrum (sprints de 2 semanas) com Waterfall na expansão Windows.
- **Branches Git**:
  - `main`: Estável.
  - `develop`: Integração.
  - `setup/sprint0-environment`: Setup inicial.
- **Segurança**:
  - OWASP: Proteção contra injeções, misconfiguration.
  - GDPR/LGPD: Logs sem PII.
  - Hardening: CI/CD com scans SAST (flake8, CodeQL).

## Como Contribuir
1. Crie branch: `git checkout -b feature/<sprintX-nome-tarefa>`.
2. Commit: `git commit -S -m "feat: descrição"`.
3. PR para `develop` com revisão.
4. Siga DoD: Código testado, scans SAST, conformidade.

## Conformidade
- **OWASP Top 10**: Proteção contra injeções, broken access control.
- **NIST AI RMF**: Riscos mapeados para IA futura.
- **GDPR/LGPD**: Logs auditáveis sem PII.

## Status do CI/CD
- **Linting**: Flake8/pylint para qualidade de código.
- **Segurança**: Safety/CodeQL para scans de vulnerabilidades.
- **Testes**: Unittest inicial (expansão com pytest).

## Contato
- **Issues**: Reporte bugs no GitHub Issues.
- **Dúvidas**: felipepizetta@icloud.com.