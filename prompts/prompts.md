# prompts.md - Versionnage des prompts utilisés en production

Ce fichier liste tous les prompts utilisés dans le code de l'application. Il est versionné avec le code pour qu'on puisse retracer l'historique des modifications.

## Pourquoi ce fichier

Un prompt n'est pas du code "mou" : c'est de la logique applicative. Une modification de prompt peut casser des comportements aussi sûrement qu'un changement d'algorithme. Le versionner avec Git permet de :
- Diffuser la connaissance dans l'équipe
- Diff facile entre versions
- Justifier les choix en soutenance
- Détecter les régressions sémantiques

## Format

Chaque prompt a une fiche structurée :
- **ID** : identifiant unique référencé dans le code
- **Localisation** : fichier où le prompt est utilisé
- **Modèle ciblé** : gemini-3.6-flash, etc.
- **Objectif** : ce qu'on veut obtenir
- **Prompt** : le texte exact
- **Paramètres associés** : température, max_tokens, schéma de sortie
- **Historique** : versions précédentes avec raison du changement
- **Notes** : pièges connus, cas qui plantent

---

## PROMPT-001 : Analyse de sentiment

**Localisation** : `backend/routers/chat.py`
**Modèle** : gemini-3.6-flash
**Objectif** : classifier le sentiment d'un texte court en positif/négatif/neutre, avec score de confiance.

**Prompt** :
```
Analyse le sentiment du texte suivant : {texte}
```

**Paramètres** :
- temperature : 0
- response_schema : Sentiment (Pydantic)
- system_instruction : (aucune)

**Historique** :
- v1 (date) : version initiale

**Notes** :
- Marche bien sur du texte français court (< 500 caractères)
- Sur du sarcasme, classifie souvent positif à tort

---

## PROMPT-002 : [À ajouter par le binôme]

[Suivez le même format pour chaque prompt utilisé dans votre code]

---

## Conventions

- Les variables interpolées sont entre `{accolades}`
- Les system prompts longs sont mis en bloc séparé avec triple backticks
- Si un prompt change, **on garde l'ancien** dans la section Historique pour audit
