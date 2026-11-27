# ❄️ Neige SB — quand démarrer la production de neige à Superbagnères

> 📘 **Mode d'emploi détaillé pour ordinateur (PDF, 26 pages, avec captures d'écran)** :
> [docs/Neige-SB-mode-emploi-PC.pdf](docs/Neige-SB-mode-emploi-PC.pdf)

Page web à utiliser surtout sur téléphone. Elle indique, pour chaque altitude du domaine
(1450 m bas de station, 1800 m plateau, 1900 m booster, 2000 m, 2100 m haut de station et 2200 m), quand la production de neige
sera possible dans les 16 prochains jours (comme les diagrammes d'ensemble de Meteociel).

- Un seul fichier `index.html` (HTML + CSS + JavaScript), sans compilation.
- Les prévisions viennent en direct d'[Open-Meteo](https://open-meteo.com/) (gratuit, sans clé)
  au moment où l'on appuie sur **Calculer**. Rien n'est enregistré sur un serveur.
- Seuls les réglages (seuils, altitude choisie) sont gardés dans le téléphone (`localStorage`).

## Mettre la page en ligne (GitHub Pages)

1. Sur GitHub, ouvrir le dépôt, puis **Settings** → **Pages**.
2. Dans **Build and deployment** → **Source**, choisir **Deploy from a branch**.
3. Choisir la branche **main** et le dossier **/ (root)**, puis **Save**.
4. Après une ou deux minutes, la page est disponible à l'adresse :
   `https://p69gp84gk7-arch.github.io/M3t305up3rb4gn3r35/`

Chaque fusion d'une pull request dans `main` met la page à jour automatiquement.

## Mettre à jour

Le bouton **⟳ Mettre à jour**, à droite de la ligne d'état en haut de la page :

1. recharge l'application depuis GitHub Pages en contournant le cache du téléphone, pour récupérer la dernière
   version publiée après la fusion d'une pull request (utile surtout depuis l'écran d'accueil, où il n'y a pas
   de bouton « actualiser ») ;
2. relance aussitôt le calcul avec les prévisions du moment.

Si une nouvelle version a été installée, la ligne d'état l'indique. La date de la version installée est affichée
en bas de la page (« Version de l'application : … »). Sans connexion, la version actuelle est gardée et un
message l'indique. GitHub Pages peut mettre une à deux minutes à publier une fusion.

## Ajouter la page sur l'écran d'accueil du téléphone

L'icône est le logo de l'application, un nuage avec un flocon sur fond bleu nuit, et le nom court est « Neige SB ».
Le logo est dessiné une seule fois dans la page (SVG de l'en-tête) ; l'icône du navigateur et celle de
l'écran d'accueil (PNG 192 et 512 px) en sont tirées automatiquement.

- **iPhone (Safari)** : ouvrir la page, toucher le bouton **Partager** (carré avec une flèche),
  puis **Sur l'écran d'accueil** → **Ajouter**.
- **Android (Chrome)** : ouvrir la page, toucher le menu **⋮** en haut à droite,
  puis **Ajouter à l'écran d'accueil** (ou **Installer l'application**) → **Ajouter**.

La page s'ouvre alors comme une application. Il faut une connexion internet pour calculer.

## Téléphone, tablette et ordinateur

La même page s'adapte à la taille de l'écran :

- **Téléphone** : une colonne, barre d'onglets en bas de l'écran (au pouce).
- **Tablette** (à partir de 700 px de large) : les 6 altitudes sur une ligne, le bouton Calculer à côté de l'état
  des prévisions, les fenêtres de démarrage et les cartes sur 2 colonnes, calendrier plus grand, liens sur 4 colonnes.
- **Ordinateur et tablette en paysage** (à partir de 1100 px) : onglets en haut comme une application de bureau,
  page plus large et blocs côte à côte :
  - Résumé : « Jour par jour » à gauche, « Démarrages possibles » à droite ;
  - Calendrier : le calendrier et le détail du jour à gauche, le temps de fonctionnement à droite ;
  - Réglages : seuils et « Comment c'est calculé » à gauche, modèles utilisés à droite ;
  - mode simple : « maintenant » et « prochain démarrage » côte à côte.

Avec une souris, les boutons s'éclairent au survol.

## Ce que montre la page

La page est rangée en **6 onglets**, avec une barre en bas de l'écran. Le bouton **Calculer** et le choix de
l'altitude restent en haut. L'onglet ouvert est gardé dans le téléphone.

| Onglet | Contenu |
|---|---|
| **Résumé** | Jour par jour, Démarrages possibles |
| **Calendrier** | Calendrier à 15 jours façon Apple, temps de fonctionnement estimé (une barre par altitude) |
| **Graphiques** | Heure par heure, Diagramme des scénarios |
| **Tableaux** | Toutes les altitudes, Par modèle, Modèles indisponibles (avec choix des modèles affichés) |
| **Simulateur** | Simulateur de température humide, profil de la montagne (650 à 2100 m) |
| **Réglages** | Réglages des seuils, Modèles utilisés, Comment c'est calculé |


- **Altitude** : gros boutons pour choisir 1450, 1800, 1900, 2000, 2100 ou 2200 m.
- **Jour par jour** : pour chaque jour, un petit schéma de la pente avec 1450, 1800 et 2000 m
  coloré selon les chances d'avoir au moins 4 h de production, et les heures théoriques de
  démarrage → arrêt à chaque altitude (« veille » quand la production a commencé la veille,
  « lendemain » quand elle s'arrête le lendemain).
- **Modèles utilisés** : choix des modèles pris en compte dans tous les résultats. On peut choisir
  un seul modèle ou en cocher plusieurs : la page fait alors la moyenne, chaque modèle comptant
  autant. Des choix tout prêts sont proposés : Ensembles (par défaut), Météo-France
  (AROME HD, AROME, ARPEGE), Modèles fins, Tous, Aucun. Le choix est gardé dans le téléphone.
- **Démarrages possibles** : les périodes d'au moins 3 h où la majorité des scénarios météo
  disent « production possible », avec l'heure de démarrage et la dernière heure favorable,
  les chances au plus haut, la température de l'air et la température humide au démarrage et
  au plus froid, et le vent maximum. Pour les périodes des 48 prochaines heures, l'heure de
  démarrage selon AROME HD et les autres modèles fins.
- **Heure par heure** : graphique en barres des chances (couleur selon le pourcentage),
  avec une ligne verte quand AROME HD dit oui. Toucher une barre affiche le détail.
- **Diagramme des scénarios** : comme les diagrammes d'ensemble de Meteociel, une ligne fine par
  scénario d'un modèle d'ensemble (GFS par défaut : 30 scénarios + 1 de contrôle, comme Meteociel ;
  ou ECMWF 51, ICON 40, GEM 21, UKMO 18), avec la médiane, le run principal du même modèle quand
  il est disponible, et le seuil. Au choix : température humide, température de l'air ou vent.
  Une bande en bas donne la part des scénarios qui disent « production possible ».
- **Sûreté de la prévision** : chaque jour reçoit un indicateur ✔ sûre / ~ moyenne / ? incertaine,
  dans les cartes « Jour par jour » (modèles choisis, 3 altitudes) et en haut du diagramme des scénarios
  (modèle affiché). Le diagramme montre aussi la **zone de sûreté** : la bande où se trouvent 8 scénarios
  sur 10. Règle :
  - **sûre** : en moyenne sur la journée, au moins 9 scénarios sur 10 disent la même chose
    (accord |2p − 1| ≥ 0,8) **et** 8 scénarios sur 10 tiennent dans 3 °C de température humide ;
  - **incertaine** : accord < 0,5 (moins de 3 scénarios sur 4 d'accord) **ou** écart > 6 °C ;
  - **moyenne** : entre les deux.
- **Toutes les altitudes** : chances d'avoir au moins 4 h de production dans la journée.
- **Par modèle** : pour l'altitude choisie, le détail de chaque modèle jour par jour.
- **Modèles indisponibles** : les modèles qui n'ont pas répondu, avec la raison.
- **Comment c'est calculé** : explication simple, dans un encadré dépliable.
- **Bulles d'information** : un petit « i » à côté de chaque titre, de chaque tableau et de chaque modèle
  (dans « Modèles utilisés » et dans le tableau « Par modèle »). En le touchant, une bulle explique
  simplement ce que montre le bloc, ou d'où vient le modèle, sa précision et sa portée.

## Choix des modèles affichés dans le tableau

Dans l'onglet **Tableaux**, au-dessus du tableau « Par modèle », le petit bloc **Modèles à afficher** permet de
choisir les lignes du tableau : un bouton par modèle disponible, et des choix tout prêts (Tous, Utilisés dans le
calcul, Ensembles, Déterministes, Météo-France). Le choix est gardé dans le téléphone. Il ne change pas le
calcul (qui se règle dans Réglages › Modèles utilisés).

## Simulateur de température humide

Onglet **Simulateur** (fonctionne sans calcul ni connexion) :

- **En haut**, la température humide à **1800 m** (altitude de référence), en grand, colorée selon le niveau, et la
  température de l'air à ne pas dépasser pour atteindre le seuil avec l'hygrométrie choisie.
- **Curseurs** : température de l'air (sèche) de **−30 à +30 °C** (pas de 0,5 °C) et hygrométrie de **0 à 100 %**
  (pas de 1 %), avec boutons − / +. Le bouton « Utiliser les prévisions actuelles à 1800 m » reprend l'air, l'humidité et
  la variation de température prévues pour l'heure en cours (après « Calculer »).
- **Profil de la montagne** : 650 m (vallée de Luchon), 1450 m (bas de station), 1800 m (plateau, référence) et
  2100 m (haut de station), avec l'air, l'hygrométrie et la température humide à chaque altitude.
  - Les valeurs (température humide et air) sont écrites sur le schéma, à côté de chaque altitude, et dans la liste.
  - **Variation de la température avec l'altitude** (gradient) : **calculée automatiquement** selon la température et
    l'hygrométrie, sans réglage : moyenne pondérée par l'hygrométrie entre le gradient adiabatique humide (air saturé,
    calculé : environ −0,5 °C/100 m à +10 °C, −0,6 à 0 °C, −0,8 à −15 °C) et le gradient adiabatique sec (−0,98 °C/100 m).
    Exemples : 0 °C et 60 % → −0,76 ; −10 °C et 80 % → −0,78 ; +5 °C et 100 % → −0,54. Le bouton « Utiliser les prévisions
    actuelles » reprend à la place la variation prévue par les modèles (qui peut montrer une **inversion**), jusqu'au
    prochain réglage des curseurs.
  - **Humidité aux autres altitudes** : « même quantité d'eau dans l'air » (conseillé : rapport de mélange constant,
    l'hygrométrie suit la température et la pression, plafonnée à 100 % = saturé) ou « même hygrométrie partout ».
  - Le gradient prévu est calculé par régression linéaire des températures des niveaux de pression situés entre
    environ 300 et 2800 m (modèles AROME, ARPEGE, ECMWF, ICON, GFS, UKMO), moyenne des modèles.

Les réglages du simulateur sont gardés dans le téléphone.

### Canons : démarrage de l'installation

Dans le Simulateur, le bloc **Canons** applique la règle de démarrage : **au moins 25 canons à −3 °C de température
humide ou moins** (et un vent sous le seuil de l'onglet Réglages).

- **203 canons numérotés** (fichier `canons.kmz` fourni le 27/11/2026 : numéros et positions GPS). Le fichier ne contenant
  pas d'altitudes, elles ont été lues sur le relief Copernicus 90 m (API `elevation` d'Open-Meteo) : de 1436 à 2167 m ;
  le 25e canon le plus haut est à 1869 m. Seuls les numéros et positions sont dans la page (`CANONS` dans `index.html`).
- La température humide de chaque canon est calculée à son altitude à partir de l'air et de l'hygrométrie à 1800 m et de la
  variation avec l'altitude (même calcul que le profil de la montagne).
- Le calcul se fait **uniquement d'après les prévisions** (pas d'après les curseurs du simulateur) ; avant le premier calcul,
  un bouton « Calculer maintenant » est proposé.
- **Jour par jour** (après « Calculer ») : sélecteur de jour (15 jours, avec le nombre d'heures où l'on peut
  démarrer), barres heure par heure du nombre de canons prêts (vert : démarrage possible, orange : vent trop fort), heures
  de démarrage possibles ; air, hygrométrie et vent prévus à 1800 m, variation prévue par les modèles en altitude
  (sinon calcul automatique).
- **Plan** des canons (vert prêt, orange limite −2,5 à −3 °C, gris trop doux) ; toucher un point donne son numéro, son
  altitude et sa température humide ; **liste des numéros** des canons prêts.

## Humidité de l'air (hygrométrie)

Un air sec est favorable à la neige de culture : la température humide est plus basse que celle de l'air.
À 1800 m, pour obtenir −2,5 °C de température humide, il faut −1,9 °C d'air à 90 % d'humidité, −0,6 °C à 70 %,
**+0,9 °C à 50 %** et **+2,8 °C à 30 %**. L'humidité relative (déjà téléchargée pour le calcul) est maintenant affichée :

- **Graphiques** : courbe « Humidité de l'air » heure par heure (moyenne des modèles choisis, zone de 8 scénarios
  sur 10, repère 70 %, humidité moyenne de chaque jour) ; bouton **Humidité** dans le diagramme des scénarios ;
- **Calendrier** : 💧 humidité moyenne du jour dans chaque carré (altitude choisie) et pour chaque altitude dans le
  détail du jour ; humidité moyenne pendant la production au clic sur une barre ;
- **Résumé** : humidité « en ce moment », au démarrage et moyenne de chaque fenêtre, 💧 humidité du jour dans les
  cartes « Jour par jour » ;
- **Tableaux** : tableau « Humidité moyenne par jour » (altitudes × jours, très sec ≤ 50 %, sec 50–70 %,
  humide 70–85 %, très humide > 85 %) ;
- **Mode simple** : humidité maintenant et humidité moyenne de chaque jour.

L'humidité affichée est la valeur du milieu des scénarios de chaque modèle, puis la moyenne des modèles choisis ;
l'humidité du jour est la moyenne des heures de la journée (heures restantes pour aujourd'hui).

## Iso 0 °C et limite pluie-neige

Dans l'onglet **Graphiques**, le graphique **Iso 0 °C et limite pluie-neige** montre heure par heure, sur 16 jours :

- l'**iso 0 °C** (ligne orange) : altitude où l'air passe sous 0 °C ;
- la **limite pluie-neige** (ligne bleue) : en dessous, il pleut ; au-dessus, il neige ;
- les altitudes de la station en pointillés (1450 m, 2200 m et l'altitude choisie) ;
- les **précipitations** en bas (mm/h), en blanc s'il neige à l'altitude choisie, en vert s'il pleut.

Choix du modèle : **Moyenne des modèles** (par défaut, avec en zone claire l'écart entre modèles), ou AROME, ARPEGE,
ECMWF, ICON, GFS, UKMO. Survoler ou toucher le graphique donne les valeurs de l'heure.

**Calcul** : un appel par modèle (6 appels en plus, 29 au total) demande la température, l'humidité et l'altitude des
niveaux 1000, 925, 850, 800, 700, 600 et 500 hPa au-dessus du plateau. L'iso 0 est la plus haute altitude où la
température passe à 0 °C ; la limite pluie-neige est la plus haute altitude où la température humide passe à +1 °C
(interpolation entre niveaux). Vérifié le 25/11/2026 : l'iso 0 calculé est à moins de 100 m de l'iso 0 fourni par
GFS et ICON ; la limite pluie-neige est à ±250 m de celle d'ICON-EU. AROME HD ne fournit pas ces niveaux.

## Calendrier à 15 jours

Onglet **Calendrier** :

- **Temps de fonctionnement estimé** : une barre par altitude (2200 m en haut, 1450 m en bas) dont la longueur
  est le nombre d'heures des 15 prochains jours où l'on peut allumer l'installation, c'est-à-dire où au moins
  50 % des scénarios disent « production possible ». Partie bleu vif : 7 premiers jours ; bleu sombre : jours 8 à 15.
- **Calendrier**, façon calendrier Apple : une grille lundi → dimanche avec un petit carré par date pour les
  15 prochains jours (date du jour en rouge). Dans chaque carré, une mini-barre par altitude (2200 m en haut,
  1450 m en bas) sur 0 h – 24 h, allumée aux heures où l'on peut produire ; en bas, les heures de fonctionnement
  à l'altitude choisie ; un point de couleur donne la sûreté du jour. Toucher un carré affiche la journée en grand
  en dessous (une barre par altitude, heures exactes, trait « maintenant »), et toucher une barre en donne le détail
  (heures, chances, température humide la plus basse).

## Autres sites météo

En bas de l'onglet **Résumé** (et du mode simple), des boutons ouvrent dans un nouvel onglet les pages de
Superbagnères sur d'autres sites, pour comparer (adresses vérifiées le 22/11/2026) :

| Bouton | Page |
|---|---|
| Météo-France | bulletin montagne « Superbagnères 1800 m » (`meteofrance.com/meteo-montagne/superbagneres-1800m/314701`) |
| Meteociel — Diagramme GFS | diagramme d'ensemble GEFS à 30 scénarios pour Luchon-Superbagnères (42.768 N, 0.577 E) |
| Meteociel — AROME ensemble | diagramme PE-AROME (ensemble AROME de Météo-France) au même point |
| Meteociel — AROME heure par heure | prévisions fines AROME, page Luchon-Superbagnères n° 40001 |
| Meteociel — Tendances | tendances à 10 jours, page n° 40001 |
| Meteoblue — Semaine / Comparaison des modèles | pages calculées pour les coordonnées et l'**altitude choisie** |
| Snow-forecast | page de la station, **bas / milieu / haut** selon l'altitude choisie (< 1700 m, < 2100 m, au-dessus) |

Rien n'est récupéré automatiquement de ces sites : ce sont de simples liens.

## Mode simplifié

Le bouton **Mode simple** en haut à droite affiche seulement l'essentiel pour l'altitude choisie :

- **Maintenant** : production possible OUI ou NON (la majorité des scénarios dit oui pour l'heure en cours),
  avec la température humide et le vent ;
- **Prochain démarrage possible** : jour et heure, dernière heure favorable, chances et sûreté de la prévision ;
- **Les 7 prochains jours** : une grosse réponse par jour, selon les chances d'avoir au moins 4 h de production :
  **OUI** à 70 % ou plus, **PEUT-ÊTRE** de 40 à 69 %, **NON** en dessous, avec les heures de démarrage → arrêt
  et la sûreté.

Les onglets sont masqués dans ce mode. Le bouton **Mode complet** (ou « Voir le détail ») les fait revenir.
Le mode choisi est gardé dans le téléphone. Le calcul suit les seuils et les modèles réglés dans le mode complet.

## Le calcul

1. **Pression à l'altitude** : `P = 1013,25 × (1 − 2,25577e-5 × altitude)^5,25588` (hPa).
2. **Température humide** `Tw`, heure par heure, trouvée par dichotomie dans
   `es(Tw) − 0,00066 × (1 + 0,00115 × Tw) × P × (T − Tw) = e`,
   avec `es(T) = 6,112 × exp(17,62 × T / (243,12 + T))` et `e = humidité/100 × es(T)`.
   Contrôle : 0 °C et 50 % d'humidité à 1800 m donnent −3,3 °C (vérifié au chargement de la page).
3. **Production possible** si `Tw ≤ −2,5 °C` **et** vent à 10 m `≤ 15 km/h`.
   Les deux seuils se règlent dans la page.
4. **Niveaux** : de −2,5 à −3 °C = limite ; −3 °C ou moins = production ; −6 °C ou moins = excellent.
5. **Pourcentage de chances** : pour chaque heure, part des membres (scénarios) de chaque
   modèle choisi qui disent « production possible », puis moyenne entre les modèles choisis
   (chaque modèle compte autant, quel que soit son nombre de membres). Par défaut, ce sont les
   6 modèles d'ensemble. Un modèle déterministe compte comme un modèle avec un seul scénario
   (0 % ou 100 %). Au-delà de la portée d'un modèle, la moyenne continue avec les autres.
6. **Fenêtres** : de la première à la dernière heure où au moins 50 % des scénarios disent oui,
   seulement si elles durent au moins 3 h.
7. **Tableau par jour** : part des scénarios qui ont au moins 4 h de production dans la journée
   (pour aujourd'hui, seulement sur les heures restantes).

Les coordonnées de chaque point sont envoyées avec le paramètre `elevation`, qui corrige
la prévision pour l'altitude exacte. Les 6 points partent dans le même appel.
Fuseau horaire Europe/Paris, vent en km/h, 16 jours de prévision (moins pour les modèles qui
vont moins loin). Les 7 premiers jours sont affichés d'office ; les jours 8 à 16, moins sûrs,
s'ouvrent avec un bouton « Voir les jours 8 à 16 ».

## Points utilisés

| Altitude | Rôle | Latitude | Longitude | Altitude du terrain à ces coordonnées* |
|---|---|---|---|---|
| 1450 m | bas de station | 42.7556 | 0.5747 | 1456 m |
| 1800 m | plateau | 42.7576 | 0.5747 | 1567 m |
| 1900 m | booster | 42.7530 | 0.5650 | 1468 m |
| 2000 m | | 42.7480 | 0.5560 | 1499 m |
| 2100 m | haut de station | 42.7440 | 0.5480 | 1596 m |
| 2200 m | | 42.7395 | 0.5410 | 1820 m |

\* Relief Copernicus 90 m, lu via l'API `elevation` d'Open-Meteo le 22/11/2026.
Les coordonnées sont approximatives : c'est le paramètre `elevation` qui impose l'altitude
utilisée pour corriger les prévisions, donc le calcul se fait bien à 1450, 1800… 2200 m.
Les coordonnées servent seulement à choisir la maille du modèle. Le point à 1450 m est provisoire
(point le plus proche du plateau à environ 1450 m sur le relief) : à remplacer par les
coordonnées réelles du bas de station.
Le contrôle « le modèle renvoie-t-il des données ? » se fait sur le point 1800 m.

## Modèles météo

Chaque modèle est appelé séparément ; un modèle en panne ne bloque pas les autres.
La page garde seulement ceux qui renvoient des données au point 1800 m et affiche la liste des autres.

### Modèles d'ensemble (pourcentages de chances)

API `https://ensemble-api.open-meteo.com/v1/ensemble`. Tous testés le 22/11/2026 sur les points d'altitude,
avec 16 jours demandés à partir de minuit (384 h au maximum).

| Modèle | Code | Membres | Portée mesurée |
|---|---|---|---|
| ECMWF | `ecmwf_ifs025` | 51 | 364 h (15 j) |
| ECMWF IA | `ecmwf_aifs025` | 51 | 373 h (15 j) |
| GFS (États-Unis) | `gfs_seamless` | 31 | 384 h (16 j) |
| ICON (Allemagne) | `icon_seamless_eps` | 40 | 182 h (7,5 j) |
| GEM (Canada) | `gem_global` | 21 | 384 h (16 j) |
| UKMO (Royaume-Uni) | `ukmo_global_ensemble_20km` | 18 | 248 h (10 j) |

Pour le GFS, `gfs_seamless` remplace `gfs025` : ce sont les mêmes 31 scénarios (30 + 1 de contrôle,
comme le diagramme GEFS de Meteociel), à 0,25° jusqu'à 10 jours puis à 0,5° jusqu'à 16 jours.
`gfs025` seul s'arrête à 10 jours (250 h).

### Modèles déterministes (précision à court terme)

API `https://api.open-meteo.com/v1/forecast`. Testés le 22/11/2026 sur le point 1800 m, avec
16 jours demandés à partir de minuit (384 h au maximum). La portée dépend de l'heure du dernier
calcul du modèle et varie donc de quelques heures d'un jour à l'autre.

| Modèle | Code | Maille | Portée mesurée | Dans les fenêtres 48 h |
|---|---|---|---|---|
| AROME HD (prioritaire) | `meteofrance_arome_france_hd` | 1,5 km | 62 h | oui ★ |
| AROME | `meteofrance_arome_france` | 2,5 km | 62 h | oui |
| HARMONIE (Danemark) | `dmi_harmonie_arome_europe` | 2 km | 70 h | oui |
| HARMONIE (Pays-Bas) | `knmi_harmonie_arome_europe` | 5,5 km | 73 h | oui |
| ICON-EU | `icon_eu` | 7 km | 128 h | oui |
| ARPEGE | `meteofrance_arpege_europe` | 10 km | 110 h | oui |
| UKMO | `ukmo_global_deterministic_10km` | 10 km | 170 h | oui |
| Météo-France (mixte) | `meteofrance_seamless` | 1,5 à 25 km | 110 h | non |
| ECMWF | `ecmwf_ifs025` | 25 km | 364 h | non |
| ECMWF IA | `ecmwf_aifs025_single` | 25 km | 373 h | non |
| ICON | `icon_global` | 13 km | 182 h | non |
| GFS | `gfs_global` | 13 km | 384 h | non |
| GEM | `gem_global` | 15 km | 242 h | non |
| JMA (Japon) | `jma_gsm` | 55 km | 271 h | non |
| CMA (Chine) | `cma_grapes_global` | 15 km | 130 h | non |

Cas particuliers constatés le 22/11/2026 :

- `gfs_graphcast025` (GraphCast) et `kma_gdps` (KMA) répondent mais **sans aucune valeur**
  pour Superbagnères. Ils restent dans la liste au cas où les données reviennent ; en attendant,
  la page les affiche dans « Modèles indisponibles ».
- `italia_meteo_arpae_icon_2i` (ICON-2I) **ne couvre pas** Superbagnères
  (« No data is available for this location ») : il a été retiré de la page.

## Limites à connaître

- Open-Meteo gratuit autorise 10 000 appels par jour et par adresse internet. Chaque appui sur
  **Calculer** fait 29 appels (les 6 altitudes partent ensemble dans chaque appel) : pas de souci pour un usage normal depuis un téléphone.
  Si le quota est dépassé, les modèles concernés apparaissent dans « Modèles indisponibles ».
- Avec 16 jours, un calcul télécharge environ 8 Mo (surtout les ensembles ECMWF et ICON) :
  préférer le wifi ou une bonne couverture 4G.
- C'est une aide à la décision : les mesures sur place (sonde, hygromètre, anémomètre) restent la référence.

Données météo : [Open-Meteo.com](https://open-meteo.com/), licence CC BY 4.0.
