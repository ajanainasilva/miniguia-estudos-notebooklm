# Performance Engineering: JMeter & K6 com IA Aplicada

![Apache JMeter](https://img.shields.io/badge/Apache%20JMeter-D22128?style=for-the-badge&logo=Apache%20JMeter&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![k6](https://img.shields.io/badge/k6-7D64FF?style=for-the-badge&logo=k6&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![CI/CD](https://img.shields.io/badge/CI/CD_Ready-Performance_as_Code-2088FF?style=for-the-badge)
![NotebookLM](https://img.shields.io/badge/AI_Aided-NotebookLM-0052CC?style=for-the-badge)

> **Sobre este projeto:** Repositório de estudo prático sobre **Engenharia de Testes de Performance**, desenvolvido com foco em aplicabilidade real em pipelines de CI/CD e ambientes de produção. Utilizei o **Google NotebookLM** como ferramenta auxiliar para estruturar conceitos técnicos, comparar arquiteturas de ferramentas e simular cenários de falha em sistemas sob carga. Projeto originado do desafio da DIO.

---

## 📑 Índice

1. [Contexto e Motivação Técnica](#-1-contexto-e-motivação-técnica)
2. [Fontes e Curadoria de Conhecimento](#-2-fontes-e-curadoria-de-conhecimento)
3. [Processo de Aprendizado com IA (Engenharia de Prompts)](#-3-processo-de-aprendizado-com-ia-engenharia-de-prompts)
4. [Guia Prático de Implementação](#-4-guia-prático-de-implementação)
5. [Estrutura do Repositório](#-5-estrutura-do-repositório)
6. [Próximos Passos](#-6-próximos-passos)

---

## 🎯 1. Contexto e Motivação Técnica

Testes de performance são uma das disciplinas mais negligenciadas no ciclo de vida de software, e também uma das mais críticas. Sistemas que passam em todos os testes funcionais podem falhar catastroficamente sob carga real. Este projeto nasce da compreensão de que **qualidade não é só ausência de bugs: é comportamento previsível sob condições adversas**.

### Por que esse tema importa para QA?

- **Shift-Left Testing:** Identificar gargalos de performance nas fases iniciais do desenvolvimento reduz drasticamente o custo de correção e aumenta a confiança do time nos deploys.
- **Integração com DevOps/SRE:** Testes de performance como parte do pipeline de CI/CD transformam qualidade em um processo contínuo, e não uma fase isolada.
- **Impacto direto no negócio:** Latência elevada causa abandono de usuários, perda de receita e degradação de SLAs.

### Ferramentas Estudadas

| Ferramenta | Modelo de Concorrência | Ideal Para |
|---|---|---|
| **Apache JMeter** | Threads Java (1 thread = 1 usuário virtual) | Protocolos variados, integrações complexas, times familiarizados com Java |
| **Grafana K6** | Goroutines em Go (leve, eficiente) | "Performance as Code", pipelines de CI/CD, times com perfil dev |

A diferença arquitetural importa: JMeter consome significativamente mais memória RAM por usuário virtual que o K6. Em simulações de **10.000 usuários simultâneos**, essa distinção define se o teste é viável na infraestrutura disponível.

### Tipos de Teste Abordados

- **Carga (Load):** Valida o comportamento do sistema no volume esperado de uso.
- **Estresse (Stress):** Identifica o ponto de ruptura da aplicação além do limite nominal.
- **Resistência (Soak/Endurance):** Detecta vazamentos de memória e degradação progressiva em execuções longas.
- **Pico (Spike):** Simula aumentos abruptos de tráfego (campanhas, viralização, black friday).

---

## 📚 2. Fontes e Curadoria de Conhecimento

A base técnica deste estudo foi construída priorizando **fontes primárias** (documentações oficiais) sobre conteúdo secundário, garantindo precisão arquitetural.

### Documentação Oficial

| Fonte | Foco |
|---|---|
| [Apache JMeter User Manual](https://jmeter.apache.org/usermanual/index.html) | Thread Groups, Web Test Plans, Listeners |
| [JMeter Best Practices](https://jmeter.apache.org/usermanual/best-practices.html) | Execução headless, tuning de JVM, otimização |
| [Grafana K6 Docs](https://docs.k6.io/docs) | Ciclo de vida de scripts, Thresholds, métricas |
| [BlazeMeter Blog](https://www.blazemeter.com/blog) | CI/CD integration, arquitetura de performance distribuída |

### Material Audiovisual

- 🎥 [Introdução aos testes de performance com K6](https://youtu.be/Azv3jxXkKeY)
- 🎥 [Testes de Performance com Grafana K6](https://youtu.be/9yRFhwBS0-8)
- 🎥 [Seu primeiro teste de carga com JMeter](https://youtu.be/-ytsCovAEhk)
- 🎥 [Testes de Stress com K6 e Grafana](https://youtu.be/66--zuutGiQ)

---

## 🧠 3. Processo de Aprendizado com IA (Engenharia de Prompts)

Um dos diferenciais deste projeto foi o uso intencional do **Google NotebookLM** para acelerar a curva de aprendizado em tópicos técnicos densos. O processo não foi passivo: cada prompt foi refinado iterativamente até produzir conhecimento aplicável.

### Registro de Iterações (Prompts → Aprendizados)

| Prompt Inicial | Objetivo | Refinamento e Resultado |
|:---|:---|:---|
| *"Crie um roteiro de estudos comparando JMeter e K6."* | Visão arquitetural geral | Resposta inicial genérica. Refinei para: *"Compare o consumo de recursos simulando 10k usuários: Threads Java vs Goroutines em Go."* — obtive dados concretos e comparáveis. |
| *"Explique o conceito de Thresholds no K6."* | Automatizar critérios de aceite em CI/CD | A IA trouxe apenas sintaxe. Refinei para: *"Gere um Threshold que quebre a pipeline se o P95 ultrapassar 500ms."* — obtive um exemplo diretamente aplicável. |
| *"Como evitar que o JMeter trave em testes de alto volume?"* | Boas práticas de infraestrutura | Resultado direto: uso obrigatório do modo CLI (Non-GUI), desativação de Listeners visuais e tuning de heap da JVM (`-Xms` / `-Xmx`). |

> **Lição aprendida:** IA como ferramenta de estudo exige que o engenheiro já tenha hipóteses e perguntas formuladas. Prompts vagos geram respostas rasas; prompts com contexto técnico geram conhecimento acionável.

---

## 📝 4. Guia Prático de Implementação

### Workflow do Engenheiro de Performance

```
1. MODELAGEM        → Mapeie as jornadas críticas (Login, Checkout, Busca, API principal)
2. SETUP BASE       → Defina VUs ou Thread Groups, tempos de ramp-up e duração
3. EXECUÇÃO CLEAN   → Rode via CLI para eliminar overhead da GUI (falsos positivos)
4. ANÁLISE          → Cruze Throughput (RPS) + Latência (P90/P95/P99) + Taxa de Erros (HTTP 5xx)
5. DECISÃO          → Compare métricas com SLOs definidos — passa ou falha a pipeline?
```

### Exemplo Prático: K6 com Thresholds (Critério de Aceite Automatizado)

O script abaixo demonstra o conceito de **"Performance as Code"**: os critérios de qualidade estão no código, versionados junto com a aplicação, e podem quebrar uma pipeline automaticamente.

```javascript
import http from 'k6/http';
import { check, sleep } from 'k6';

export const options = {
  stages: [
    { duration: '30s', target: 50 },  // Ramp-up: 0 → 50 VUs em 30s
    { duration: '1m',  target: 50 },  // Carga sustentada: 50 VUs por 1 minuto
    { duration: '20s', target: 0  },  // Ramp-down: 50 → 0 VUs em 20s
  ],
  thresholds: {
    // SLOs: critérios de aceite — falha aqui = quebra de pipeline
    http_req_duration: ['p(95)<200'],  // 95% das requisições < 200ms
    http_req_failed:   ['rate<0.01'],  // Taxa de erros < 1%
  },
};

export default function () {
  const res = http.get('https://test-api.k6.io/public/crocodiles/');

  check(res, {
    'status 200 OK':           (r) => r.status === 200,
    'response time aceitável': (r) => r.timings.duration < 200,
  });

  sleep(1); // Think time: simula comportamento humano entre requests
}
```

**Por que isso é relevante para QA?**
- Os `thresholds` são SLOs (Service Level Objectives) explícitos no código
- O script é versionável, revisável e executável em qualquer ambiente com K6 instalado
- O resultado é binário e auditável: **PASS** ou **FAIL** — ideal para gates de qualidade em CI/CD

### Boas Práticas Consolidadas

**JMeter:**
- ✅ Sempre execute em modo CLI (`jmeter -n -t test.jmx -l results.jtl`)
- ✅ Desative todos os Listeners visuais durante a execução — eles consomem recursos e distorcem métricas
- ✅ Configure o heap da JVM adequadamente: `-Xms1g -Xmx4g` no `jmeter.bat/sh`
- ❌ Nunca rode testes de carga pesados pela GUI

**K6:**
- ✅ Use `stages` para ramp-up gradual — picos abruptos mascaram o comportamento real
- ✅ Defina `thresholds` sempre — sem critério de aceite, não há "teste", há apenas "medição"
- ✅ Integre com Grafana + InfluxDB para dashboards em tempo real em testes longos

---

## 📁 5. Estrutura do Repositório

```
📁 performance-engineering/
│
├── 📁 jmeter/
│   ├── 📁 test-plans/        → Planos de teste (.jmx)
│   ├── 📁 results/           → Resultados brutos (.jtl)
│   └── 📁 reports/           → Relatórios HTML gerados pelo JMeter
│
├── 📁 k6/
│   ├── 📁 scripts/
│   │   ├── load-test.js      → Carga sustentada (uso esperado)
│   │   ├── stress-test.js    → Estresse até ponto de ruptura
│   │   └── spike-test.js     → Pico abrupto de tráfego
│   └── 📁 thresholds/        → SLOs reutilizáveis entre scripts
│
├── 📁 docs/
│   └── analise-comparativa.md → JMeter vs K6: dados e conclusões
│
└── 📄 README.md
```

**Navegação rápida pelas seções deste documento:**

- [Contexto e Motivação Técnica](#-1-contexto-e-motivação-técnica)
- [Fontes e Curadoria de Conhecimento](#-2-fontes-e-curadoria-de-conhecimento)
- [Processo de Aprendizado com IA](#-3-processo-de-aprendizado-com-ia-engenharia-de-prompts)
- [Guia Prático de Implementação](#-4-guia-prático-de-implementação)
- [Próximos Passos](#-6-próximos-passos)

---

## 🔭 6. Próximos Passos

- [ ] **Integração CI/CD:** Configurar execução automática dos scripts K6 em GitHub Actions com gate de qualidade (falha de build se Threshold for violado)
- [ ] **Testes distribuídos com JMeter:** Configurar arquitetura Controller + Workers para simular carga geograficamente distribuída
- [ ] **Observabilidade:** Integrar K6 com Grafana + InfluxDB para dashboards em tempo real
- [ ] **Cenários realistas:** Modelar jornadas com autenticação, correlação de sessões e dados dinâmicos (CSV Data Set no JMeter / SharedArray no K6)
- [ ] **Análise de root cause:** Correlacionar métricas de performance com logs de APM (ex: New Relic, Datadog) para identificar gargalos na camada de aplicação vs infraestrutura

---

## 🏁 Conclusão

Este projeto representa mais do que o aprendizado de duas ferramentas. Representa a compreensão de que **qualidade de software é sistêmica**: envolve antecipar riscos, medir com precisão, estabelecer critérios objetivos de aceite e integrar essa cultura no fluxo de desenvolvimento.

Testes de performance feitos corretamente não são uma fase final — são uma prática contínua que protege tanto a experiência do usuário quanto a estabilidade operacional do negócio.

---

*Projeto desenvolvido como parte do desafio da [DIO](https://www.dio.me/bootcamp/ci-t-do-prompt-ao-agente). Contribuições e feedbacks são bem-vindos.*
