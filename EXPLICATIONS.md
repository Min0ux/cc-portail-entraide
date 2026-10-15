# EXPLICATIONS — CC Git (A2 - S2)

**GALLAND / Emma :** 

## 1. Point de départ

- Commit de départ de `main` : `76184a8` (« Ajouter le conseil de vérification du compteur »).
- Historique fourni : `4a266e1`, `b88cc98`, `76184a8` sur `main` ; `a43f314` sur `feature/tutorat`.
- Identité configurée avant mes commits : `git config user.name` / `user.email` (Min0ux - Emmagalland72@gmail.com) .

## 2. Branches : rôle et point de départ

| Branche | Rôle | Part de |
|---|---|---|
| `feature/accueil` | Annonce de l'accueil libre sans inscription | `76184a8` |
| `feature/contact` | Adresse de contact cliquable (`mailto:`) | `76184a8` |
| `feature/tutorat` | Contribution fournie (tutorat sur inscription) | `76184a8` |
| `hotfix/duree` | Annulation de la durée erronée | `33421e9` (main intégré) |

## 3. Mes changements

- `82ca883` sur `feature/accueil` : j’ai modifié le paragraphe permanence d’index.html pour annoncer un accueil libre sans inscription le jeudi à 16 h.
- `21c139b` sur `feature/contact` : j’ai rendu l’adresse entraide@example.org cliquable avec un lien mailto:.
- Fusion de `feature/accueil` dans `main` : avancement simple (fast-forward), sans nouveau commit.
- Fusion de `feature/contact` dans `main` : commit de fusion `33ca122`, sans conflit. Les deux branches sont parties du même commit 76184a8 et touchent des lignes différentes.

## 4. Conflit rencontré

- **État constaté :** `git merge feature/tutorat` a signalé un conflit dans `index.html`, paragraphe `permanence`. Le message CONFLICT (content): Merge conflict in index.html, les marqueurs <<<<<<< HEAD, ======= et >>>>>>> feature/tutorat dans le fichier, et les deux phrases en concurrence (accueil à 16 h contre tutorat à 16 h 30).
- **Pourquoi les branches ont divergé :** feature/accueil et feature/tutorat sont parties du même commit 76184a8.
Chacune a modifié la même ligne (le paragraphe permanence) avec un contenu différent, donc Git ne peut pas choisir seul.
feature/contact n’a pas causé de conflit parce qu’elle touchait une autre ligne.
- **Ce que j'ai tenté / décidé :** J’ai remplacé le bloc de conflit (marqueurs compris) par deux paragraphes : l’accueil libre sans inscription à 16 h, puis le tutorat individuel sur inscription à 16 h 30, pour garder les deux informations.
- **Résultat :** commit de fusion `33421e9`, parents `33ca122` et `a43f314`.
- **Vérification :** Recherche des marqueurs avec Select-String : aucun résultat.
- git status propre, sans mention de merging.
- Recherche de Accueil libre|Tutorat|mailto dans index.html : les trois sont présents.
- Page ouverte dans le navigateur : les deux informations sont lisibles et distinctes.

## 5. Erreur annulée

- Commit erroné : `b88cc98bf3fae11998895be8365305f22b2cc49c`, qui a porté la durée de 20 à 200 minutes.
- Pourquoi `git revert` et pas un retour en arrière de la branche : [expliquez : l'historique est partagé, on ne le réécrit pas].
- Commit d'annulation : `31f2a00`, créé sur `hotfix/duree` puis fusionné dans `main` (fast-forward).
- Le commit suivant (`76184a8`, conseil du README) est conservé.

## 6. Tests

| Test | Attendu | Observé |
|---|---|---|
| Avant : durée affichée | 200 min | 200 min |
| Avant : 2 clics | 2 créneaux · 400 min | 400 min |
| Après : durée affichée | 20 min | 20 min |
| Après : 2 clics | 2 créneaux · 40 min | 40 min  |
| Après : Recommencer | 0 créneau · 0 min | 0 créneau · 0 min  |
| Après : contenu | conseil README, accueil 16 h, tutorat 16 h 30, contact cliquable | Idem |

## 7. Publication

- Dépôt public : [\[URL\]](https://github.com/Min0ux/cc-portail-entraide).
- Dernier `main` vérifié localement (`git rev-parse main`) et sur GitHub avant EXPLICATIONS.md : `31f2a00`.
- Branches publiées : `main`, `feature/accueil`, `feature/contact`, `feature/tutorat`, `hotfix/duree`.

## 8. Difficultés supplémentaires



## 9. Aides et vérifications personnelles

- **Aide reçue :** j'ai utilisé Claude (assistant IA) pour obtenir la marche à suivre et les commandes Git, et pour relire la structure de ce document. modifications des fichiers, résolution du conflit, rédaction.
- **Ce que j'ai vérifié moi-même :** exemples réels : `git log --graph`, `git diff` avant chaque commit, tests dans le navigateur, comparaison des hashes avec GitHub