# FastAPI Restaurantes

API REST construída com FastAPI que funciona como uma camada intermediária para dados de cardápio de redes de fast food. A aplicação busca informações de uma fonte externa e as disponibiliza através de endpoints próprios, com suporte a filtragem por restaurante.

---

## Endpoints

### `GET /api/hello`
Endpoint de healthcheck. Verifica se a aplicação está no ar.

**Resposta:**
```json
{
  "Hello": "world"
}
```

---

### `GET /api/restaurantes/`
Retorna o cardápio dos restaurantes. Suporta filtragem por nome do restaurante via query parameter.

**Parâmetros:**

| Parâmetro    | Tipo   | Obrigatório | Descrição                        |
|--------------|--------|-------------|----------------------------------|
| `restaurante`| string | Não         | Nome do restaurante para filtrar |

**Exemplo sem filtro:**
```
GET /api/restaurantes/
```
Retorna todos os itens de todos os restaurantes.

**Exemplo com filtro:**
```
GET /api/restaurantes/?restaurante=McDonald's
```
Retorna apenas o cardápio do restaurante especificado.

**Resposta:**
```json
[
  {
    "nome": "McDonald's",
    "item": "Big Mac",
    "preco": 25.90,
    "descricao": "Dois hambúrgueres, alface, queijo..."
  }
]
```

---

## Estrutura do Projeto

```
fastapi-venv/
├── main.py        # API principal com os endpoints FastAPI
├── app.py         # Script auxiliar para download e salvamento local dos dados
└── ...
```

> **Nota:** O `app.py` é um script independente que baixa os dados da API externa e os salva em arquivos `.json` separados por restaurante. Ele não interfere na execução da API principal.

---

## Como executar

### Pré-requisitos

- Python 3.8+
- pip

### Instalação

```bash
# Clone o repositório
git clone https://github.com/Dan1Ems/fastapi-venv.git
cd fastapi-venv

# Crie e ative o ambiente virtual
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# Instale as dependências
pip install fastapi uvicorn httpx
```

### Rodando a API

```bash
uvicorn main:app --reload
```

A API estará disponível em `http://localhost:8000`.

Documentação interativa (Swagger): `http://localhost:8000/docs`

---

## Fonte dos Dados

Os dados são obtidos em tempo real da API pública:

```
https://guilhermeonrails.github.io/api-restaurantes/restaurantes.json
```

A aplicação **não utiliza banco de dados** — todos os dados são processados em memória a cada requisição.

---

## Autenticação

Esta API não possui autenticação. Todos os endpoints são públicos.

---

## Tecnologias

- [FastAPI](https://fastapi.tiangolo.com/)
- [Uvicorn](https://www.uvicorn.org/)
- Python 3.8+
