# Voici une stack de base clé en main, incluant :

**Prometheus (collecte de métriques)**

**Node Exporter (pour surveiller ton VPS Linux)**

Grafana (dashboard visuel)

**Configuration via Docker Compose**



✅ 1. Accéder aux interfaces
Prometheus : http://<IP_VPS>:9090

Grafana : http://<IP_VPS>:3000

Node Exporter metrics : http://<IP_VPS>:9100/metrics

🧠 2. Ce que fait chaque composant

Composant	Rôle
Node Exporter	Collecte les métriques système (CPU, RAM, disque, réseau, etc.)
Prometheus	Scrape et stocke les métriques, fournit un moteur de requête
Grafana	Visualise les données en dashboards
⚙️ 3. Configuration de Prometheus
Tu l’as déjà bien configuré avec prometheus.yml :

yaml
Copier
Modifier
scrape_configs:
- job_name: 'prometheus'
  static_configs:
    - targets: ['prometheus:9090']

- job_name: 'node_exporter'
  static_configs:
    - targets: ['node-exporter:9100']
      Tu peux ajouter d’autres services plus tard (comme nginx, postgres, docker, etc.)

📊 4. Configuration de Grafana
➤ Connexion initiale
URL : http://<IP_VPS>:3000

Identifiants par défaut :

user : admin

pass : admin (tu devras le changer au premier login)

➤ Ajouter Prometheus comme Data Source
Va dans ⚙️ Configuration > Data Sources

Clique sur Add data source

Choisis Prometheus

Dans URL, mets : http://prometheus:9090 (le nom du service Docker)

Clique sur Save & test

📁 5. Importer un dashboard Node Exporter
Option 1 : depuis Grafana
Va dans + > Import

Colle cet ID : 1860 (Dashboard officiel pour Node Exporter Full)

Clique sur Load

Choisis la data source Prometheus

Clique sur Import

Option 2 : tu veux que je te le prépare en provisioning automatique ?
Je peux te générer un fichier dashboard.json + provisioning YAML.

🔎 6. Explorer les métriques dans Prometheus
Va sur http://<IP_VPS>:9090

Tape par exemple :

node_cpu_seconds_total

node_memory_MemAvailable_bytes

rate(node_network_receive_bytes_total[1m])

Tu peux voir les séries de temps et tester les expressions PromQL

📦 7. Bonus : sauvegarde et persistance
➤ Volume Docker
Tu l’as déjà fait avec :

yaml
Copier
Modifier
volumes:
- prometheus_data:/prometheus
- grafana_data:/var/lib/grafana
  Cela permet de garder les données entre redémarrages.



---------------------------------------------------------
yacouboubassarou@gmail.com
+229 97 60 26 57 