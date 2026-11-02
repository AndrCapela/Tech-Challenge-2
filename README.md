# Web - Completo: Sistema de Otimização de Rotas Hospitalares (VRP) & Copiloto Gemini
### FIAP — Tech Challenge Fase 2 | Pós-Tech em IA para Devs

> **Autor:** André Capela (andr.capela@gmail.com)  
> **Vídeo no YouTube:** [https://youtu.be/d2x2oioqB9E](https://youtu.be/d2x2oioqB9E)  
> **Demonstração em Produção (VPS com SSL):** [https://app.143.95.175.167.nip.io](https://app.143.95.175.167.nip.io)  
> **Relatório Oficial de Entrega:** [`RELATORIO_TECNICO.docx`](RELATORIO_TECNICO.docx) | [`RELATORIO_TECNICO.md`](RELATORIO_TECNICO.md)

---

## 📋 Resumo desta Pasta

Esta pasta contém a **aplicação web completa de produção** do Tech Challenge da Fase 2, incluindo:
* **`web_app.py`**: Servidor Flask com endpoints REST, streaming *Server-Sent Events (SSE)* e exportação/download de arquivos JSON;
* **`templates/index.html`**: Interface gráfica moderna com Canvas 2D interativo (setas direcionais de fluxo de tráfego, cores exclusivas por veículo e halos de prioridade médica), gráfico de convergência Chart.js com eixos graduados, popover de auditoria de multas e navegação responsiva por abas para dispositivos móveis (*Mobile Tabs*);
* **`vrp_core.py`**: Núcleo desacoplado com as regras de negócio hospitalar, particionamento de frota heterogênea (`split_route_into_vehicles`) e função fitness multicritério com as 3 penalidades (Prioridade Clínica, Carga em kg e Autonomia);
* **`route_optimizer_dispatcher.py`**: Orquestrador que injeta os parâmetros e penalidades da interface e invoca o algoritmo selecionado;
* **`genetic_algorithm.py`**: Algoritmo Genético evolucionário (Torneio $k=4$, Roleta Inversa $1/\text{Fitness}$, Order Crossover OX1 e Mutação Híbrida 2-opt/Swap/Crítico);
* **`algo_*.py`**: 4 algoritmos comparativos (Ant Colony ACO, Simulated Annealing SA, Nearest Neighbor NN e Convex Hull CH);
* **`llm_driver_assistant.py`**: Assistente Copiloto integrado à API do Google Gemini (`gemini-3-flash-preview`) com grounding automático da rota via [`melhor_rota_hospitalar.json`](melhor_rota_hospitalar.json);
* **`test_vrp_system.py`**: Suíte de testes unitários automatizados cobrindo 100% das regras e endpoints;
* **`Dockerfile` & `docker-compose.yml`**: Configurações de conteinerização com servidor WSGI Gunicorn para deploy de alta disponibilidade.

---

## ⚡ Como Executar

### 1. Execução Local com Python
```bash
# 1. Ativar o ambiente virtual
# Windows:
..\..\..\.venv\Scripts\activate
# Linux/macOS:
source ../../../.venv/bin/activate

# 2. Instalar dependências
pip install -r requirements.txt

# 3. Configurar a chave do Gemini
cp .env.example .env
# Preencha a variável GEMINI_API_KEY no arquivo .env

# 4. Iniciar o servidor
python web_app.py
```
Acesse em: `http://localhost:5000`

### 2. Execução com Docker Compose
```bash
docker compose up -d --build
```
Acesse em: `http://localhost:5000`

### 3. Execução dos Testes Automatizados
```bash
python -m unittest test_vrp_system.py -v
```

---

Para a documentação completa, consulte o arquivo [`OVERVIEW_PROJETO.md`](OVERVIEW_PROJETO.md) e o [`RELATORIO_TECNICO.md`](RELATORIO_TECNICO.md).
