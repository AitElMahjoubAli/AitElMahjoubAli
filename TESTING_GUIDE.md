# 🧪 Guide Complet de Tests - CloudSecure Monitor

## 📋 Table des Matières

1. [Tests Unitaires](#tests-unitaires)
2. [Tests d'Intégration](#tests-dintégration)
3. [Tests Frontend](#tests-frontend)
4. [Tests API](#tests-api)
5. [Tests de Performance](#tests-de-performance)
6. [Tests de Sécurité](#tests-de-sécurité)
7. [Tests de Compatibilité](#tests-de-compatibilité)

---

## 1. Tests Unitaires

### Configuration Jest

```bash
# Jest est déjà inclus avec Create React App
npm test
```

### Tests des Composants React

**Créer `src/components/__tests__/MetricCard.test.js` :**

```javascript
import { render, screen } from '@testing-library/react';
import MetricCard from '../MetricCard';

describe('MetricCard Component', () => {
  test('affiche le titre correctement', () => {
    render(<MetricCard title="CPU Usage" value="75%" />);
    expect(screen.getByText('CPU Usage')).toBeInTheDocument();
  });

  test('affiche la valeur correctement', () => {
    render(<MetricCard title="CPU Usage" value="75%" />);
    expect(screen.getByText('75%')).toBeInTheDocument();
  });

  test('applique la classe de couleur correcte', () => {
    const { container } = render(
      <MetricCard title="CPU" value="75%" color="blue" />
    );
    expect(container.firstChild).toHaveClass('bg-blue-500');
  });
});
```

### Tests des Fonctions Utilitaires

**Créer `src/utils/__tests__/calculations.test.js` :**

```javascript
import { calculateSecurityScore, formatBytes, getAlertSeverity } from '../calculations';

describe('Calculations Utils', () => {
  test('calculateSecurityScore retourne un score valide', () => {
    const score = calculateSecurityScore(10, 2, 5);
    expect(score).toBeGreaterThanOrEqual(0);
    expect(score).toBeLessThanOrEqual(100);
  });

  test('formatBytes formate correctement les octets', () => {
    expect(formatBytes(1024)).toBe('1 KB');
    expect(formatBytes(1048576)).toBe('1 MB');
    expect(formatBytes(1073741824)).toBe('1 GB');
  });

  test('getAlertSeverity retourne la bonne sévérité', () => {
    expect(getAlertSeverity(90)).toBe('critical');
    expect(getAlertSeverity(70)).toBe('high');
    expect(getAlertSeverity(50)).toBe('medium');
    expect(getAlertSeverity(20)).toBe('low');
  });
});
```

### Commandes de Test

```bash
# Lancer tous les tests
npm test

# Lancer les tests en mode watch
npm test -- --watch

# Lancer les tests avec couverture
npm test -- --coverage

# Lancer un fichier de test spécifique
npm test MetricCard.test.js
```

### Objectifs de Couverture

- ✅ **Statements:** > 80%
- ✅ **Branches:** > 75%
- ✅ **Functions:** > 80%
- ✅ **Lines:** > 80%

---

## 2. Tests d'Intégration

### Configuration Supertest (Backend)

```bash
cd backend
npm install --save-dev supertest jest
```

**Créer `backend/__tests__/api.test.js` :**

```javascript
const request = require('supertest');
const app = require('../server');

describe('API Endpoints', () => {
  describe('GET /api/metrics', () => {
    test('retourne les métriques avec status 200', async () => {
      const response = await request(app).get('/api/metrics');
      expect(response.status).toBe(200);
      expect(response.body).toHaveProperty('cpu');
      expect(response.body).toHaveProperty('memory');
      expect(response.body).toHaveProperty('network');
    });

    test('les métriques ont le bon format', async () => {
      const response = await request(app).get('/api/metrics');
      expect(response.body.cpu).toBeGreaterThanOrEqual(0);
      expect(response.body.cpu).toBeLessThanOrEqual(100);
    });
  });

  describe('GET /api/security', () => {
    test('retourne l\'analyse de sécurité', async () => {
      const response = await request(app).get('/api/security');
      expect(response.status).toBe(200);
      expect(response.body).toHaveProperty('score');
      expect(response.body).toHaveProperty('vulnerabilities');
    });
  });

  describe('POST /api/alerts', () => {
    test('crée une nouvelle alerte', async () => {
      const newAlert = {
        type: 'security',
        severity: 'high',
        message: 'Test alert'
      };
      
      const response = await request(app)
        .post('/api/alerts')
        .send(newAlert);
      
      expect(response.status).toBe(201);
      expect(response.body).toHaveProperty('id');
    });

    test('rejette une alerte invalide', async () => {
      const invalidAlert = {
        type: 'invalid'
      };
      
      const response = await request(app)
        .post('/api/alerts')
        .send(invalidAlert);
      
      expect(response.status).toBe(400);
    });
  });
});
```

---

## 3. Tests Frontend (Browser)

### Checklist Manuelle

#### 3.1 Page d'Accueil (Dashboard)

- [ ] **Chargement Initial**
  - [ ] Le dashboard s'affiche en moins de 3 secondes
  - [ ] Aucune erreur dans la console
  - [ ] Tous les composants sont visibles

- [ ] **Cartes de Métriques**
  - [ ] 4 cartes principales affichées (CPU, RAM, Réseau, Stockage)
  - [ ] Les valeurs sont numériques et réalistes
  - [ ] Les icônes s'affichent correctement
  - [ ] Les couleurs correspondent aux seuils

- [ ] **Graphiques**
  - [ ] Graphique de performance s'affiche
  - [ ] Graphique de sécurité s'affiche
  - [ ] Les données sont cohérentes
  - [ ] Les tooltips fonctionnent au survol
  - [ ] Les légendes sont lisibles

#### 3.2 Navigation

- [ ] **Menu Principal**
  - [ ] Tous les liens sont cliquables
  - [ ] La navigation change la page
  - [ ] L'élément actif est surligné
  - [ ] Le logo ramène à l'accueil

- [ ] **Breadcrumbs**
  - [ ] Le fil d'Ariane s'affiche
  - [ ] Les liens fonctionnent
  - [ ] La page actuelle est indiquée

#### 3.3 Page Sécurité

- [ ] **Score de Sécurité**
  - [ ] Le score s'affiche (0-100)
  - [ ] La jauge visuelle fonctionne
  - [ ] La couleur change selon le score

- [ ] **Liste des Vulnérabilités**
  - [ ] Les vulnérabilités s'affichent
  - [ ] Filtrage par sévérité fonctionne
  - [ ] Détails au clic fonctionnent

#### 3.4 Page Alertes

- [ ] **Liste des Alertes**
  - [ ] Les alertes s'affichent
  - [ ] Badge de compteur correct
  - [ ] Tri par date fonctionne
  - [ ] Filtrage par type fonctionne

- [ ] **Actions sur Alertes**
  - [ ] Marquer comme lu fonctionne
  - [ ] Supprimer une alerte fonctionne
  - [ ] Détails de l'alerte s'affichent

#### 3.5 Responsive Design

- [ ] **Mobile (< 768px)**
  - [ ] Menu hamburger fonctionne
  - [ ] Cartes empilées verticalement
  - [ ] Graphiques adaptés
  - [ ] Texte lisible

- [ ] **Tablette (768px - 1024px)**
  - [ ] Layout à 2 colonnes
  - [ ] Navigation adaptée
  - [ ] Graphiques optimisés

- [ ] **Desktop (> 1024px)**
  - [ ] Layout complet
  - [ ] Sidebar visible
  - [ ] Tous les éléments visibles

#### 3.6 Interactions

- [ ] **Boutons**
  - [ ] Tous les boutons sont cliquables
  - [ ] Effet hover fonctionne
  - [ ] Feedback visuel au clic

- [ ] **Formulaires**
  - [ ] Validation des champs
  - [ ] Messages d'erreur clairs
  - [ ] Soumission fonctionne

- [ ] **Modales**
  - [ ] S'ouvrent correctement
  - [ ] Se ferment au clic extérieur
  - [ ] Bouton fermer fonctionne

---

## 4. Tests API (avec curl)

### 4.1 Test des Endpoints

```bash
# Démarrer le serveur backend
cd backend
node server.js &

# Test 1: Récupérer les métriques
curl -X GET http://localhost:5000/api/metrics

# Résultat attendu:
# {
#   "cpu": 45.2,
#   "memory": 67.8,
#   "network": 234.5,
#   "storage": 78.3,
#   "timestamp": "2025-11-14T10:30:00Z"
# }

# Test 2: Récupérer l'analyse de sécurité
curl -X GET http://localhost:5000/api/security

# Résultat attendu:
# {
#   "score": 85,
#   "vulnerabilities": [...],
#   "recommendations": [...]
# }

# Test 3: Récupérer les alertes
curl -X GET http://localhost:5000/api/alerts

# Test 4: Créer une nouvelle alerte
curl -X POST http://localhost:5000/api/alerts \
  -H "Content-Type: application/json" \
  -d '{
    "type": "security",
    "severity": "high",
    "message": "Tentative d'\''accès non autorisé détectée",
    "source": "Firewall"
  }'

# Test 5: Récupérer une alerte spécifique
curl -X GET http://localhost:5000/api/alerts/1

# Test 6: Mettre à jour une alerte
curl -X PUT http://localhost:5000/api/alerts/1 \
  -H "Content-Type: application/json" \
  -d '{"status": "resolved"}'

# Test 7: Supprimer une alerte
curl -X DELETE http://localhost:5000/api/alerts/1

# Test 8: Générer un rapport
curl -X POST http://localhost:5000/api/reports \
  -H "Content-Type: application/json" \
  -d '{
    "type": "security",
    "period": "last_7_days"
  }'
```

### 4.2 Tests de Validation

```bash
# Test avec données invalides (doit retourner 400)
curl -X POST http://localhost:5000/api/alerts \
  -H "Content-Type: application/json" \
  -d '{"invalid": "data"}'

# Test avec méthode non supportée (doit retourner 405)
curl -X PATCH http://localhost:5000/api/metrics

# Test endpoint inexistant (doit retourner 404)
curl -X GET http://localhost:5000/api/nonexistent
```

### 4.3 Tests de Performance API

```bash
# Test de charge avec Apache Bench
ab -n 1000 -c 10 http://localhost:5000/api/metrics

# Métriques attendues:
# - Requests per second: > 100
# - Time per request: < 100ms
# - Failed requests: 0
```

---

## 5. Tests de Performance

### 5.1 Lighthouse Audit

```bash
# Installer Lighthouse
npm install -g lighthouse

# Lancer l'audit
lighthouse http://localhost:3000 --view

# Scores attendus:
# - Performance: > 90
# - Accessibility: > 90
# - Best Practices: > 90
# - SEO: > 90
```

### 5.2 Bundle Analysis

```bash
# Analyser la taille du bundle
npm run build
npm install -g source-map-explorer
source-map-explorer 'build/static/js/*.js'

# Objectifs:
# - Bundle total: < 500 KB
# - Main chunk: < 250 KB
# - Vendor chunk: < 200 KB
```

### 5.3 Métriques Web Vitals

**Objectifs à atteindre :**

- **LCP (Largest Contentful Paint):** < 2.5s
- **FID (First Input Delay):** < 100ms
- **CLS (Cumulative Layout Shift):** < 0.1
- **FCP (First Contentful Paint):** < 1.8s
- **TTI (Time to Interactive):** < 3.8s

---

## 6. Tests de Sécurité

### 6.1 Checklist de Sécurité

- [ ] **Authentification**
  - [ ] Pas de credentials en dur dans le code
  - [ ] Tokens stockés de manière sécurisée
  - [ ] Session timeout configuré

- [ ] **Validation des Entrées**
  - [ ] Tous les inputs sont validés
  - [ ] Protection contre XSS
  - [ ] Protection contre SQL Injection

- [ ] **Headers de Sécurité**
  - [ ] Content-Security-Policy configuré
  - [ ] X-Frame-Options: DENY
  - [ ] X-Content-Type-Options: nosniff
  - [ ] Strict-Transport-Security activé

- [ ] **CORS**
  - [ ] Origines autorisées définies
  - [ ] Méthodes HTTP limitées
  - [ ] Credentials gérés correctement

- [ ] **Secrets**
  - [ ] Pas de clés API dans le code
  - [ ] Variables d'environnement utilisées
  - [ ] .env dans .gitignore

### 6.2 Tests de Pénétration

```bash
# Scanner les vulnérabilités avec OWASP ZAP
# (Installer OWASP ZAP d'abord)
zap-cli quick-scan http://localhost:3000

# Tester les injections SQL
sqlmap -u "http://localhost:5000/api/alerts?id=1"

# Tester XSS
# Essayer d'injecter: <script>alert('XSS')</script>
```

---

## 7. Tests de Compatibilité

### 7.1 Navigateurs

- [ ] **Chrome** (dernière version)
- [ ] **Firefox** (dernière version)
- [ ] **Safari** (dernière version)
- [ ] **Edge** (dernière version)
- [ ] **Chrome Mobile**
- [ ] **Safari Mobile**

### 7.2 Systèmes d'Exploitation

- [ ] **Windows 10/11**
- [ ] **macOS**
- [ ] **Linux (Ubuntu/Fedora)**
- [ ] **Android**
- [ ] **iOS**

### 7.3 Résolutions d'Écran

- [ ] **Mobile:** 375x667 (iPhone SE)
- [ ] **Mobile:** 414x896 (iPhone 11)
- [ ] **Tablette:** 768x1024 (iPad)
- [ ] **Desktop:** 1366x768
- [ ] **Desktop:** 1920x1080
- [ ] **4K:** 3840x2160

---

## 📊 Rapport de Tests

### Template de Rapport

```markdown
# Rapport de Tests - CloudSecure Monitor
Date: [DATE]
Version: [VERSION]
Testeur: [NOM]

## Résumé
- Tests réussis: X/Y
- Taux de réussite: Z%
- Bugs critiques: N
- Bugs mineurs: M

## Détails par Catégorie

### Tests Unitaires
- Composants: ✅ 15/15
- Fonctions: ✅ 10/10
- Couverture: 85%

### Tests d'Intégration
- API Endpoints: ✅ 8/8
- Flux utilisateur: ✅ 5/5

### Tests Frontend
- Navigation: ✅
- Responsive: ✅
- Interactions: ✅

### Tests de Performance
- Lighthouse Score: 92/100
- Bundle Size: 450 KB ✅
- Load Time: 2.1s ✅

### Tests de Sécurité
- Vulnérabilités: 0 ✅
- Headers: ✅
- CORS: ✅

## Bugs Identifiés
1. [BUG-001] Description...
2. [BUG-002] Description...

## Recommandations
1. Améliorer...
2. Optimiser...

## Conclusion
[Résumé global]
```

---

## 🎯 Critères de Validation Finale

### Application Prête pour Production

- ✅ Tous les tests unitaires passent
- ✅ Tous les tests d'intégration passent
- ✅ Aucun bug critique
- ✅ Performance > 90 (Lighthouse)
- ✅ Responsive sur tous les devices
- ✅ Compatible tous navigateurs
- ✅ Aucune vulnérabilité de sécurité
- ✅ Documentation complète
- ✅ Code review effectué
- ✅ Build de production réussi

---

## 🔧 Outils Recommandés

- **Jest** - Tests unitaires
- **React Testing Library** - Tests composants
- **Supertest** - Tests API
- **Lighthouse** - Performance
- **OWASP ZAP** - Sécurité
- **BrowserStack** - Compatibilité
- **Postman** - Tests API manuels

---

**Bon testing ! 🧪**

*Guide créé par Ali Ait El Mahjoub*
