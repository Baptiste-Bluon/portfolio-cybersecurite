# Revue de configuration — [PÉRIMÈTRE]

| | |
|---|---|
| **Client** | Client [A/B/C] — [secteur, effectif approximatif] |
| **Périmètre audité** | [ex. tenant Microsoft 365 — Entra ID, Exchange Online, comptes à privilèges] |
| **Hors périmètre** | [ex. postes de travail, infrastructure on-premise, applications métier] |
| **Date de la revue** | JJ/MM/AAAA |
| **Auditeur** | Baptiste Bluon |
| **Méthode** | Revue de configuration en lecture seule. Aucun test d'intrusion, aucune modification. |
| **Référentiels** | Guide d'hygiène ANSSI ; CIS Benchmark [version] ; ISO/IEC 27002:2022 |

---

## 1. Synthèse pour la direction

> À rédiger en dernier, en 5 à 8 lignes, sans aucun terme technique.
> Structure : niveau de maturité constaté → les 2 risques majeurs exprimés en conséquences métier
> (interruption d'activité, perte de données clients, non-conformité) → l'effort de remédiation
> en ordre de grandeur → la recommandation prioritaire unique.

**Niveau de maturité constaté :** [Faible / Partiel / Satisfaisant]

[Rédaction]

**Recommandation prioritaire :** [une seule phrase]

---

## 2. Vue d'ensemble des constats

| Criticité | Nombre | Délai de traitement recommandé |
|---|---|---|
| Critique | | Immédiat (< 7 jours) |
| Majeur | | 1 mois |
| Mineur | | 3 mois |
| Observation | | Au fil de l'eau |

**Échelle de criticité retenue**

| Niveau | Définition |
|---|---|
| **Critique** | Exploitation directe possible, impact majeur sur la confidentialité ou la disponibilité. Aucune mesure compensatoire. |
| **Majeur** | Écart significatif au référentiel, exploitation nécessitant une condition supplémentaire. |
| **Mineur** | Écart réel, impact limité ou mesure compensatoire existante. |
| **Observation** | Pas d'écart, mais amélioration recommandée. |

---

## 3. Constats détaillés

### C-01 — [Titre factuel du constat]

| | |
|---|---|
| **Criticité** | Critique |
| **Mesure ISO 27002:2022** | 8.2 — Droits d'accès à privilèges |
| **Autre référentiel** | ANSSI — mesure n° [x] |

**Constat**
[Ce qui a été observé, factuellement, avec la donnée chiffrée. Pas d'interprétation.]
*Exemple : 4 comptes disposent du rôle Administrateur général. 2 d'entre eux ne sont pas
protégés par une authentification multifacteur. 1 n'a pas été utilisé depuis 214 jours.*

**Risque**
[La conséquence concrète si le constat est exploité — en termes métier, pas techniques.]

**Recommandation**
1. [Action précise, vérifiable, assignable]
2. [Action suivante]

**Effort estimé** : [heures ou jours] — **Prérequis** : [validation client, fenêtre de maintenance, licence…]

---

### C-02 — [Titre]

*(dupliquer le bloc ci-dessus)*

---

## 4. Plan de remédiation priorisé

| ID | Constat | Criticité | Effort | Responsable | Échéance |
|---|---|---|---|---|---|
| C-01 | | Critique | | | |
| C-02 | | Majeur | | | |

---

## 5. Limites de la revue

- Revue documentaire et de configuration uniquement — aucune vérification par test offensif.
- État constaté à la date indiquée ; toute modification postérieure invalide les constats.
- [Éléments non accessibles pendant la revue]

---

## Annexe — Correspondance constats / mesures ISO 27002:2022

| Constat | Mesure | Thème |
|---|---|---|
| C-01 | 8.2 | Technologique |

---

### Règles de rédaction (à supprimer du livrable final)

1. **Un constat = un fait mesurable.** « La politique de mots de passe est faible » n'est pas un constat.
   « La longueur minimale est de 8 caractères, sans exigence de complexité » en est un.
2. **Jamais de recommandation dans le constat**, et jamais de constat dans la recommandation.
3. **Anonymisation systématique** : pas de nom de client, de domaine, d'IP, de nom de compte réel.
4. **La synthèse direction se rédige en dernier** et doit être compréhensible par un dirigeant non technique.
   C'est la partie que le client lit vraiment.
5. **Ne jamais écrire un constat non vérifié.** Un auditeur perd sa crédibilité sur un seul faux constat.
