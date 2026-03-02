# Automação WEB com Robot Framework + Playwright (Browser) + GitHub Actions

[![run Web Testing](https://github.com/rafarfelipe/rf_browser_library/actions/workflows/webtesting-workflow.yml/badge.svg)](https://github.com/rafarfelipe/rf_browser_library/actions/workflows/webtesting-workflow.yml)

## Visão geral

Projeto de portfólio com exemplos práticos de automação de testes WEB usando **Robot Framework** com a **Browser Library** (baseada em **Playwright**) e execução automatizada via **GitHub Actions**.

## Destaques (o que este projeto demonstra)

- Automação WEB com **Playwright sem WebDriver** (Browser Library)
- Execução em **múltiplos navegadores** via matrix no CI (`chromium`, `firefox`, `webkit`)
- Parametrização por variáveis (`HEADLESS`, `BROWSER`) para rodar local/CI com o mesmo código
- Publicação de **artefatos e relatórios** de teste no pipeline

## Tecnologias

- Robot Framework
- Robot Framework Browser (Playwright)
- GitHub Actions (CI)

## Browser vs SeleniumLibrary (diferenças principais)

- **Engine**: Browser usa Playwright (driverless); SeleniumLibrary depende de WebDriver
- **Multi-navegador**: Browser facilita rodar em Chromium/Firefox/WebKit com a mesma base de testes
- **Estabilidade**: Browser costuma ter auto-wait mais consistente para UI moderna
- **Seletores**: Browser usa locators do Playwright (CSS, text, role, etc.)

## Estrutura do projeto

- `tests/`: suites Robot Framework (`.robot`)
- `resources/`: resources reutilizáveis (`.resource`)

## Suites e cenários

- `tests/the-internet-herokuapp.robot`: interações com dropdown, iFrame, tabelas e múltiplas abas (pages)
- `tests/serve-rest-front.robot`: fluxo de cadastro/login, validação em listagens, cadastro/consulta de produtos, uso de requisições HTTP e storage no contexto

## Pré-requisitos

- Python (para instalar `requirements.txt`)
- Node.js (necessário para instalar/rodar o Playwright)

## Como executar localmente

1. Instale as dependências Python:

```bash
pip install -U -r requirements.txt
```

2. Inicialize a Browser Library (download de browsers + deps):

```bash
rfbrowser init
```

3. Execute os testes:

```bash
robot -d ./results -v HEADLESS:true -v BROWSER:chromium tests/
```

Variações úteis:

```bash
# outro navegador
robot -d ./results -v HEADLESS:true -v BROWSER:firefox tests/

# modo visível (não headless)
robot -d ./results -v HEADLESS:false -v BROWSER:chromium tests/
```

## CI no GitHub Actions

O workflow `.github/workflows/webtesting-workflow.yml` executa os testes a cada `push` e roda uma **matrix** de browsers (`chromium`, `firefox`, `webkit`). Ao final, o pipeline faz upload dos artefatos (logs/relatórios) e publica um report.

## Resultados no GitHub Actions

- Runs do workflow: https://github.com/rafarfelipe/rf_browser_library/actions/workflows/webtesting-workflow.yml
- Artifacts por navegador (para baixar): `results-chromium`, `results-firefox`, `results-webkit`
- Conteúdo típico do artifact: `log.html`, `report.html`, `output.xml`
- Retenção dos artifacts no CI: 4 dias (configurado no workflow)

## Resultados e evidências

Os arquivos gerados localmente ficam em `results/` (por exemplo `log.html`, `report.html`, `output.xml`). Essa pasta é ignorada pelo Git para manter o repositório focado em código de testes e recursos reutilizáveis.

## Aprendizados aplicados

- Você utilizou a Browser Library para automação WEB com Playwright
- Você comparou Browser vs SeleniumLibrary na prática
- Você executou testes localmente com parametrização (headless e navegador)
- Você implementou uma pipeline CI no GitHub Actions para executar e reportar testes
