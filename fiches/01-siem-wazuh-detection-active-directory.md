# Déploiement d'un SIEM et conception de règles de détection sur Active Directory

**Contexte** — Projet annuel, Bachelor 3 Sécurité informatique, ESGI Lyon (2025-2026)
**Rôle** — Responsable du lot Sécurité / SIEM, en équipe de 4
**Durée** — Année universitaire, en parallèle de l'alternance
**Technologies** — Wazuh 4.14, Active Directory (Windows Server 2022), Proxmox VE, OPNsense, Debian 12, MITRE ATT&CK, CIS Benchmarks

---

## Situation

Le projet consistait à concevoir l'infrastructure sécurisée d'un cabinet comptable fictif de 37 salariés, manipulant des données soumises au secret professionnel et au RGPD. Le besoin principal exprimé était une absence totale de visibilité sur les événements de sécurité, doublée d'une crainte de rançongiciel après qu'un cabinet concurrent avait été chiffré.

J'ai pris en charge le lot détection et réponse, ainsi que le durcissement de l'annuaire.

## Action

**Déploiement du SIEM.** Installation du manager Wazuh sur une machine dédiée et enrôlement de 7 agents sur un parc hétérogène : contrôleurs de domaine Windows Server, poste de travail Windows 11, hyperviseur Proxmox, serveurs Debian, hôte de conteneurs.

**Conception de règles de détection personnalisées.** Au-delà des règles natives, j'ai développé une trentaine de règles réparties en trois familles — authentification et force brute, intégrité de l'hyperviseur, persistance sur Active Directory — chacune rattachée à une technique du référentiel MITRE ATT&CK. La règle dont je suis le plus satisfait est une corrélation qui détecte une substitution de compte d'administration (retrait puis ajout d'un membre dans un groupe à privilèges en moins de 60 secondes), scénario invisible pour les règles natives prises isolément.

**Surveillance d'intégrité et conformité.** Configuration du FIM en temps réel sur les fichiers sensibles (base de l'annuaire, ruches SAM/SYSTEM, secrets système Linux, configuration et clés du cluster de l'hyperviseur) et exploitation du module SCA pour un audit continu contre les benchmarks CIS.

**Réponse automatisée.** Mise en place du blocage automatique de l'adresse source au niveau du pare-feu de l'hôte sur détection d'échecs d'authentification répétés, et alerting par courriel au-delà d'un seuil de gravité.

**Durcissement de l'annuaire.** Contribution au modèle de tiering des comptes d'administration T0/T1/T2 et aux GPO de durcissement CIS.

## Résultat

- Chaîne complète **détection → alerte → blocage** validée par des scénarios d'attaque contrôlés menés depuis une machine Kali positionnée côté WAN : force brute SSH bloquée automatiquement, création puis suppression d'un compte administrateur détectées et remontées par courriel avec la chronologie complète des événements.
- Cartographie des règles vers MITRE ATT&CK documentée et livrée en annexe du rapport.
- Audit de conformité CIS opérationnel, fournissant un score de durcissement et des recommandations exploitables.

## Difficulté rencontrée et résolution

Après une montée de version majeure de Wazuh, mes règles personnalisées ont cessé de se déclencher sur les événements de l'annuaire. Le diagnostic a montré que la priorité de l'arbre de décodage faisait masquer mes règles par les règles natives. La résolution a consisté à rattacher explicitement chaque règle personnalisée à la règle native concernée et à ajuster le décodage.

Ce type d'incident est instructif : une règle de détection qui ne se déclenche plus est silencieuse. Rien ne signale sa défaillance. J'en ai tiré la conclusion qu'un dispositif de détection doit être **testé périodiquement**, et pas seulement à sa mise en place.

## Enseignement

Concevoir les règles m'a obligé à comprendre précisément quelles traces une infrastructure produit lorsqu'elle est attaquée — quels Event ID, quelles séquences, quels angles morts. C'est exactement le raisonnement que demande un audit d'architecture : savoir quoi vérifier, et savoir ce qui ne serait pas détecté.

C'est ce qui m'a orienté vers l'audit d'architecture et de configuration plutôt que vers le SOC en production.

## Limites assumées

- Remontée des journaux du pare-feu vers le SIEM restée partielle.
- Deux scénarios de test (dépôt de fichier EICAR, modification d'un fichier système) reposaient sur une configuration FIM documentée, mais les captures d'alerte n'ont pas été conservées — la preuve du résultat manque, la configuration qui le rend possible est documentée.

---

*Rapport de projet complet disponible sur demande.*
