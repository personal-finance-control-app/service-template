# 📋 Service Template

![Finance Control](https://img.shields.io/badge/Project-Finance%20Control-blue)
![Template](https://img.shields.io/badge/Type-Template-yellow)
![Python](https://img.shields.io/badge/Python-3.11%2B-green)
![FastAPI](https://img.shields.io/badge/Framework-FastAPI-009688)
![Status](https://img.shields.io/badge/Status-✅_Active-brightgreen)
![Version](https://img.shields.io/badge/Version-1.0.0-blue)

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## 🏗️ Estrutura do Projeto (Nova Organização)

```
service-template/
├── .github/
│   └── workflows/
│       ├── ci.yml              # Pipeline de integração contínua
│       ├── cd.yml              # Pipeline de deploy contínuo
│       └── codeql-analysis.yml # Análise de segurança CodeQL
├── app/
│   ├── application/
│   │   ├── __init__.py
│   │   ├── dto.py              # Data Transfer Objects
│   │   └── use_cases.py        # Casos de uso da aplicação
│   ├── domain/
│   │   ├── controllers/
│   │   │   ├── __init__.py
│   │   │   └── teste_controller.py
│   │   ├── entities/
│   │   │   └── __init__.py
│   │   ├── enums/
│   │   │   └── __init__.py
│   │   ├── models/
│   │   │   ├── __init__.py
│   │   │   └── __init__.py
│   │   ├── repository/
│   │   │   ├── __init__.py
│   │   │   └── __init__.py
│   │   ├── services/
│   │   │   ├── __init__.py
│   │   │   └── example_service.py
│   │   └── __init__.py
│   ├── infrastructure/
│   │   ├── api/
│   │   │   └── __init__.py
│   │   ├── database.py         # Configuração do banco de dados
│   │   └── __init__.py
│   ├── page/
│   │   └── __init__.py
│   ├── utils/
│   │   ├── __init__.py
│   │   ├── constants.py        # Constantes do projeto
│   │   └── files.py            # Utilitários para manipulação de arquivos
│   ├── __init__.py
│   ├── config.py               # Configurações da aplicação
│   └── container.py            # Injeção de dependências
├── tests/
│   ├── integration/            # Testes de integração
│   ├── unit/                   # Testes unitários
│   ├── __init__.py
│   └── conftest.py             # Configuração do pytest
├── logging.ini                 # Configuração de logging (INI)
├── logging.json                # Configuração de logging (JSON)
├── .dockerignore
├── .env.example                # Variáveis de ambiente exemplo
├── .gitignore
├── Dockerfile                  # Configuração Docker
├── README.md                   # Documentação
└── requirements.txt            # Dependências do projeto
```

## 🎯 Camadas da Arquitetura

### 1. **Domain Layer** (`app/domain/`)
- **Entities**: Entidades de domínio e modelos de dados
- **Enums**: Definições de enumeradores
- **Repository**: Interfaces para acesso a dados
- **Services**: Lógica de negócio central
- **Controllers**: Controladores de domínio

### 2. **Application Layer** (`app/application/`)
- **DTOs**: Objetos de transferência de dados
- **Use Cases**: Casos de uso da aplicação

### 3. **Infrastructure Layer** (`app/infrastructure/`)
- **API**: Configurações e rotas da API
- **Database**: Configuração de banco de dados

### 4. **Utils** (`app/utils/`)
- **Constants**: Constantes do projeto
- **Files**: Utilitários para manipulação de arquivos

## 🚀 Como Usar Este Template

### Método Recomendado: Via GitHub Template

```bash
# Criar novo repositório a partir do template
gh repo create finance-control-app/meu-novo-service \
  --template finance-control-app/service-template \
  --public \
  --description "Meu novo microserviço" \
  --add-topic "finance-control" \
  --add-topic "microservice"

# Clonar o novo repositório
gh repo clone finance-control-app/meu-novo-service
cd meu-novo-service
```

### Personalização do Novo Serviço

```bash
# 1. Atualizar configurações básicas
nano app/config.py

# 2. Configurar variáveis de ambiente
cp .env.example .env
nano .env

# 3. Atualizar dependências
nano requirements.txt

# 4. Personalizar entidades de domínio
nano app/domain/models/__init__.py

# 5. Configurar serviços de domínio
nano app/domain/services/example_service.py
```

## ⚙️ Configuração Rápida

```bash
# Instalar dependências
pip install -r requirements.txt

# Configurar ambiente
cp .env.example .env
# Editar .env com suas configurações

# Executar em modo desenvolvimento
uvicorn app.infrastructure.api:app --reload --port 8000
```

## 🧪 Executando Testes

```bash
# Executar todos os testes
pytest tests/ -v

# Executar apenas testes unitários
pytest tests/unit/ -v

# Executar apenas testes de integração
pytest tests/integration/ -v

# Executar com coverage
pytest --cov=app --cov-report=html
```

## 📦 Deploy com Docker

```bash
# Build da imagem
docker build -t meu-servico .

# Executar container
docker run -p 8000:8000 --env-file .env meu-servico
```

## 🔧 Principais Arquivos de Configuração

### `app/config.py`
```python
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    SERVICE_NAME: str = "meu-servico"
    VERSION: str = "1.0.0"
    ENVIRONMENT: str = "development"
    DATABASE_URL: str
    # Adicione outras configurações necessárias
```

### `app/container.py`
```python
from dependency_injector import containers, providers
from .config import Settings

class Container(containers.DeclarativeContainer):
    config = providers.Configuration()
    
    # Registrar serviços e repositórios aqui
    example_service = providers.Factory(
        ExampleService
    )
```

### `app/infrastructure/api/__init__.py`
```python
from fastapi import FastAPI
from app.container import container

app = FastAPI(
    title=container.config.SERVICE_NAME,
    version=container.config.VERSION
)

# Registrar rotas e middlewares aqui
```

## 🛠️ Implementando um Novo Serviço

### 1. Definir Entidades (`app/domain/models/__init__.py`)
```python
from pydantic import BaseModel

class User(BaseModel):
    id: int
    name: str
    email: str
```

### 2. Criar Serviço de Domínio (`app/domain/services/`)
```python
class UserService:
    async def create_user(self, user_data: dict):
        # Lógica de negócio aqui
        return user_data
```

### 3. Implementar Controlador (`app/domain/controllers/`)
```python
from fastapi import APIRouter
from app.domain.services import UserService

router = APIRouter()

@router.post("/users")
async def create_user(user_data: dict):
    service = UserService()
    return await service.create_user(user_data)
```

### 4. Registrar Rota (`app/infrastructure/api/__init__.py`)
```python
from app.domain.controllers import user_controller

app.include_router(user_controller.router, prefix="/api/v1")
```

## 📊 Health Checks e Monitoramento

O template inclui endpoints pré-configurados:

- `GET /health` - Health check do serviço
- `GET /metrics` - Métricas Prometheus
- `GET /docs` - Documentação Swagger automática

## 🔒 Segurança

Configurações de segurança incluídas:
- ✅ CORS configurado
- ✅ Rate limiting
- ✅ Validation com Pydantic v2
- ✅ Environment variables para dados sensíveis

## 📝 Licença

MIT License - veja [LICENSE](LICENSE) para detalhes.

---

**⭐ Gostou deste template? Deixe uma estrela no repositório!**

*Template mantido por [Finance Control Team](https://github.com/finance-control-app)*