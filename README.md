# 📋 Service Template

![Finance Control](https://img.shields.io/badge/Project-Finance%20Control-blue)
![Template](https://img.shields.io/badge/Type-Template-yellow)
![Python](https://img.shields.io/badge/Python-3.11%2B-green)
![FastAPI](https://img.shields.io/badge/Framework-FastAPI-009688)
![Status](https://img.shields.io/badge/Status-✅_Active-brightgreen)
![Version](https://img.shields.io/badge/Version-1.0.0-blue)

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Template](https://img.shields.io/badge/Template-Use_This-blueviolet)](https://github.com/personal-finance-control-app/fc-service-template/generate)

## 🚀 Sobre o Template

Este repositório é um template para criar novos microserviços no projeto **Finance Control**. Ele fornece uma estrutura padronizada, configurações pré-definidas e pipelines CI/CD para acelerar o desenvolvimento de novos serviços.

## 📦 O que está incluído

### 🏗️ Estrutura do Projeto
```
fc-service-template/
├── .github/
│   └── workflows/
│       ├── ci.yml              # Pipeline de CI
│       ├── cd.yml              # Pipeline de CD
│       └── codeql-analysis.yml # Análise de segurança
├── src/
│   ├── domain/                 # Entidades e regras de negócio
│   │   ├── entities.py         # Entidades do domínio
│   │   ├── repositories.py     # Interfaces de repositórios
│   │   └── services.py         # Serviços de domínio
│   ├── application/            # Camada de aplicação
│   │   ├── use_cases.py        # Casos de uso
│   │   └── dto.py              # Data Transfer Objects
│   ├── infrastructure/         # Implementações concretas
│   │   ├── database.py         # Configuração do banco
│   │   ├── repositories.py     # Implementação de repositórios
│   │   └── api/                # Controladores API
│   │       ├── routes.py       # Rotas da API
│   │       ├── dependencies.py # Dependências
│   │       └── middleware.py   # Middlewares
│   ├── config.py               # Configurações da aplicação
│   ├── main.py                 # Entry point da aplicação
│   └── container.py            # Injeção de dependência
├── tests/
│   ├── unit/                   # Testes unitários
│   ├── integration/            # Testes de integração
│   ├── conftest.py             # Configuração do pytest
│   └── __init__.py
├── scripts/
│   ├── start.sh                # Script de inicialização
│   ├── test.sh                 # Script de testes
│   └── deploy.sh               # Script de deploy
├── Dockerfile                  # Configuração Docker
├── docker-compose.yml          # Docker Compose para desenvolvimento
├── requirements.txt            # Dependências Python
├── requirements-dev.txt        # Dependências de desenvolvimento
├── .env.example                # Variáveis de ambiente exemplo
├── .python-version             # Versão do Python
├── .gitignore                  # Arquivos ignorados pelo git
├── pyproject.toml              # Configuração de ferramentas
└── README.md                   # Este arquivo
```

### ⚙️ Funcionalidades Pré-configuradas

- **✅ FastAPI** com configuração otimizada
- **✅ Injeção de Dependência** com dependency-injector
- **✅ Health Checks** automaticos (`/health`, `/ready`)
- **✅ Metrics Prometheus** pré-configuradas (`/metrics`)
- **✅ Logging Estruturado** com JSON formatting
- **✅ CORS** configurado
- **✅ Rate Limiting** básico
- **✅ Validation** com Pydantic v2

## 🚀 Como Usar Este Template

### Método 1: Via GitHub UI (Recomendado)

1. **Acesse o template**: [fc-service-template](https://github.com/personal-finance-control-app/fc-service-template)
2. **Clique em "Use this template"** → "Create a new repository"
3. **Configure o novo repositório**:
   - Owner: `personal-finance-control-app`
   - Repository name: `fc-{nome}-service`
   - Description: Microserviço para {funcionalidade}
   - ⚠️ **Marque "Public"**
4. **Adicione os tópicos**: `finance-control`, `microservice`, `python`

### Método 2: Via GitHub CLI

```bash
# Criar novo repositório a partir do template
gh repo create personal-finance-control-app/fc-{nome}-service \
  --template personal-finance-control-app/fc-service-template \
  --public \
  --description "Microserviço para {funcionalidade}" \
  --add-topic "finance-control" \
  --add-topic "microservice" \
  --add-topic "python"

# Clonar o novo repositório
gh repo clone personal-finance-control-app/fc-{nome}-service
cd fc-{nome}-service
```

### Método 3: Manual (Clone e Push)

```bash
# Clonar o template
git clone https://github.com/personal-finance-control-app/fc-service-template.git fc-{nome}-service
cd fc-{nome}-service

# Remover a conexão com o template
rm -rf .git
git init

# Configurar novo repositório remoto
git remote add origin https://github.com/personal-finance-control-app/fc-{nome}-service.git

# Primeiro commit
git add .
git commit -m "chore: initial commit from template"

# Push para o novo repositório
git branch -M main
git push -u origin main
```

## 🔧 Personalização do Novo Serviço

### 1. Configuração Básica

```bash
# Editar o arquivo de configuração principal
nano src/config.py

# Atualizar o nome do serviço
class Settings:
    SERVICE_NAME = "fc-{nome}-service"  # ← Alterar aqui
    VERSION = "1.0.0"
```

### 2. Variáveis de Ambiente

```bash
# Copiar arquivo de exemplo
cp .env.example .env

# Editar com configurações específicas
nano .env

# Configurações mínimas necessárias
SERVICE_NAME=fc-{nome}-service
PORT=8000
ENVIRONMENT=development
LOG_LEVEL=INFO
```

### 3. Dependências Específicas

```bash
# Editar requirements.txt para adicionar dependências únicas
nano requirements.txt

# Exemplo: adicionar dependência específica
# fastapi==0.104.1
# uvicorn==0.24.0
# pymongo==4.6.0  # ← Nova dependência
```

### 4. Configuração da API

```python
# Editar src/main.py para personalizar a API
app = FastAPI(
    title="FC {Nome} Service",  # ← Alterar aqui
    description="Microserviço para gerenciamento de {funcionalidade}",  # ← Alterar aqui
    version="1.0.0",
    docs_url="/docs",
    redoc_url="/redoc",
)
```

## 🧪 Desenvolvimento

### Executar Localmente

```bash
# Instalar dependências
pip install -r requirements-dev.txt

# Configurar variáveis de ambiente
cp .env.example .env

# Executar em modo desenvolvimento
uvicorn src.main:app --reload --port 8000
```

### Executar com Docker

```bash
# Build da imagem
docker build -t fc-{nome}-service .

# Executar container
docker run -p 8000:8000 --env-file .env fc-{nome}-service
```

### Testes

```bash
# Executar todos os testes
pytest

# Executar testes com coverage
pytest --cov=src --cov-report=html

# Executar testes específicos
pytest tests/unit/ -v
```

## 📡 API Endpoints Pré-configurados

- `GET /health` - Health check do serviço
- `GET /ready` - Readiness check
- `GET /metrics` - Métricas Prometheus
- `GET /docs` - Documentação Swagger/OpenAPI
- `GET /redoc` - Documentação Redoc

## 🔄 CI/CD Pipeline

O template inclui pipelines automatizados:

### CI Pipeline (.github/workflows/ci.yml)
- ✅ Linting com flake8 e black
- ✅ Type checking com mypy
- ✅ Testes unitários e de integração
- ✅ Coverage reporting
- ✅ Security scanning

### CD Pipeline (.github/workflows/cd.yml)
- ✅ Build da imagem Docker
- ✅ Push para GitHub Container Registry
- ✅ Deploy para Kubernetes (configurável)
- ✅ Rollback automático em caso de falha

## 🛡️ Segurança

Configurações de segurança incluídas:
- ✅ Rate limiting
- ✅ CORS configurado
- ✅ Security headers
- ✅ Input validation com Pydantic
- ✅ SQL injection protection
- ✅ Dependency scanning

## 📊 Monitoring

Métricas pré-configuradas:
- ✅ HTTP request metrics
- ✅ Database query metrics
- ✅ Error rates
- ✅ Response times
- ✅ Business metrics

## 🤝 Contribuindo para o Template

Para sugerir melhorias no template:

1. Fork este repositório
2. Crie uma branch para sua feature (`git checkout -b feature/improvement`)
3. Commit suas mudanças (`git commit -am 'Add some improvement'`)
4. Push para a branch (`git push origin feature/improvement`)
5. Abra um Pull Request

## 📝 Licença

Este projeto está licenciado sob a licença MIT - veja o arquivo [LICENSE](LICENSE) para detalhes.

## 🆘 Suporte

- 📚 [Documentação do Projeto](https://github.com/personal-finance-control-app/finance-control)
- 🐛 [Reportar Bug](https://github.com/personal-finance-control-app/fc-service-template/issues)
- 💡 [Sugerir Melhoria](https://github.com/personal-finance-control-app/fc-service-template/issues)
- 💬 [Discussions](https://github.com/personal-finance-control-app/finance-control/discussions)

---

**⭐ Gostou deste template? Deixe uma estrela no repositório!**

*Template mantido por [Finance Control Team](https://github.com/personal-finance-control-app)*
