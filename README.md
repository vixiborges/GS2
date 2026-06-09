# 🛰️ AgroSat — Previsão de Produtividade Agrícola com IA e Dados de Satélite

> **Global Solution 2025 — FIAP**  
> Como a Inteligência Artificial e as tecnologias digitais podem transformar a nova economia espacial e gerar impacto positivo na Terra?

---

## 👥 Integrantes

| Nome | RM |
|------|----|
| Gustavo Borges Marinho Peres | RM 567477 |

---

## 📌 Sobre o Projeto

O **AgroSat** é uma plataforma de monitoramento agrícola inteligente que combina **dados de satélite (NDVI)**, **informações climáticas** e **Machine Learning** para prever a produtividade de soja em estados brasileiros, gerando alertas automáticos sobre riscos climáticos como El Niño e secas.

### Problema
O agronegócio brasileiro — responsável por ~25% do PIB — sofre perdas bilionárias anuais por eventos climáticos extremos e dificuldade de acesso a previsões de produtividade confiáveis.

### Solução
Pipeline completo de dados espaciais + ML que transforma dados de satélite e clima em previsões acionáveis de produtividade, acessíveis via API REST e dashboard interativo.

---

## 🏗️ Arquitetura

```
🛰️ Satélite (NDVI)    🌦️ Clima (INMET)    📊 IBGE PAM
        │                     │                  │
        └─────────────────────┴──────────────────┘
                              │
                    📥 Data Pipeline (Python/Pandas)
                              │
                   ⚙️ Feature Engineering
                   (NDVI×Precip, El Niño, Estresse Hídrico)
                              │
                   🤖 Random Forest Regressor
                      (scikit-learn, 200 trees)
                              │
              ┌───────────────┴───────────────┐
              │                               │
      🌐 FastAPI REST API          ☁️ AWS S3 Simulado
      7 endpoints                  6 datasets/modelos
              │
      📊 Dashboard Streamlit
      Mapas · Gráficos · Previsões · Alertas
```

---

## 🚀 Como Executar

### Pré-requisitos
- Python 3.10+
- pip

### Instalação

```bash
# Clone o repositório
git clone [<url-do-repositorio>](https://github.com/vixiborges/GS2.git)
cd agrosat

# Instale as dependências
pip install -r requirements.txt
```

### Execução

```bash
# 1. Gerar os dados
python data/collect_data.py

# 2. Treinar o modelo
python models/train_model.py

# 3. Simular upload para AWS S3
python api/s3_simulation.py

# 4. Subir a API
uvicorn api.main:app --reload
# Acesse: http://localhost:8000/docs

# 5. Subir o Dashboard
streamlit run dashboard/app.py
# Acesse: http://localhost:8501
```

---

## 🛠️ Tecnologias

| Tecnologia | Uso |
|------------|-----|
| Python 3.10+ | Pipeline de dados, ML, API |
| Scikit-learn | Random Forest Regressor |
| FastAPI | API REST (7 endpoints) |
| Streamlit | Dashboard interativo |
| Plotly | Visualizações interativas |
| Pandas / NumPy | Manipulação de dados |
| Joblib | Persistência do modelo |
| Boto3 (simulado) | AWS S3 — armazenamento em nuvem |
| NDVI Copernicus | Dados de vegetação por satélite |
| IBGE PAM/SIDRA | Dados reais de produção agrícola |

---

## 📊 Resultados

- **10 estados** brasileiros monitorados
- **120 registros** históricos (2012–2023)
- **17 features** por registro
- **MAPE de 4.74%** (erro médio de previsão)
- **7 endpoints** REST disponíveis
- **5 páginas** de visualização no dashboard

---

## 📁 Estrutura do Repositório

```
agrosat/
├── data/
│   ├── collect_data.py        # Pipeline de coleta e geração de dados
│   ├── raw/                   # Dados brutos (NDVI, clima, produção)
│   └── processed/             # Dataset final consolidado
├── models/
│   ├── train_model.py         # Treinamento do modelo ML
│   ├── agrosat_model.pkl      # Modelo treinado (Random Forest)
│   └── model_metadata.json    # Métricas e metadata do modelo
├── api/
│   ├── main.py                # API FastAPI (7 endpoints)
│   └── s3_simulation.py       # Simulação AWS S3
├── dashboard/
│   └── app.py                 # Dashboard Streamlit
├── requirements.txt
└── README.md
```

---

## 🌍 Impacto

- Redução de perdas agrícolas por antecipação de riscos climáticos
- Democratização do acesso a dados de satélite para pequenos produtores
- Contribuição para segurança alimentar e sustentabilidade do agronegócio brasileiro
- Base para integração com sistemas de seguro agrícola e crédito rural
