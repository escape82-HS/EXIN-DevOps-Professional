# 🚀 Laboratorio: CI/CD Pipeline con GitHub Actions e Docker

![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![EXIN DevOps](https://img.shields.io/badge/EXIN-DevOps%20Professional-purple?style=for-the-badge)

Questo repository contiene il codice sorgente e la documentazione per il laboratorio pratico del corso **EXIN DevOps Professional**.

L'obiettivo è dimostrare l'implementazione di una pipeline di **Continuous Delivery** che automatizza la creazione (Build) e la pubblicazione (Push) di un'immagine Docker su Docker Hub ogni volta che viene modificato il codice sorgente.

---

## 📋 Prerequisiti

Per eseguire questo laboratorio, è necessario disporre di:
1.  Un account **[GitHub](https://github.com/)**.
2.  Un account **[Docker Hub](https://hub.docker.com/)**.
3.  Conoscenza base di Git e Docker.

---

## 🛠️ Struttura del Progetto

Il repository è composto dai seguenti file chiave:

*   `Dockerfile`: Definisce l'ambiente del container (basato su Nginx) e copia l'applicazione al suo interno.
*   `index.html`: Una semplice pagina web statica che funge da nostra "applicazione".
*   `.github/workflows/docker-publish.yml`: Il file di configurazione della pipeline CI/CD.

---

## ⚙️ Configurazione (Step-by-Step)

### 1. Fork o Clone
Effettua il fork di questo repository o clonalo localmente:
```bash
git clone https://github.com/TUO_USERNAME/devops-docker-lab.git
cd devops-docker-lab
```

### 2. Configurazione dei Secrets (Critico)
Per permettere a GitHub Actions di accedere al tuo Docker Hub in modo sicuro, **NON** scrivere la password nel codice. Usa i **GitHub Secrets**:

1.  Vai su `Settings` > `Secrets and variables` > `Actions` nel tuo repository GitHub.
2.  Clicca su `New repository secret`.
3.  Aggiungi le seguenti due variabili:

| Nome Secret | Valore |
| :--- | :--- |
| `DOCKER_USERNAME` | Il tuo ID utente di Docker Hub. |
| `DOCKER_PASSWORD` | La tua password di Docker Hub (o meglio, un [Access Token](https://docs.docker.com/security/for-developers/access-tokens/)). |

### 3. La Pipeline (Workflow)
Il file `.github/workflows/docker-publish.yml` esegue i seguenti passaggi automatici:
1.  **Checkout**: Scarica il codice.
2.  **Login**: Si autentica su Docker Hub usando i Secrets.
3.  **Build & Push**: Crea l'immagine Docker e la carica sul registro.

---

## 🚀 Esecuzione e Verifica

Per attivare la pipeline, è sufficiente effettuare una modifica e un push sul branch `main`.

1.  Modifica il file `index.html` (es. cambia il testo del titolo).
2.  Esegui il commit e il push:
    ```bash
    git add index.html
    git commit -m "Aggiornamento homepage"
    git push origin main
    ```
3.  Vai nella tab **Actions** su GitHub per vedere il processo in tempo reale.
4.  Una volta terminato (segno di spunta verde ✅), controlla il tuo repository su **Docker Hub**: troverai l'immagine aggiornata con il tag `latest`.

---

## 🧠 Concetti EXIN DevOps Trattati

Questo laboratorio copre i seguenti argomenti d'esame:

*   **Continuous Integration (CI):** Il trigger automatico (`on: push`) garantisce che ogni modifica venga integrata immediatamente.
*   **Continuous Delivery (CD):** Il software è sempre in uno stato rilasciabile (l'immagine Docker è pronta su Hub).
*   **Infrastructure as Code (IaC):** L'ambiente è definito via codice (`Dockerfile`) e non configurato manualmente.
*   **Security & Configuration Management:** Gestione delle credenziali tramite variabili d'ambiente segrete (Secrets), separando il codice dalla configurazione sensibile.

---

## 📄 Licenza

Questo progetto è a scopo didattico per la preparazione all'esame EXIN DevOps Professional.