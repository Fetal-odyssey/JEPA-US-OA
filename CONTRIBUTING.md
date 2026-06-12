# Guide de contribution — JEPA-US-OA

**Auteur principal** : Olivier Ami

## Conventions

- Tous les commits doivent être signés au nom d'**Olivier Ami** (`dr.olivierami@gmail.com`)
- Format des messages de commit : `type: description courte — YYYY-MM-DD`
  - Types : `feat` (nouvelle fonctionnalité), `fix` (correction), `data` (données), `eval` (résultats), `docs` (documentation)
- Branches : `main` (production), `dev` (développement), `exp/xxx` (expériences)

## Configuration Git locale

```bash
git config user.name "Olivier Ami"
git config user.email "dr.olivierami@gmail.com"
```

## Structure des notebooks

Chaque notebook doit commencer par un header incluant :
- Auteur, date, version
- Description de l'expérience
- Dépendances et données requises

*Olivier Ami — 2026*
