# Sistema de Gerenciamento de Monitorias

<div align="center">

**Uma plataforma web centralizada para gerenciar vagas de monitoria, conectando alunos, professores e coordenadores.**

[![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Django](https://img.shields.io/badge/Django-REST-green?logo=django&logoColor=white)](https://www.djangoproject.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

</div>

---

## 📋 Sobre o Projeto

Uma aplicação backend desenvolvida para **gerenciar de forma centralizada e eficiente** as atividades de monitoria em instituições de ensino. O sistema permite:

- 📝 **Controle de Vagas**: Professores criam e gerenciam vagas de monitoria
- 👥 **Candidaturas**: Alunos se candidatam e acompanham suas aplicações
- 📊 **Relatórios**: Visualização consolidada de atividades e desempenho
- 🔐 **Gestão de Acesso**: Diferentes perfis de usuário com permissões específicas
- ✅ **Sistema de Aprovação**: Análise e aprovação de candidaturas

**Disciplina**: IBM8936 | **Instituição**: IBMEC

---

## 👥 Equipe

| Nome | Matrícula |
|------|-----------|
| Arthur Riess | 202407096026 |
| Yago Carvalho | 202407095781 |
| Felipe Maia | 202408474474 |
| Pedro Macedo | 202401318728 |

---

## 🚀 Quick Start

### Pré-requisitos

- **Python** 3.8 ou superior
- **pip** (gerenciador de pacotes Python)
- **Git**

### 1. Clonar o Repositório

```bash
git clone https://github.com/seu-usuario/backend-django.git
cd backend-django
```

### 2. Criar Ambiente Virtual

```bash
# No Windows
python -m venv venv
venv\Scripts\activate

# No macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### 3. Instalar Dependências

```bash
pip install -r requirements.txt
```

### 4. Configurar Banco de Dados

```bash
# Executar migrações
python manage.py migrate

# Criar superusuário (administrador)
python manage.py createsuperuser
```

### 5. Executar o Servidor

```bash
python manage.py runserver
```

A aplicação estará disponível em: **http://127.0.0.1:8000/**
Admin em: **http://127.0.0.1:8000/admin/**

---

## 📁 Estrutura do Projeto

```
backend-django/
├── config/                 # Configurações do Django
│   ├── settings.py        # Variáveis de ambiente e apps
│   ├── urls.py            # URLs principais
│   └── wsgi.py           # Servidor WSGI
├── core/                   # Aplicação principal
│   ├── models.py          # Modelos (Professor, Aluno, Vaga, Candidatura)
│   ├── views.py           # Visualizações e lógica de negócio
│   ├── serializers.py     # Serializadores para API REST
│   ├── permissions.py     # Permissões customizadas
│   ├── api.py             # Endpoints da API
│   ├── urls.py            # URLs da aplicação
│   └── migrations/        # Histórico de migrações do banco
├── templates/             # Templates HTML
├── docs/                  # Documentação do projeto
├── requirements.txt       # Dependências do projeto
└── manage.py             # CLI do Django
```

---

## 🔧 Modelos Principais

### Professor
```python
- user (OneToOneField)
- cpf
- telefone
- disciplinas (relacionado)
- vagas_criadas (relacionado)
```

### Aluno
```python
- user (OneToOneField)
- matrícula
- cpf
- crgeral (coeficiente de rendimento)
- curso
- período
- telefone
- candidaturas (relacionado)
```

### Vaga
```python
- nome
- disciplina (ForeignKey)
- professor (ForeignKey)
- crminimo (CR mínimo exigido)
- status (aberta/fechada)
- descricao
- candidaturas (relacionado)
```

### Candidatura
```python
- aluno (ForeignKey)
- vaga (ForeignKey)
- documento (FileField - opcional)
- data_candidatura (auto_now_add)
- status (pendente/aprovada/rejeitada)
```

---

## 🔌 API Endpoints

A aplicação oferece uma API REST para acesso aos dados:

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/api/vagas/` | Lista todas as vagas |
| GET | `/api/vagas/{id}/` | Detalhe de uma vaga |
| POST | `/api/candidaturas/` | Criar nova candidatura |
| GET | `/api/candidaturas/` | Listar candidaturas do usuário |
| PUT | `/api/candidaturas/{id}/` | Atualizar candidatura |

---

## 📦 Dependências Principais

- **Django** - Framework web
- **Django REST Framework** - Para criar a API REST
- **Pillow** - Processamento de imagens
- **python-dateutil** - Manipulação de datas
- **Markdown** - Processamento de documentação
- **MkDocs** - Gerador de documentação

Veja [requirements.txt](requirements.txt) para a lista completa.

---

## 🛠️ Comandos Úteis

```bash
# Criar nova aplicação Django
python manage.py startapp nome_app

# Fazer migrações após alterar models
python manage.py makemigrations
python manage.py migrate

# Acessar shell interativo do Django
python manage.py shell

# Executar testes
python manage.py test

# Coletar arquivos estáticos
python manage.py collectstatic

# Ver URLs cadastradas
python manage.py show_urls
```

---

## 🧪 Testes

```bash
# Executar todos os testes
python manage.py test

# Executar testes de uma app específica
python manage.py test core

# Com saída verbosa
python manage.py test --verbosity=2
```

---

## 📚 Documentação

Documentação completa do projeto em [docs/](docs/):
- [Documento de Visão](docs/Iniciacao/documento_de_visao.md)
- [Casos de Uso](docs/Elaboracao/casos_de_uso.md)
- [Diagrama de Classes](docs/Elaboracao/diagrama_de_classes.md)
- [Requisitos](docs/Elaboracao/requisitos.md)

Para gerar documentação localmente:
```bash
pip install mkdocs mkdocs-material
mkdocs serve
```

---

## 🔐 Variáveis de Ambiente

Crie um arquivo `.env` na raiz do projeto (não commitar):

```env
SECRET_KEY=sua-chave-secreta-aqui
DEBUG=False
ALLOWED_HOSTS=localhost,127.0.0.1
DATABASE_URL=sqlite:///db.sqlite3
```

---

## 🐛 Troubleshooting

### Erro: "ModuleNotFoundError"
```bash
# Certifique-se que o ambiente virtual está ativado
# Windows: venv\Scripts\activate
# macOS/Linux: source venv/bin/activate

# Reinstale as dependências
pip install -r requirements.txt
```

### Erro de Migração
```bash
# Reset do banco (cuidado: apaga dados)
python manage.py migrate core zero
python manage.py migrate
```

---

## 📝 Contribuindo

1. Faça um Fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/MinhaFeature`)
3. Commit suas mudanças (`git commit -m 'Add MinhaFeature'`)
4. Push para a branch (`git push origin feature/MinhaFeature`)
5. Abra um Pull Request

---

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

## 📧 Contato

Para dúvidas ou sugestões sobre o projeto, abra uma issue no repositório.

---

**Desenvolvido para a disciplina IBM8936 - IBMEC**
