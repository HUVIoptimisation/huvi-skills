# HUVI Contract Reviewer

Analyse complète et structurée d'un contrat du point de vue de la personne qui l'a reçu — en français clair, orienté conséquences pratiques. Risques, coûts, sortie, propriété intellectuelle, responsabilité, asymétrie entre les parties, priorités de négociation avec formulations prêtes à proposer, et verdict final.

Développé par [HUVI Optimisation](https://huvioptimisation.com) — automatisation, structure opérationnelle et systèmes d'entreprise.

## Ce que ce skill fait

- Analyse un contrat (service, mandat, licence, SaaS, partenariat, sous-traitance) avant signature.
- Détecte la loi applicable (défaut Québec sur indices de rattachement, bascule explicite vers le droit français, jamais de mélange).
- Distingue en permanence ce qui est **écrit** dans le contrat, ce qui est une **interprétation** raisonnable, et ce qui est une **recommandation**.
- Identifie les risques avec impact concret (FAIBLE / MOYEN / ÉLEVÉ), le tableau d'asymétrie entre les parties, les 3 priorités de négociation avec formulations prêtes à proposer, et un verdict 🟢 / 🟡 / 🔴.
- Deux modes : **rapide** (contrats simples) et **complet**.

Le skill structure, alerte et prépare — il ne donne pas d'avis juridique et ne remplace pas un avocat pour les contrats à enjeux élevés.

## Installation

Copiez le dossier `skills/huvi-contract-reviewer/` dans le répertoire des skills de votre agent (par exemple `~/.hermes/skills/` pour Hermes Agent, ou le répertoire de skills de votre assistant IA).

Le dossier contient :

```
skills/huvi-contract-reviewer/
├── SKILL.md                    ← le skill (instruction principale)
└── references/
    ├── qc-flags.md             ← règles du droit québécois (activées si loi = Québec)
    ├── fr-flags.md             ← règles du droit français (activées si loi = France)
    └── general-principles.md   ← principes d'interprétation transversaux
```

## Exemple d'utilisation

```
Analyse ce contrat de façon complète, de mon point de vue en tant que [RÔLE : prestataire / client / les deux].
Réponds en français simple, orienté conséquences pratiques pour moi.
- Priorités de négociation : [optionnel]
- Type de travail (si pertinent pour la PI) : [optionnel]
- Loi applicable, si je la connais : [Québec / France / autre / je ne sais pas]

Contrat : [COLLE LE CONTRAT]
```

## Licence

MIT — utilisation libre, mention de HUVI Optimisation appréciée.

---

[huvioptimisation.com](https://huvioptimisation.com) · HUVI Optimisation — Automatisation, structure opérationnelle et systèmes d'entreprise
