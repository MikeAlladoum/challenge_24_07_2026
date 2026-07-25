# Challenge Codeurs Pro — Chatbot 100 % local

**Nom du dépôt :** `challenge_24_07_2026`  
**Compte :** [CodeursPro](https://github.com/CodeursPro)  
**Début du challenge :** dès réception de cet énoncé  
**Fin des soumissions :** **mercredi à 23h59 GMT**  
**Publication des résultats :** **vendredi soir**

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

> **Ne poussez pas directement sur le dépôt officiel CodeursPro.**  
> Travaillez **uniquement** depuis **votre fork**.

1. Ouvrez le dépôt officiel :  
   **https://github.com/CodeursPro/challenge_24_07_2026**
2. Cliquez sur **Fork** (en haut à droite).
3. Créez le fork sur **votre compte GitHub** personnel.
4. Clonez **votre fork** en local :

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

### 5. Ouvrir une Pull Request vers le dépôt officiel

1. Sur GitHub, ouvrez une **Pull Request** depuis votre fork  
   vers `CodeursPro/challenge_24_07_2026` (branche `main`).
2. Titre suggéré : `[Challenge] <votre-pseudo> — <cas d’usage>`
3. Dans la description, résumez :
   - cas d’usage ;
   - modèle local utilisé ;
   - points forts (anti hors-sujet, system prompt, etc.).

Les soumissions doivent être reçues **avant mercredi 23h59 GMT**.

---

## Comment ça marche (vue d’ensemble)

```text
┌─────────────────┐     fork      ┌──────────────────────────┐
│  Dépôt officiel │ ───────────►  │  Votre fork (personnel)  │
│  CodeursPro/   │               │  <user>/challenge_...    │
│  challenge_...  │ ◄───────────  │                          │
└─────────────────┘   Pull Request└──────────────────────────┘
         ▲
         │  revue / évaluation
         │
   Équipe Codeurs Pro
```

1. **Le dépôt officiel CodeursPro** sert de référence (énoncé + réception des PR).
2. **Chaque participant fork** pour avoir son propre espace de travail.
3. **Le développement se fait en local** : modèle LLM local (souvent Ollama) + votre code.
4. **Le system prompt** cadre le rôle du bot et limite les réponses hors sujet.
5. **La Pull Request** est votre soumission officielle pour l’évaluation.
6. **Les résultats** sont communiqués **vendredi soir**.

---

## Idées de cas d’usage

- **Assistant commercial** : présente une offre, répond aux objections, reste dans le catalogue.
- **FAQ universitaire** : inscriptions, emplois du temps, procédures administratives.
- **Assistant documentaire** : répond à partir d’un corpus local (PDF, notes, wiki).
- **Support produit** : guide l’utilisateur dans l’usage d’un logiciel / d’un service.

Peu importe le cas choisi : ce qui compte, c’est la **maîtrise du comportement** du modèle en local.

---

## Checklist avant soumission

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

Bonne chance à toutes et à tous — **Codeurs Pro**
