# ❄️ Neige SB — quand démarrer la production de neige à Superbagnères

Page web à utiliser surtout sur téléphone. Elle indique, pour chaque altitude du domaine
(1450 m bas de station, 1800 m front de neige, 1900, 2000, 2100 et 2200 m), quand la production de neige
sera possible dans les 7 prochains jours.

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

## Ajouter la page sur l'écran d'accueil du téléphone

L'icône est un flocon ❄️ et le nom court est « Neige SB ».

- **iPhone (Safari)** : ouvrir la page, toucher le bouton **Partager** (carré avec une flèche),
  puis **Sur l'écran d'accueil** → **Ajouter**.
- **Android (Chrome)** : ouvrir la page, toucher le menu **⋮** en haut à droite,
  puis **Ajouter à l'écran d'accueil** (ou **Installer l'application**) → **Ajouter**.

La page s'ouvre alors comme une application. Il faut une connexion internet pour calculer.

## Ce que montre la page

- **Altitude** : gros boutons pour choisir 1450, 1800, 1900, 2000, 2100 ou 2200 m.
- **Démarrages possibles** : les périodes d'au moins 3 h où la majorité des scénarios météo
  disent « production possible », avec l'heure de démarrage et la dernière heure favorable,
  les chances au plus haut, la température de l'air et la température humide au démarrage et
  au plus froid, et le vent maximum. Pour les périodes des 48 prochaines heures, l'heure de
  démarrage selon AROME HD et les autres modèles fins.
- **Heure par heure** : graphique en barres des chances (couleur selon le pourcentage),
  avec une ligne verte quand AROME HD dit oui. Toucher une barre affiche le détail.
- **Toutes les altitudes** : chances d'avoir au moins 4 h de production dans la journée.
- **Par modèle** : pour l'altitude choisie, le détail de chaque modèle jour par jour.
- **Modèles indisponibles** : les modèles qui n'ont pas répondu, avec la raison.
- **Comment c'est calculé** : explication simple, dans un encadré dépliable.

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
   modèle d'ensemble qui disent « production possible », puis moyenne entre modèles
   (chaque modèle compte autant, quel que soit son nombre de membres).
6. **Fenêtres** : de la première à la dernière heure où au moins 50 % des scénarios disent oui,
   seulement si elles durent au moins 3 h.
7. **Tableau par jour** : part des scénarios qui ont au moins 4 h de production dans la journée
   (pour aujourd'hui, seulement sur les heures restantes).

Les coordonnées de chaque point sont envoyées avec le paramètre `elevation`, qui corrige
la prévision pour l'altitude exacte. Les 6 points partent dans le même appel.
Fuseau horaire Europe/Paris, vent en km/h, 7 jours de prévision.

## Points utilisés

| Altitude | Rôle | Latitude | Longitude | Altitude du terrain à ces coordonnées* |
|---|---|---|---|---|
| 1450 m | bas de station | 42.7556 | 0.5747 | 1456 m |
| 1800 m | front de neige | 42.7576 | 0.5747 | 1567 m |
| 1900 m | | 42.7530 | 0.5650 | 1468 m |
| 2000 m | | 42.7480 | 0.5560 | 1499 m |
| 2100 m | | 42.7440 | 0.5480 | 1596 m |
| 2200 m | haut | 42.7395 | 0.5410 | 1820 m |

\* Relief Copernicus 90 m, lu via l'API `elevation` d'Open-Meteo le 22/11/2026.
Les coordonnées sont approximatives : c'est le paramètre `elevation` qui impose l'altitude
utilisée pour corriger les prévisions, donc le calcul se fait bien à 1450, 1800… 2200 m.
Les coordonnées servent seulement à choisir la maille du modèle. Le point à 1450 m est provisoire
(point le plus proche du front de neige à environ 1450 m sur le relief) : à remplacer par les
coordonnées réelles du bas de station.
Le contrôle « le modèle renvoie-t-il des données ? » se fait sur le point 1800 m.

## Modèles météo

Chaque modèle est appelé séparément ; un modèle en panne ne bloque pas les autres.
La page garde seulement ceux qui renvoient des données au point 1800 m et affiche la liste des autres.

### Modèles d'ensemble (pourcentages de chances)

API `https://ensemble-api.open-meteo.com/v1/ensemble`. Tous testés le 22/11/2026 sur les points d'altitude.

| Modèle | Code | Membres | Portée |
|---|---|---|---|
| ECMWF | `ecmwf_ifs025` | 51 | 168 h (7 j demandés) |
| ECMWF IA | `ecmwf_aifs025` | 51 | 168 h |
| GFS (États-Unis) | `gfs025` | 31 | 168 h |
| ICON (Allemagne) | `icon_seamless_eps` | 40 | 168 h |
| GEM (Canada) | `gem_global` | 21 | 168 h |
| UKMO (Royaume-Uni) | `ukmo_global_ensemble_20km` | 18 | 168 h |

### Modèles déterministes (précision à court terme)

API `https://api.open-meteo.com/v1/forecast`. Testés le 22/11/2026 sur le point 1800 m, avec
7 jours demandés à partir de minuit (168 h au maximum). La portée dépend de l'heure du dernier
calcul du modèle et varie donc de quelques heures d'un jour à l'autre.

| Modèle | Code | Maille | Portée mesurée | Dans les fenêtres 48 h |
|---|---|---|---|---|
| AROME HD (prioritaire) | `meteofrance_arome_france_hd` | 1,5 km | 62 h | oui ★ |
| AROME | `meteofrance_arome_france` | 2,5 km | 59 h | oui |
| HARMONIE (Danemark) | `dmi_harmonie_arome_europe` | 2 km | 70 h | oui |
| HARMONIE (Pays-Bas) | `knmi_harmonie_arome_europe` | 5,5 km | 72 h | oui |
| ICON-EU | `icon_eu` | 7 km | 128 h | oui |
| ARPEGE | `meteofrance_arpege_europe` | 10 km | 110 h | oui |
| UKMO | `ukmo_global_deterministic_10km` | 10 km | 168 h | oui |
| Météo-France (mixte) | `meteofrance_seamless` | 1,5 à 25 km | 110 h | non |
| ECMWF | `ecmwf_ifs025` | 25 km | 168 h | non |
| ECMWF IA | `ecmwf_aifs025_single` | 25 km | 168 h | non |
| ICON | `icon_global` | 13 km | 168 h | non |
| GFS | `gfs_global` | 13 km | 168 h | non |
| GEM | `gem_global` | 15 km | 168 h | non |
| JMA (Japon) | `jma_gsm` | 55 km | 168 h | non |
| CMA (Chine) | `cma_grapes_global` | 15 km | 124 h | non |

Cas particuliers constatés le 22/11/2026 :

- `gfs_graphcast025` (GraphCast) et `kma_gdps` (KMA) répondent mais **sans aucune valeur**
  pour Superbagnères. Ils restent dans la liste au cas où les données reviennent ; en attendant,
  la page les affiche dans « Modèles indisponibles ».
- `italia_meteo_arpae_icon_2i` (ICON-2I) **ne couvre pas** Superbagnères
  (« No data is available for this location ») : il a été retiré de la page.

## Limites à connaître

- Open-Meteo gratuit autorise 10 000 appels par jour et par adresse internet. Chaque appui sur
  **Calculer** fait 23 appels (les 6 altitudes partent ensemble dans chaque appel) : pas de souci pour un usage normal depuis un téléphone.
  Si le quota est dépassé, les modèles concernés apparaissent dans « Modèles indisponibles ».
- C'est une aide à la décision : les mesures sur place (sonde, hygromètre, anémomètre) restent la référence.

Données météo : [Open-Meteo.com](https://open-meteo.com/), licence CC BY 4.0.
