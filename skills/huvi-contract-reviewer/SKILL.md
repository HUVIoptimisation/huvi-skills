---
name: huvi-contract-reviewer
description: "Analyse de contrats : risques, coûts, sortie, négociation."
version: 1.0.0
author: HUVI Optimisation
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [huvi, contrats, négociation, risques, juridique, revue]
    related_skills: []
---

# HUVI Revue de Contrats

Analyse un contrat de manière complète et structurée du point de vue de la personne qui l'a reçu — en français clair, orienté conséquences pratiques. Couvre : complétude du document, portée, obligations, coûts, risques, sortie, propriété intellectuelle, responsabilité, asymétrie entre les parties, puis priorités de négociation et verdict. Ce skill structure, alerte et prépare — il ne donne pas d'avis juridique et ne remplace jamais un avocat pour un contrat à enjeux élevés.

## Quand l'utiliser

- Un contrat reçu doit être analysé avant signature : service, mandat, licence, SaaS, partenariat, sous-traitance, client/fournisseur.
- Demande du type : « analyse ce contrat », « est-ce que je signe ? », « quels sont les risques ? », « que dois-je négocier ? ».
- Comparer les droits des deux parties et détecter les clauses déséquilibrées.
- Auditer son propre template avant envoi (rôle = rédacteur) : les constats sont les mêmes, les priorités s'inversent.
- Ne pas utiliser pour : rédiger un contrat de zéro, un litige déjà engagé, ou un dossier nécessitant un acte juridique (immobilier, succession) — rediriger vers un avocat/notaire.

## Principes directeurs

1. **Les 3 registres épistémiques — toujours distingués** :
   - **ÉCRIT** : ce que le contrat dit explicitement.
   - **INTERPRÉTATION** : le sens raisonnable d'une clause ambiguë, et pourquoi.
   - **RECOMMANDATION / RISQUE** : ce que l'utilisateur devrait clarifier, négocier ou refuser.
2. **Jamais inventer une clause.** Si le contrat ne dit rien, le dire : un silence n'est pas une clause, c'est un risque (le droit supplétif comble les vides — souvent au détriment de celui qui n'a pas négocié).
3. **Le rôle déclaré change la lecture** : une même clause (résiliation, PI, responsabilité) se lit différemment selon qu'on est client ou prestataire.
4. **L'asymétrie se prouve, ne se présume pas** : chaque droit d'une partie doit avoir son miroir chez l'autre.
5. **Profondeur proportionnelle à l'enjeu** : le mode d'analyse suit la valeur, la durée et le risque du contrat.
6. **Zéro citation juridique non vérifiée** : texte à jour vérifié en ligne (Légis Québec / Légifrance) ou référence embarquée datée. Jamais de mémoire.
7. **Une seule loi applicable par analyse** : la loi détectée détermine les références juridiques — jamais de mélange QC/FR. Si incertain → avertir, ne pas choisir au hasard.

## Modes d'analyse

Deux modes, décidés à l'étape 0 et annoncés dans l'en-tête du rapport :

| | **RAPIDE** | **COMPLET** |
|---|---|---|
| **Quand** | Contrat simple, courte durée, faible valeur, risque connu | Contrat important, longue durée, clauses atypiques, enjeux élevés, ou doute |
| **Parcours** | Étapes 1 → 2 → 4 → 6 → 8 → 12 (les autres étapes ne sont traitées que si un risque évident saute aux yeux) | Tout le workflow 1 → 12 |
| **Rapport** | Concis : verdict + essentiel, coûts, sortie, responsabilité, risques majeurs | Gabarit complet |

Règle : en cas de doute → COMPLET. L'utilisateur peut forcer un mode en le précisant (« analyse rapide » / « analyse complète »).

## Workflow

### 0. Choisir le mode
Estimer valeur, durée d'engagement et risque. Appliquer la grille des modes ci-dessus et annoncer le mode choisi.

### 1. Complétude, l'affaire, les parties et la loi applicable
- **Complétude du document — avant toute analyse.** Vérifier et signaler en tête de rapport les éléments essentiels absents, vides ou non remplis : parties identifiées, montant chiffré, date, objet, modalités de paiement, signatures. Un template avec champs vides (placeholders) n'est pas signable en l'état — le dire immédiatement, ne jamais l'analyser comme s'il était complet.
- **Documents référencés** : si le contrat renvoie à des annexes, CGV, bons de commande ou conditions en ligne (URL), vérifier s'ils sont joints ou accessibles. Tout document référencé non fourni est marqué « non analysé — exiger avant signature ». Les pièges vivent souvent dans les documents référencés, pas dans le contrat.
- Objet, montant, durée, contexte commercial (l'affaire derrière le contrat).
- Parties : noms légaux exacts, entités, juridiction d'incorporation, signataire et son autorité.
- **Détecter la loi applicable — arbre à suivre dans l'ordre** :
  1. **Clause expresse** (loi applicable / governing law) → cette loi régit l'analyse. Ne jamais appliquer une autre règle locale.
  2. **Pas de clause + indices de rattachement au Québec** (parties au Québec, exécution au Québec, contrat rédigé en français, mentions C.c.Q. / Loi 25 / Québec) → **défaut : droit québécois** — le cas le plus fréquent pour le public de ce skill. L'annoncer comme un choix par défaut motivé par les indices, pas comme une certitude.
  3. **Clause ou indices France** (loi française, Code civil français, établissement ou exécution en France) → droit français.
  4. **Autre juridiction nommée** → principes généraux uniquement ; ne pas appliquer les drapeaux QC/FR ; le dire explicitement.
  5. **Aucun indice** → **avertissement explicite dans le rapport** : « Loi applicable non spécifiée. En cas de litige, le tribunal retiendra la loi du lien le plus étroit (lieu d'exécution, domicile des parties). » Analyser en principes généraux et signaler les points où la réponse changerait selon la loi retenue. Pour un utilisateur au Québec, mentionner que le droit québécois est le défaut le plus probable — à confirmer par un professionnel si l'enjeu le justifie.
- **Sources vivantes** : quand une règle locale précise pèse sur une conclusion, vérifier son texte à jour en ligne avant de la citer — legisquebec.gouv.qc.ca (textes QC), legifrance.gouv.fr (textes FR), canlii.org (jurisprudence QC). Les références embarquées (`references/qc-flags.md`, `references/fr-flags.md`) sont des points de départ vérifiés à date : la loi évolue, le texte en ligne à jour prime. En cas d'accès impossible, citer la référence embarquée avec sa date de vérification.

### 2. Portée, livrables et changements
- Ce qui est inclus et **exclu** ; critères d'achèvement.
- Mécanique des changements de portée : écrit ? seuil d'approbation ? impact prix et délais ? signature obligatoire ?
- Sans clause de changements : risque majeur de « scope creep » — le signaler.

### 3. Obligations et calendrier
Engagements de chaque partie, délais, dates importantes. Produire la liste des dates-butoir (préavis, renouvellement, paiements, révisions).

### 4. Coûts et paiements (maths vérifiées)
Recalculer les totaux, durées et pourcentages. Identifier : frais, dépôts, retenues, délais de paiement, pénalités, intérêts, taxes, remboursements, indexation, minimums. Signaler tout coût **flou, variable, illimité ou contrôlé unilatéralement** par l'autre partie.

### 5. Acceptation et qualité
Délais de révision, processus d'approbation des livrables, clause de « réputé accepté », conséquence du silence. Absence de mécanisme = risque de rejet tardif en bloc.

### 6. Sortie et renouvellement
Durée d'engagement, renouvellement automatique, préavis, frais d'annulation, pénalités de sortie anticipée, obligations qui survivent, sortie pour convenance vs pour faute. Comparer les droits de sortie des deux parties.

### 7. PI, données et confidentialité
Propriété du travail, licences (portée, durée, exclusivité), droit de modifier/revendre/sous-licencier, droits après la fin du contrat, usage portfolio. Données personnelles : si le contrat traite des renseignements personnels, vérifier les drapeaux locaux pertinents (QC : Loi 25 — voir `qc-flags`).

### 8. Responsabilité et assurances
Plafonds, exclusions, indemnités, garanties, assurances requises, frais juridiques. Exceptions au plafond (faute lourde/intentionnelle, violation de confidentialité, PI...). Comparer la protection des deux parties.

### 9. Tableau d'asymétrie
Construire un tableau comparatif : qui peut résilier / retenir des paiements / céder le contrat / sous-traiter / changer les prix / plafonner sa responsabilité / utiliser le travail. Marquer chaque case où l'autre partie est mieux traitée.

### 10. Négociation — 3 priorités maximum
Pour chaque priorité : pourquoi elle compte, résultat à viser, solution de repli raisonnable, **formulation améliorée prête à proposer** (texte court, ton neutre). Classer : À CHANGER ABSOLUMENT / À CHANGER / SOUHAITABLE.

### 11. Questions à poser avant de signer
Liste finale des questions concrètes à adresser à l'autre partie (clarifications, vides, chiffres, documents référencés).

### 12. Synthèse et verdict
Résumé : obligations des deux parties, risques majeurs, dates, engagements financiers, clauses déséquilibrées, ambiguïtés. **Le verdict est annoncé en tête de rapport (section 1) et justifié en détail en clôture** :
- 🟢 FAIBLE PRÉOCCUPATION
- 🟡 NÉCESSITE DES CLARIFICATIONS
- 🔴 NÉCESSITE UNE RÉVISION JURIDIQUE PROFESSIONNELLE

## Structure du rapport de sortie

```
# Analyse de contrat — [Type / nom]
Point de vue : [rôle] · Loi applicable : [X] · Mode : rapide/complet
## 1. Verdict et essentiel — 5 lignes max, décision d'abord
   Verdict 🟢/🟡/🔴 · top 3 points à régler · alertes de complétude (montant, date, parties, annexes manquants)
## 2. Obligations et calendrier (dates-butoir)
## 3. Coûts et paiements — maths vérifiées
## 4. Risques (tableau : risque | impact concret | niveau | quoi faire)
## 5. Sortie et renouvellement
## 6. PI, données, confidentialité
## 7. Responsabilité
## 8. Tableau d'asymétrie
## 9. Négociation — priorités classées + formulations
## 10. Questions à poser avant de signer
## 11. Justification détaillée du verdict
```

Marquer en permanence les 3 registres (ÉCRIT / INTERPRÉTATION / RECOMMANDATION). Coter chaque risque FAIBLE / MOYEN / ÉLEVÉ. Le mode rapide produit un rapport allégé mais garde l'en-tête, le verdict en tête, les registres.

## Entrées

- Le contrat (texte intégral — requis ; si l'extraction d'un PDF est dégradée, demander une version texte propre).
- Rôle : client, prestataire, rédacteur ou autre (si absent, analyser les deux points de vue).
- Priorités de négociation (optionnel).
- Type de travail (optionnel — nécessaire pour l'analyse PI/portfolio).
- Loi applicable si connue (sinon, détectée à l'étape 1).
- Mode souhaité (optionnel — rapide ou complet ; sinon décidé à l'étape 0).

## Résultats attendus

1. Rapport structuré selon le gabarit de sortie, mode annoncé.
2. Verdict annoncé en tête, justifié en détail en clôture.
3. Trois registres épistémiques distingués en permanence — zéro clause inventée, silences signalés.
4. Complétude vérifiée : éléments manquants et documents référencés non fournis signalés en tête.
5. Chaque risque coté avec un exemple concret d'impact.
6. Tableau d'asymétrie complet (mode complet).
7. Loi applicable identifiée ou absence signalée — jamais de références juridiques mélangées.

## Exemple de prompt

```
Analyse ce contrat de façon complète, de mon point de vue en tant que [RÔLE : prestataire / client / les deux]. Réponds en français simple, orienté conséquences pratiques pour moi.

Contexte :
- Rôle : [RÔLE]
- Priorités de négociation : [ex. : éviter l'engagement long, protéger mon portfolio, plafonner ma responsabilité] (optionnel)
- Type de travail (si pertinent pour la PI) : [ex. : développement web, conseil, design]
- Loi applicable, si je la connais : [Québec / France / autre / je ne sais pas]

1. Complétude et parties — signale-moi d'abord ce qui manque ou n'est pas rempli (montant, date, parties, annexes, conditions référencées). Qui contracte avec qui, qui signe, quelle loi régit le contrat et quel tribunal serait compétent. Si la loi n'est pas précisée, détecte-la par les indices (parties, lieu d'exécution) et dis-moi clairement ce que tu retiens.
2. Portée et acceptation — ce que je dois livrer ou recevoir, ce qui est exclu, comment les changements sont gérés, comment le travail est accepté (délais, silence).
3. Obligations et calendrier — mes engagements, ceux de l'autre partie, dates et délais importants.
4. Coûts — toutes les obligations financières, totaux recalculés ; signale tout coût flou, variable, illimité ou contrôlé unilatéralement par l'autre partie.
5. Sortie — durée d'engagement, renouvellement automatique, préavis, pénalités, obligations qui survivent ; l'autre partie a-t-elle de meilleurs droits de sortie que moi ?
6. PI, données, confidentialité — qui possède le travail et les données, quels droits je cède, pour combien de temps, usage portfolio après la fin du contrat.
7. Responsabilité — plafonds, exclusions, indemnités ; suis-je moins protégé que l'autre partie ?
8. Asymétrie — tableau : qui peut résilier, retenir des paiements, céder, changer les prix, plafonner sa responsabilité, utiliser le travail ?
9. Risques majeurs — tableau : risque | impact concret sur moi | FAIBLE/MOYEN/ÉLEVÉ | quoi faire.
10. Négociation — 3 priorités maximum, classées À CHANGER ABSOLUMENT / À CHANGER / SOUHAITABLE ; pour chacune : pourquoi elle compte, le résultat à viser, une solution de repli, une formulation prête à proposer.
11. Synthèse et verdict — mes obligations, celles de l'autre partie, les risques majeurs, les dates importantes, les montants, les clauses déséquilibrées, les ambiguïtés, les questions à poser avant de signer. Termine par : 🟢 FAIBLE PRÉOCCUPATION / 🟡 NÉCESSITE DES CLARIFICATIONS / 🔴 NÉCESSITE UNE RÉVISION JURIDIQUE PROFESSIONNELLE — justifié.

Règle absolue : distingue toujours ce qui est ÉCRIT dans le contrat, ce qui est une INTERPRÉTATION raisonnable, et ce qui est une RECOMMANDATION. N'invente jamais une clause : si le contrat est silencieux, dis-le — un silence est un risque. Si des éléments essentiels manquent (montant, date, parties, annexes ou conditions référencées), signale-le en premier.

Contrat :
[COLLE LE CONTRAT]
```

## Ressources liées

- `references/qc-flags.md` — drapeaux juridiques si loi applicable = Québec (articles vérifiés Légis Québec, 2026-09-04).
- `references/fr-flags.md` — drapeaux juridiques si loi applicable = France (articles vérifiés Légifrance, 2026-09-04).
- `references/general-principles.md` — principes d'interprétation transversaux (civil law / common law).

## Dépendances

- Aucune obligatoire (autoportant).
- Pour toute règle locale pesante : consulter les textes officiels en ligne pendant l'analyse (legisquebec.gouv.qc.ca, legifrance.gouv.fr, canlii.org). Les références embarquées servent de points de départ datés et de filet de secours.

## Pièges

- **Un contrat incomplet n'est pas un contrat.** Template avec champs vides, montant absent, date absente, renvoi à des conditions non jointes : le signaler en premier, ne jamais analyser comme si le document était complet.
- **Les pièges vivent dans les documents référencés** (annexes, CGV, conditions en ligne). Non fournis = « non analysés — exiger avant signature ».
- **Extraction PDF dégradée** : tableaux, scans ou cellules illisibles → demander une version texte propre ou marquer explicitement les zones non analysées. Ne jamais deviner le contenu d'une zone illisible.
- **Jamais de mélange QC/FR** : une seule loi applicable par analyse. Le droit québécois est le défaut seulement si les indices de rattachement y penchent (parties ou exécution au Québec) ; le droit français ne s'active que sur clause ou indices explicites. Ex. : l'art. 1171 C.civ. (France) ne joue que pour un contrat d'adhésion régi par le droit français.
- **Art. 2125 C.c.Q. : l'épée est dans la main du client.** Dans un contrat de service régi par le droit québécois, le **client** peut résilier unilatéralement en tout temps, même prestation commencée ; le prestataire, lui, ne peut résilier que pour motif sérieux. Pour un prestataire, c'est un risque de sortie adverse à mitiger (frais de dédit, minimums, pénalités) — jamais une protection.
- **Art. 2129 C.c.Q. : pas de manque à gagner.** En cas de résiliation par le client, l'indemnité couvre frais et dépenses, travaux exécutés et biens fournis — pas le profit espéré, sauf clause expresse.
- **Silence ≠ acceptation.** Le « réputé accepté » n'existe que si une clause le prévoit. Sans délai de révision ferme, le client peut rejeter tardivement en bloc.
- **La loi change — vérifier en ligne.** Les références embarquées sont datées ; pour une conclusion importante, re-vérifier le texte officiel à jour avant de citer un article.
- **Clause ambiguë → clarifier par écrit, ne pas interpréter seul.** En cas de litige, la commune intention prime sur le sens littéral (art. 1425 C.c.Q.) et, dans le doute, la clause s'interprète contre celui qui l'a stipulée (art. 1432 C.c.Q.).
- **Ne jamais citer un article non vérifié.** Hors références du skill : « règle à vérifier par un professionnel ».
- **Ne pas donner d'avis juridique ferme.** Le verdict 🔴 existe pour rediriger vers un avocat — l'utiliser sans hésiter quand l'enjeu le justifie.

## Vérification

- [ ] Complétude signalée en tête : éléments manquants (montant, date, parties, annexes) listés.
- [ ] Documents référencés non fournis marqués « non analysés ».
- [ ] Les 3 registres (ÉCRIT / INTERPRÉTATION / RECOMMANDATION) sont distingués partout.
- [ ] Aucune clause inventée ; chaque silence important est signalé.
- [ ] Loi applicable identifiée par l'arbre de détection (clause → indices QC → indices FR → autre → avertissement) ; une seule référence juridique utilisée.
- [ ] Toute règle locale citée est vérifiée (texte en ligne à jour ou référence embarquée datée).
- [ ] Mode (rapide/complet) annoncé et adapté à la valeur et au risque du contrat.
- [ ] Verdict annoncé en tête, justifié en clôture.
- [ ] Maths des coûts recalculées (totaux, durées, pourcentages).
- [ ] Tableau d'asymétrie présent (mode complet).
- [ ] Risques cotés FAIBLE / MOYEN / ÉLEVÉ avec impact concret.
- [ ] Négociation : priorités classées + formulations prêtes à proposer.

## Historique des révisions

| Version | Date | Notes |
|---|---|---|
| v1.0.0 | 2026-09-04 | Publication publique dans la librairie HUVIoptimisation/huvi-skills (skills/huvi-contract-reviewer/) : test d'autonomie concluant (agent externe sans contexte → rapport conforme, trouvailles indépendantes). |
| v0.1.2 | 2026-09-04 | Test réel (2 contrats) : complétude du document + documents référencés (annexes/CGV/URL) en étape 1, verdict annoncé en tête du rapport, piège extraction PDF dégradée, cas d'usage « audit de son propre template ». |
| v0.1.1 | 2026-09-04 | Détection de la loi applicable (défaut Québec sur indices, bascule FR explicite, jamais de mélange), modes rapide/complet matérialisés, sources vivantes en ligne, prompt d'exemple reformulé. |
| v0.1.0 | 2026-09-04 | Ébauche initiale : workflow 12 étapes, registres épistémiques, gabarit de sortie, drapeaux QC vérifiés (Légis Québec). |
