# Todo API

Uma API REST simples para gerenciamento de tarefas (To-Do List) desenvolvida em Django com Django REST Framework e MySQL.

## 📋 Funcionalidades

- ✅ Listar todas as tarefas
- ✅ Criar nova tarefa
- ✅ Visualizar detalhes de uma tarefa específica
- ✅ Atualizar tarefa existente
- ✅ Excluir tarefa
- ✅ Marcar tarefa como completa/incompleta

## 🛠️ Tecnologias Utilizadas

- **Python 3.x**
- **Django 5.2.4**
- **Django REST Framework**
- **MySQL 8.0**
- **Docker & Docker Compose**

## 📁 Estrutura do Projeto

```
todo_api/
├── docker-compose.yml
├── manage.py
├── popular_DB.sql
├── tasks/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── serializers.py
│   ├── tests.py
│   ├── urls.py
│   ├── views.py
│   └── migrations/
│       ├── __init__.py
│       └── 0001_initial.py
└── todo_api/
    ├── __init__.py
    ├── asgi.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

## 🚀 Como Executar

### Pré-requisitos

- Docker
- Docker Compose
- Python 3.x (opcional, se não usar Docker)

### Usando Docker (Recomendado)

1. **Clone o repositório**
```bash
git clone <url-do-repositorio>
cd todo_api
```

2. **Inicie o banco de dados MySQL**
```bash
docker-compose up -d
```

3. **Instale as dependências Python**
```bash
pip install django djangorestframework mysqlclient
```

4. **Execute as migrações**
```bash
python manage.py makemigrations
python manage.py migrate
```

5. **Popule o banco com dados de exemplo (opcional)**
```bash
# Acesse o MySQL e execute o arquivo popular_DB.sql
# Certifique-se de ajustar o nome da tabela para tasks_task
```

6. **Inicie o servidor Django**
```bash
python manage.py runserver
```

### Instalação Local (sem Docker)

1. **Instale e configure o MySQL**
```bash
# Crie um banco de dados chamado 'todo_db'
# Crie um usuário 'user' com senha '123456'
```

2. **Instale as dependências**
```bash
pip install django djangorestframework mysqlclient
```

3. **Execute as migrações**
```bash
python manage.py makemigrations
python manage.py migrate
```

4. **Inicie o servidor**
```bash
python manage.py runserver
```

## 📡 Endpoints da API

### Base URL
```
http://localhost:8000/api/
```

### Endpoints Disponíveis

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| GET | `/api/tasks/` | Lista todas as tarefas |
| POST | `/api/tasks/` | Cria uma nova tarefa |
| GET | `/api/tasks/{id}` | Busca uma tarefa específica |
| PUT | `/api/tasks/{id}` | Atualiza uma tarefa específica |
| DELETE | `/api/tasks/{id}` | Remove uma tarefa específica |

## 📝 Exemplos de Uso

### Listar todas as tarefas
```bash
curl -X GET http://localhost:8000/api/tasks/
```

### Criar nova tarefa
```bash
curl -X POST http://localhost:8000/api/tasks/ \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Estudar Django",
    "description": "Aprender sobre Models, Views e Templates",
    "completed": false
  }'
```

### Buscar tarefa específica
```bash
curl -X GET http://localhost:8000/api/tasks/1
```

### Atualizar tarefa
```bash
curl -X PUT http://localhost:8000/api/tasks/1 \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Estudar Django - Concluído",
    "description": "Aprender sobre Models, Views e Templates",
    "completed": true
  }'
```

### Excluir tarefa
```bash
curl -X DELETE http://localhost:8000/api/tasks/1
```

## 🗃️ Modelo de Dados

### Task
```python
class Task(models.Model):
    title = models.CharField(max_length=200)
    description = models.TextField(blank=True)
    completed = models.BooleanField(default=False)
```

**Campos:**
- `id`: Identificador único (auto-incremento)
- `title`: Título da tarefa (obrigatório, máx. 200 caracteres)
- `description`: Descrição detalhada (opcional)
- `completed`: Status de conclusão (padrão: false)

## ⚙️ Configurações

### Banco de Dados
O projeto está configurado para usar MySQL com as seguintes credenciais:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'todo_db',
        'USER': 'user',
        'PASSWORD': '123456',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

### Docker Compose
O arquivo `docker-compose.yml` configura automaticamente:
- MySQL 8.0
- Banco de dados `todo_db`
- Usuário `user` com senha `123456`
- Porta 3306 exposta

## 🧪 Testes

Para executar os testes:

```bash
python manage.py test
```

## 📊 Dados de Exemplo

O arquivo `popular_DB.sql` contém dados de exemplo para popular o banco:

```sql
INSERT INTO tasks_task (title, description, completed) VALUES
('Organizar arquivos', 'Separar documentos importantes em pastas digitais', false),
('Estudar Django', 'Revisar Models, Views e Templates', false),
('Fazer backup', 'Criar backup dos projetos atuais no drive externo', true),
-- ... mais dados
```

## 🔧 Troubleshooting

### Erro de Conexão com MySQL
- Verifique se o MySQL está rodando: `docker-compose ps`
- Confirme as credenciais no arquivo `settings.py`
- Aguarde alguns segundos após iniciar o container do MySQL

### Erro de Migração
```bash
python manage.py makemigrations tasks
python manage.py migrate
```

### Tabela não encontrada
Certifique-se de que as migrações foram executadas corretamente e que o nome da tabela no SQL seja `tasks_task`.

## 🤝 Contribuindo

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/AmazingFeature`)
3. Commit suas mudanças (`git commit -m 'Add some AmazingFeature'`)
4. Push para a branch (`git push origin feature/AmazingFeature`)
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.

## 📞 Contato

Para dúvidas ou sugestões, entre em contato através do GitHub Issues.

---

**Desenvolvido com ❤️ usando Django e Django REST Framework**
