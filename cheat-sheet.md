# Github Actions

Ein Service von Github, um automatisierte Prozesse, sogennante Workflows, zu erstellen. Das Feature kann genutzt werden, um CI/CD Pipelines
(Builds, Tests, Deployments) zu entwickeln oder für die Verwaltung des eigenen Repositories (automatische Code Reviews, Issue Management). Als Basis dient
immer das hochgeladene Repository, in dem die Action bzw. Workflow liegt.

## Hauptelemente

### Workflows
Workflows liegen immer unter `./github/workflows` und im `yml` Format vor. Sie werden durch Events getriggered. Ein Event/Trigger kann zum Beispiel ein `push` eines Commits sein und es können mehrere Events angegeben werden, die ein Workflow starten `[push, workflow_dispatch]`.

Mehr Informationen zu **Events** gibt es hier:
https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows

### Jobs
Ein Workflow kann aus einer Vielzahl an Jobs bestehen, die, wenn nicht anders konfiguriert, parallel laufen. Jeder Job wird auf einem definierten Server/Host
ausgeführt. Es gibt von Github gehostete Server für die gängigen Betriebsysteme (z.B. `ubuntu-latest`). Aber man kann auch einen eigenen Server nutzen, 
falls man möchte.

Mehr Informationen zu **Runner** gibt es hier: 
https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners

### Steps
Jeder Job besteht aus einer Vielzahl an Steps. Ein Step führt entweder ein Kommando (Shell-Befehl) oder eine andere Github Action aus. Steps werden sequentiell
ausgeführt. 

#### Beispiel eines ersten Workflows mit den Hauptelementen
```yml
name: Erster Workflow
on: workflow_dispatch
jobs:
  ErsterJob:
    runs-on: ubuntu-latest
    steps:
      - name: Erster Schritt
        run: echo "Hello World"
```

#### Mehrere Kommandos
```yml
  run: |
    echo "Erstes Kommando"
    echo "Zweites Kommando"
```

### GitHub Actions Marketplace
Um nicht stets das Rad neu zu erfinden, gibt es einen GitHub Actions Marketplace, der diverse Actions zur Verfügung stellt. Angeführt mit dem Schlagwort `uses` sind Actions nützlich um repetitive komplexe Aufgaben auszulagern. Damit wird die eigene Action überschaubar und man spart an Zeit. Jede Action hat eine Seite auf dem Marketplace mit Informationen. Beispielsweise zur Nutzung und ob es sich um einen verifizierte Action handelt. Eine gängige Action ist die `actions/checkout` Action. Mit dieser kann man das eigene Repository auf den laufenden Runner klonen, denn dieser hat zu Beginn eines Jobs keine Informationen über unseren Repoinhalt.

Mehr Informationen zu Checkout Action: https://github.com/marketplace/actions/checkout

#### Nutzung einer GitHub Action
```yml
name: Workflow mit Action
on: workflow_dispatch
jobs:
  Klonen:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repo
        uses: actions/checkout@v3
```
