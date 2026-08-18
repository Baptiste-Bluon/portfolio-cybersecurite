# Règles de détection Wazuh

Extraits du fichier `local_rules.xml` développé pour le projet annuel décrit dans la
[fiche 01](../fiches/01-siem-wazuh-detection-active-directory.md) — environ trente règles
réparties en trois familles : authentification et force brute, intégrité de l'hyperviseur,
persistance sur Active Directory.

Les règles publiées ici proviennent d'un laboratoire (infrastructure fictive, projet
académique).

| Règle | Ce qu'elle détecte | Technique MITRE |
| --- | --- | --- |
| [100406](ad-substitution-compte-privilegie.xml) | Substitution d'un membre dans un groupe d'administration par un même opérateur en moins de 60 s — invisible pour les règles natives prises isolément | T1531 / T1098.007 |

Le fichier inclut les deux règles parentes (100403 ajout, 100405 retrait) sans lesquelles
la corrélation n'est pas lisible.
