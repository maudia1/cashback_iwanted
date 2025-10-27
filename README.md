Cashback CRM (FastAPI)

Como iniciar

- Criar o ambiente e instalar dependÃªncias (jÃ¡ feito na primeira execuÃ§Ã£o):
  - `py -m venv venv`
  - `venv\Scripts\pip install -U pip`
  - `venv\Scripts\pip install fastapi uvicorn[standard] jinja2 sqlalchemy pydantic-settings python-multipart`

- Rodar o servidor:
  - `venv\Scripts\uvicorn app.main:app --reload`
  - Abrir `http://127.0.0.1:8000`

Estrutura

- `app/main.py` â€“ rotas e views
- `app/models.py` â€“ modelos SQLAlchemy (Store, Employee, Sale)
- `app/db.py` â€“ criaÃ§Ã£o do SQLite e sessÃ£o
- `app/templates/` â€“ pÃ¡ginas Jinja2
- `app/static/style.css` â€“ estilos do formulÃ¡rio
- `uploads/` â€“ onde os PDFs enviados sÃ£o salvos

Fluxo de uso

- Preencha o formulÃ¡rio e envie.
- O sistema salva o registro e mostra um botÃ£o â€œEnviar via WhatsAppâ€.
- O link abre a conversa com o texto preenchido. Anexe o PDF manualmente (o link nÃ£o envia anexos pelo WhatsApp Web/API sem provedor).

ObservaÃ§Ãµes

- Os dados de lojas e colaboradores iniciais sÃ£o criados automaticamente (seed simples).
- Para personalizar lojas/colaboradores, ajuste diretamente em `init_db()` dentro de `app/main.py` ou expanda com rotas de cadastro.


Deploy em VPS (Docker)

1) Copie o projeto para a VPS (scp, git clone ou upload).
2) Na pasta do projeto, rode:
   - docker build -t cashback-app .
   - docker compose up -d

Detalhes:
- O serviço expõe a app em http://SEU_IP:80 (mapeia 80->8000).
- O banco SQLite fica em ./data/cashback.db (volume montado em /data).
- Os uploads ficam em ./uploads (volume montado em /app/uploads).
- Variáveis importantes: DB_PATH=/data/cashback.db (já configurada no compose).

Para atualizar a versão:
- docker compose pull (se usar image) ou docker compose build --no-cache
- docker compose up -d

Logs e status:
- docker compose logs -f
- docker compose ps
