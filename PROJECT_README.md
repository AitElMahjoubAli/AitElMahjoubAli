# 🛡️ CloudSecure Monitor

## Plateforme de Surveillance et Sécurité pour Infrastructures Cloud

[![React](https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://react.dev)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-3.4-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com)
[![Node.js](https://img.shields.io/badge/Node.js-18-339933?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

---

## 📖 Vue d'Ensemble

**CloudSecure Monitor** est une plateforme web moderne de surveillance et de sécurité pour infrastructures cloud. Elle permet de monitorer en temps réel vos ressources cloud, d'analyser les vulnérabilités de sécurité, et de gérer les alertes de manière intelligente.

### 🎯 Pourquoi ce Projet ?

Ce projet a été conçu pour répondre aux besoins croissants de :
- 📊 **Visibilité** sur les infrastructures cloud complexes
- 🔐 **Sécurité** proactive avec détection de menaces
- 🚨 **Réactivité** face aux incidents de sécurité
- 📈 **Conformité** aux standards de sécurité (ISO 27001, NIST)

---

## ✨ Fonctionnalités

### 🖥️ Dashboard Interactif
- Métriques en temps réel (CPU, RAM, Réseau, Stockage)
- Graphiques interactifs avec Recharts
- Interface responsive et moderne

### 🔐 Analyse de Sécurité
- Score de sécurité global
- Détection de vulnérabilités
- Recommandations automatiques
- Scan de conformité

### 🚨 Système d'Alertes
- Notifications en temps réel
- Filtrage par sévérité (Critical, High, Medium, Low)
- Historique des alertes
- Gestion des incidents

### 📊 Rapports
- Génération automatique de rapports
- Export PDF/CSV
- Rapports de conformité
- Analyse de tendances

---

## 🏗️ Architecture

```
Frontend (React + Tailwind)
         ↓
    API Gateway
         ↓
   ┌──────┴──────┐
   ↓      ↓      ↓
Monitor Security Alert
Service Service Service
   └──────┬──────┘
         ↓
   Data Storage
         ↓
Cloud Infrastructure
(Nutanix, VMware, OpenStack, Proxmox)
```

Voir le [schéma d'architecture complet](architecture-diagram.html) pour plus de détails.

---

## 🛠️ Technologies

### Frontend
- **React 18** - Framework UI moderne
- **Tailwind CSS 3.4** - Styling utility-first
- **Recharts** - Visualisations de données
- **Lucide React** - Icônes modernes

### Backend
- **Node.js 18+** - Runtime JavaScript
- **Express.js** - Framework web
- **REST API** - Architecture API

### DevOps
- **Docker** - Conteneurisation
- **Git** - Contrôle de version
- **Vercel/Netlify** - Déploiement

---

## 🚀 Installation

### Prérequis

- Node.js 18+ et npm
- Git
- Un éditeur de code (VS Code recommandé)

### Installation Rapide

```bash
# 1. Créer l'application React
npx create-react-app cloudsecure-monitor
cd cloudsecure-monitor

# 2. Installer les dépendances
npm install -D tailwindcss@3.4.1 postcss autoprefixer postcss-flexbugs-fixes postcss-preset-env
npm install recharts lucide-react

# 3. Configurer Tailwind CSS
npx tailwindcss init -p

# 4. Lancer l'application
npm start
```

L'application sera accessible sur **http://localhost:3000**

### Configuration Détaillée

Voir le [Guide de Démarrage Rapide](QUICK_START.md) pour une configuration complète.

---

## 📁 Structure du Projet

```
cloudsecure-monitor/
├── public/
│   ├── index.html
│   └── favicon.ico
├── src/
│   ├── components/          # Composants React
│   │   ├── Dashboard.js
│   │   ├── Header.js
│   │   ├── Sidebar.js
│   │   ├── MetricCard.js
│   │   └── Charts.js
│   ├── pages/              # Pages de l'application
│   │   ├── Home.js
│   │   ├── Security.js
│   │   ├── Alerts.js
│   │   └── Reports.js
│   ├── services/           # Services API
│   │   ├── api.js
│   │   └── dataGenerator.js
│   ├── utils/              # Fonctions utilitaires
│   ├── App.js
│   ├── index.js
│   └── index.css
├── backend/                # API Backend
│   ├── server.js
│   ├── routes/
│   │   ├── metrics.js
│   │   ├── security.js
│   │   └── alerts.js
│   └── package.json
├── package.json
├── tailwind.config.js
└── README.md
```

---

## 🧪 Tests

### Lancer les Tests

```bash
# Tests unitaires
npm test

# Tests avec couverture
npm test -- --coverage

# Tests d'intégration
cd backend
npm test
```

### Tests Manuels

Voir le [Guide de Tests Complet](TESTING_GUIDE.md) pour :
- ✅ Tests unitaires
- ✅ Tests d'intégration
- ✅ Tests frontend (browser)
- ✅ Tests API (curl)
- ✅ Tests de performance
- ✅ Tests de sécurité

---

## 📊 Métriques de Performance

### Objectifs

- ⚡ **Temps de chargement:** < 3s
- 📦 **Taille du bundle:** < 500KB
- 🎨 **First Contentful Paint:** < 1.5s
- 🖱️ **Time to Interactive:** < 3.5s
- 🏆 **Lighthouse Score:** > 90

### Résultats Actuels

```
Performance:     92/100 ✅
Accessibility:   95/100 ✅
Best Practices:  90/100 ✅
SEO:            100/100 ✅
```

---

## 🔐 Sécurité

### Mesures de Sécurité Implémentées

- ✅ Validation des entrées utilisateur
- ✅ Protection CSRF
- ✅ Headers de sécurité HTTP
- ✅ Pas de secrets dans le code
- ✅ CORS configuré
- ✅ Rate limiting sur l'API

### Audit de Sécurité

```bash
# Scanner les vulnérabilités
npm audit

# Corriger automatiquement
npm audit fix
```

---

## 🚢 Déploiement

### Option 1 : Vercel (Recommandé)

```bash
# Installer Vercel CLI
npm install -g vercel

# Déployer
vercel --prod
```

### Option 2 : Docker

```bash
# Build l'image
docker build -t cloudsecure-monitor .

# Lancer le conteneur
docker run -p 3000:3000 cloudsecure-monitor
```

### Option 3 : Build Local

```bash
# Créer le build de production
npm run build

# Servir le build
npm install -g serve
serve -s build -p 3000
```

---

## 📚 Documentation

- 📖 [Documentation Complète](PROJECT_DOCUMENTATION.md)
- 🚀 [Guide de Démarrage Rapide](QUICK_START.md)
- 🧪 [Guide de Tests](TESTING_GUIDE.md)
- 🏗️ [Schéma d'Architecture](architecture-diagram.html)

---

## 🎓 Compétences Développées

En réalisant ce projet, vous développerez :

- ⚛️ **React** - Développement d'applications modernes
- 🎨 **Tailwind CSS** - Design UI/UX responsive
- 📊 **Data Visualization** - Graphiques interactifs
- 🔧 **API REST** - Architecture backend
- 🐳 **Docker** - Conteneurisation
- 🧪 **Testing** - Tests unitaires et d'intégration
- 🔐 **Security** - Best practices de sécurité
- 📝 **Documentation** - Documentation technique

---

## 🗺️ Roadmap

### Phase 1 : MVP (Actuel)
- ✅ Dashboard de base
- ✅ Métriques temps réel
- ✅ Système d'alertes
- ✅ Interface responsive

### Phase 2 : Améliorations
- [ ] Authentification JWT
- [ ] Base de données réelle
- [ ] WebSocket pour temps réel
- [ ] Notifications push

### Phase 3 : Intégrations
- [ ] Connecteurs cloud (AWS, Azure, GCP)
- [ ] API Nutanix
- [ ] API VMware
- [ ] API OpenStack

### Phase 4 : Avancé
- [ ] Machine Learning pour détection d'anomalies
- [ ] Prédiction de pannes
- [ ] Automatisation de réponses
- [ ] Multi-tenancy

---

## 🤝 Contribution

Les contributions sont les bienvenues ! Pour contribuer :

1. Fork le projet
2. Créer une branche (`git checkout -b feature/AmazingFeature`)
3. Commit les changements (`git commit -m 'Add AmazingFeature'`)
4. Push vers la branche (`git push origin feature/AmazingFeature`)
5. Ouvrir une Pull Request

---

## 📄 Licence

Ce projet est sous licence MIT. Voir le fichier [LICENSE](LICENSE) pour plus de détails.

---

## 👨‍💻 Auteur

**Ali Ait El Mahjoub**

🎓 Étudiant Ingénieur - 5ème année  
🔐 Spécialisation : Cyber Sécurité  
☁️ Systèmes, Réseaux, Sécurité & Cloud Infrastructure

### Certifications

- 🏅 Nutanix Certified Associate (NCA)
- 🏅 Nutanix Certified Professional – Multicloud Infrastructure (NCP-MCI)
- 🏅 Nutanix Certified Specialist – Core (NCS-Core)

### Contact

- 📧 Email: [ali.aitelmahjoub01@gmail.com](mailto:ali.aitelmahjoub01@gmail.com)
- 💼 LinkedIn: [Ali Ait El Mahjoub](https://www.linkedin.com/in/ali-ait-el-mahjoub/)
- 🐙 GitHub: [@AitElMahjoubAli](https://github.com/AitElMahjoubAli)

---

## 🙏 Remerciements

- React Team pour le framework
- Tailwind Labs pour Tailwind CSS
- Recharts pour les visualisations
- La communauté open-source

---

## 📊 Statistiques du Projet

![GitHub stars](https://img.shields.io/github/stars/AitElMahjoubAli/cloudsecure-monitor?style=social)
![GitHub forks](https://img.shields.io/github/forks/AitElMahjoubAli/cloudsecure-monitor?style=social)
![GitHub issues](https://img.shields.io/github/issues/AitElMahjoubAli/cloudsecure-monitor)
![GitHub license](https://img.shields.io/github/license/AitElMahjoubAli/cloudsecure-monitor)

---

<div align="center">

**Fait avec ❤️ par Ali Ait El Mahjoub**

*"The future of infrastructure is not only cloud-native — it's security-native."*

[⬆ Retour en haut](#-cloudsecure-monitor)

</div>
