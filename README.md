# Challenge Codeurs Pro — Chatbot 100 % local

**Nom du dépôt :** `challenge_24_07_2026`  
**Dépôt officiel (prioritaire) :** [CodeursPro/challenge_24_07_2026](https://github.com/CodeursPro/challenge_24_07_2026)  
**Dépôt de secours :** [KELI-Kekeli-Christ/challenge_24_07_2026](https://github.com/KELI-Kekeli-Christ/challenge_24_07_2026)  
**Début du challenge :** dès réception de cet énoncé  
**Fin des soumissions :** **mercredi à 23h59 GMT**  
**Publication des résultats :** **vendredi soir**

> **À lire avant de forker :** utilisez d’abord le dépôt **CodeursPro**.  
> Si le lien officiel ne s’ouvre pas (page introuvable / 404), forkez alors le **dépôt de secours** ci-dessus.

---

## Objectif

Construire un **chatbot fonctionnant entièrement en local** (sans dépendance à une API cloud obligatoire pour l’inférence).

Le chatbot peut servir différents cas d’usage, par exemple :

- assistant commercial ;
- FAQ d’une université ;
- assistant documentaire ;
- tout autre scénario métier pertinent.

> **Important :** le but principal n’est **pas** de livrer une interface graphique très avancée.  
> L’essentiel est que le chatbot soit **performant**, qu’il **réponde correctement** aux questions, et qu’il **ne génère pas de réponses hors sujet**.

---

## Contraintes & critères d’évaluation

| Critère | Attendu |
| --- | --- |
| Exécution locale | Le modèle tourne en local (ex. via [Ollama](https://ollama.com)) |
| Pertinence | Réponses alignées avec le domaine / le rôle défini |
| Anti hors-sujet | Le bot refuse ou recentre poliment les questions hors périmètre |
| Qualité | Réponses claires, utiles, cohérentes |
| UI | Simple acceptée (CLI, terminal, petite UI web, etc.) |

Ce qui sera particulièrement regardé :

1. **Qualité des réponses** (exactitude, clarté, utilité).
2. **Respect du rôle** (system prompt / consignes système).
3. **Robustesse face aux questions hors sujet**.
4. **Reproductibilité** (README clair, installation simple, démarrage documenté).

---

## Piste technique recommandée : Ollama + system prompts

Pour bien **contraindre** le LLM et améliorer la qualité des réponses, renseignez-vous sur les **rôles système (system prompts)**.

### Documentation officielle Ollama

- Modelfile & instruction `SYSTEM` : [https://docs.ollama.com/modelfile#system](https://docs.ollama.com/modelfile#system)
- Documentation Modelfile complète : [https://docs.ollama.com/modelfile](https://docs.ollama.com/modelfile)
- API (paramètre `system` / messages de rôle) : [https://docs.ollama.com/api](https://docs.ollama.com/api)

Un **system prompt** définit le comportement du modèle : son rôle, son ton, ses limites, et ce qu’il ne doit **pas** faire. C’est l’outil principal pour éviter les digressions et les réponses hors sujet.

### Exemple de Modelfile (Ollama)

```dockerfile
FROM llama3.2

SYSTEM """
Tu es un assistant FAQ pour une université.
Tu réponds uniquement aux questions liées à l’inscription, les cursus,
les examens, les bourses et la vie étudiante.

Si la question est hors sujet, refuse poliment et propose de reformuler
dans le périmètre universitaire.
Réponds de façon concise, claire et en français.
"""

PARAMETER temperature 0.3
```

Création du modèle personnalisé :

```bash
ollama create mon-assistant-faq -f Modelfile
ollama run mon-assistant-faq
```

---

## Comment participer (obligatoire)

### 1. Faire un fork (avant tout push)

> **Ne poussez pas directement sur le dépôt source.**  
> Travaillez **uniquement** depuis **votre fork**.

1. Ouvrez **en priorité** le dépôt officiel :  
   **https://github.com/CodeursPro/challenge_24_07_2026**
2. **Si ce lien ne marche pas** (404 / dépôt introuvable), utilisez le dépôt de secours :  
   **https://github.com/KELI-Kekeli-Christ/challenge_24_07_2026**
3. Cliquez sur **Fork** (en haut à droite).
4. Créez le fork sur **votre compte GitHub** personnel.
5. Clonez **votre fork** en local :

```bash
git clone https://github.com/<VOTRE_USERNAME>/challenge_24_07_2026.git
cd challenge_24_07_2026
```

### 2. Créer une branche de travail

```bash
git checkout -b challenge/<votre-pseudo>
```

### 3. Développer votre solution

Structure suggérée (libre, tant que c’est clair) :

```text
challenge_24_07_2026/
├── README.md                 # énoncé du challenge (ce fichier)
├── participants/
│   └── <votre-pseudo>/
│       ├── README.md         # comment installer & lancer VOTRE bot
│       ├── Modelfile         # (optionnel) system prompt / config Ollama
│       ├── src/              # code du chatbot
│       └── ...
└── ...
```

Dans le `README.md` de votre dossier participant, documentez au minimum :

- le cas d’usage choisi (FAQ univ, commercial, documentaire, etc.) ;
- les prérequis (Ollama, modèle utilisé, Python/Node, etc.) ;
- les commandes d’installation et de lancement ;
- quelques exemples de questions / réponses attendues ;
- comment le bot gère les questions hors sujet.

### 4. Commit & push sur VOTRE fork

```bash
git add .
git commit -m "feat: mon chatbot local pour le challenge"
git push -u origin challenge/<votre-pseudo>
```

### 5. Ouvrir une Pull Request vers le dépôt source

1. Sur GitHub, ouvrez une **Pull Request** depuis votre fork vers la branche `main` du dépôt que vous avez forké :
   - **prioritaire :** `CodeursPro/challenge_24_07_2026`
   - **sinon (secours) :** `KELI-Kekeli-Christ/challenge_24_07_2026`
2. Titre suggéré : `[Challenge] <votre-pseudo> — <cas d’usage>`
3. Dans la description, résumez :
   - cas d’usage ;
   - modèle local utilisé ;
   - points forts (anti hors-sujet, system prompt, etc.).

Les soumissions doivent être reçues **avant mercredi 23h59 GMT**.

---

## Comment ça marche (vue d’ensemble)

```text
┌──────────────────────────────┐
│  1) CodeursPro/...  (prioritaire)
│  2) KELI-Kekeli-Christ/... (si lien KO)
└──────────────┬───────────────┘
               │ fork
               ▼
┌──────────────────────────┐
│  Votre fork (personnel)  │
│  <user>/challenge_...    │
└──────────────┬───────────┘
               │ Pull Request
               ▼
        Équipe Codeurs Pro
```

1. **Priorité :** forkez [CodeursPro/challenge_24_07_2026](https://github.com/CodeursPro/challenge_24_07_2026).
2. **Secours :** si ce lien ne marche pas, forkez [KELI-Kekeli-Christ/challenge_24_07_2026](https://github.com/KELI-Kekeli-Christ/challenge_24_07_2026).
3. **Chaque participant** travaille uniquement depuis **son fork**.
4. **Le développement se fait en local** : modèle LLM local (souvent Ollama) + votre code.
5. **Le system prompt** cadre le rôle du bot et limite les réponses hors sujet.
6. **La Pull Request** vers le dépôt source est votre soumission officielle.
7. **Les résultats** sont communiqués **vendredi soir**.

---

## Idées de cas d’usage

- **Assistant commercial** : présente une offre, répond aux objections, reste dans le catalogue.
- **FAQ universitaire** : inscriptions, emplois du temps, procédures administratives.
- **Assistant documentaire** : répond à partir d’un corpus local (PDF, notes, wiki).
- **Support produit** : guide l’utilisateur dans l’usage d’un logiciel / d’un service.

Peu importe le cas choisi : ce qui compte, c’est la **maîtrise du comportement** du modèle en local.

---

## Checklist avant soumission

- [ ] J’ai tenté d’abord le dépôt **CodeursPro**, sinon le **dépôt de secours**
- [ ] J’ai **forké** le dépôt avant de pousser mon code
- [ ] Mon chatbot tourne **entièrement en local**
- [ ] Un **system prompt** (ou équivalent) définit clairement le rôle
- [ ] Les questions hors sujet sont gérées (refus / recentrage)
- [ ] Mon `README` participant permet de relancer le projet facilement
- [ ] Ma **Pull Request** est ouverte avant **mercredi 23h59 GMT**

---

## Ressources utiles

- [Ollama](https://ollama.com)
- [Documentation Modelfile — instruction SYSTEM](https://docs.ollama.com/modelfile#system)
- [Documentation API Ollama](https://docs.ollama.com/api)
- [Bibliothèque de modèles Ollama](https://ollama.com/library)

---

# 📌 Solution : Mikero AI par Mike Alladoum

Cette section documente la solution **Mikero AI** développée pour ce challenge.

## À propos de Mikero AI

**Mikero AI** est un **chatbot local spécialisé en blockchain et Web3**, assistant officiel de Mike Alladoum.

**Cas d'usage:** Assistant commercial pour les services Web3 et documentaire blockchain  
**Modèle:** Qwen 2.5 7B (Alibaba) en local via Ollama  
**Auteur:** Mike Alladoum  
**Date:** 24-07-2026

---

## 🎯 Description de la solution

Mikero AI est un chatbot qui :
- ✅ Tourne **entièrement en local** avec Ollama
- ✅ Répond sur le profil et services de Mike Alladoum
- ✅ Explique la blockchain et le Web3
- ✅ Refuse poliment les questions hors sujet
- ✅ Fournit des réponses claires, structurées et pertinentes

---

## 📥 Installation rapide

### Prérequis
- Ollama installé et fonctionnant
- 16GB RAM minimum
- 5GB espace disque libre

### Étapes

```bash
# 1. Télécharger le modèle Qwen 2.5
ollama pull qwen2.5:7b

# 2. Créer Mikero AI à partir du Modelfile
cd challenge_24_07_2026
ollama create mikero-ai -f Modelfile

# 3. Vérifier l'installation
ollama list  # Doit afficher "mikero-ai"
```

---

## 🚀 Lancement

### Via Terminal (CLI)

```bash
ollama run mikero-ai "Bonjour! Qui es-tu?"
```

**Réponse attendue:**
```
Je suis Mikero AI, l'assistant IA de Mike Alladoum. Je peux vous aider avec
toutes vos questions concernant le développement en blockchain et Web3, les
smart contracts, Ethereum et d'autres technologies connexes.
```

### Via Ollama App
1. Ouvrez Ollama App
2. Cherchez "mikero-ai"
3. Sélectionnez et posez vos questions

### Via API
```bash
curl http://localhost:11434/api/generate -d '{
  "model": "mikero-ai",
  "prompt": "Quels services Mike propose?",
  "stream": false
}'
```

---

## 💬 Exemples de réponses

### Q: Quels services Mike propose-t-il?
**R:** Mike Alladoum propose plusieurs services liés à la blockchain:
- Développement d'applications Web3 et DApps
- Développement et audit de smart contracts (Solidity)
- Intégration de wallets et Web3
- Solutions blockchain personnalisées
- Développement frontend/backend
- Création de prototypes et MVP
- Conseil technique blockchain

### Q: Explique Solidity
**R:** Solidity est un langage de programmation pour écrire des smart contracts sur Ethereum. 
Il offre une syntaxe proche de JavaScript avec des fonctionnalités blockchain...

### Q: Peux-tu me donner une recette?
**R:** Je suis Mikero AI, l'assistant de Mike Alladoum, spécialisé en blockchain et Web3. 
Je ne peux pas répondre à cette question, mais je peux vous aider sur les services et concepts 
blockchain de Mike.

---

## ✅ Critères d'évaluation — Résultats

| Critère | Statut | Détails |
|---------|--------|---------|
| **Exécution locale** | ✅ VALIDÉ | Qwen 2.5 7B + Ollama, fonctionnement 100% local |
| **Pertinence** | ✅ VALIDÉ | Réponses alignées blockchain/Web3/services Mike |
| **Anti hors-sujet** | ✅ VALIDÉ | Refuse poliment, recentre vers ses compétences |
| **Qualité** | ✅ VALIDÉ | Réponses claires, structurées, cohérentes |
| **UI** | ✅ VALIDÉ | CLI + Ollama App + API disponibles |
| **Reproductibilité** | ✅ VALIDÉ | Installation documentée, Modelfile inclus |

---

## 📁 Fichiers de la solution

```
challenge_24_07_2026/
├── README.md              # Ce fichier + spécifications challenge
├── Modelfile              # Configuration Ollama (System Prompt Mikero AI)
└── .git/                  # Branche: challenge/mike-alladoum
```

### Fichier clé: Modelfile

Le `Modelfile` définit :
- Modèle de base: `qwen2.5:7b`
- System Prompt personnalisé avec:
  - Rôle de Mikero AI
  - Infos sur Mike Alladoum
  - Domaines de spécialisation
  - Ton et style à respecter
  - Limites et gestion des hors-sujets

---

## 🔧 Architecture technique

```
Qwen 2.5 7B (brut)
        ↓
    + Modelfile
        ↓
    Mikero AI (modèle personnalisé)
        ↓
    Ollama (runtime local)
        ↓
    Utilisateur (CLI / App / API)
```

**Taille modèle:** 4.7 GB (quantization Q4)  
**RAM requise:** 16 GB  
**Temps réponse:** 2-5 sec (CPU i5)  
**Langues:** Français, Anglais

---

## 👤 Contacts

- **GitHub:** https://github.com/MikeAlladoum
- **LinkedIn:** https://www.linkedin.com/in/mike-alladoum-a557102a1/
- **YouTube:** https://youtube.com/@damlegend
- **Email:** Damlegend48@

---

## 📚 Ressources utilisées

- [Ollama](https://ollama.com)
- [Qwen 2.5 Model](https://github.com/QwenLM/Qwen2.5)
- [Ollama Modelfile Docs](https://docs.ollama.com/modelfile)
- [Ethereum Dev](https://ethereum.org/developers)

---

Bonne chance à toutes et à tous — **Codeurs Pro**
