# Roadmap SPARTA — Fin 2026

Feuille de route de septembre à décembre 2026, parcourue comme une carte de
campagne. Le scroll ne fait pas défiler la page : il fait **avancer la caméra**
le long d'une route tracée sur un relief en courbes de niveau.

## DA « Table de sable »

| | |
|---|---|
| Palette | obsidienne `#07080A`, or SPARTA `#D4AF37`, puis une descente saisonnière : or vif (sept) → bronze (oct) → acier (nov) → givre (déc). La route reste or du début à la fin. |
| Typographie | Cinzel (sceau, mois gravés au sol) · Barlow Condensed (libellés de carte) · IBM Plex Mono (dates) |
| Motion | CatmullRom + caméra en plongée 3/4, la portion parcourue de la route s'allume derrière soi, le plan à venir reste en pointillés |
| Mois | franchis physiquement : deux stèles, une frontière pointillée au sol, bascule d'atmosphère et de météo |
| Final | la caméra s'élève et découvre toute la campagne, horizon 2027 |

## Contenu

12 rendez-vous, repris tels quels. Septembre remis dans l'ordre chronologique
(24 avant 25-28).

## Regarder le site

Pas de serveur permanent : on le lance quand on en a besoin, depuis le Terminal,
qui a l'accès macOS au Bureau.

```bash
cd "/Users/hugosanchezflores/Desktop/Claude Code/Decks & Présentations/Roadmap SPARTA/site" && python3 -m http.server 8340
```

Puis http://localhost:8340. Ctrl+C pour arrêter.

Un service launchd avait été mis en place puis retiré : à retenir si l'envie
revient, un service de fond n'a **pas** le droit macOS de lire le Bureau et ne
peut pas demander l'autorisation. Il faudrait lui faire servir une copie placée
hors des dossiers protégés.

## Paramètres## Paramètres## Paramètres d'URL (contrôle qualité)

| Paramètre | Effet |
|---|---|
| `?flat=0.35` | rendu figé à 35 % du parcours, sans Lenis, pour les captures |
| `?reduced` | force le mode mouvement réduit |
| `?bench` | mesure la cadence pendant 12 s et publie le résultat dans le titre |
| `?audit` | parcourt toute la route et signale le moindre texte coupé ou hors cadre |

`window.__roadmap.goto(u)` déplace le parcours depuis la console, et
`window.__roadmap.balayage()` lance le contrôle des textes sans recharger la page.
Le balayage est synchrone : il fonctionne même quand le panneau d'aperçu dort
et bride le rAF.

Contrôlé sans aucun texte coupé sur huit largeurs, de 320 à 1920 px.

## Mesures

60,0 fps en Chrome headless (`--use-angle=metal`) : bureau 1440x900 @2x
(148 k triangles, 15 appels de rendu) et téléphone 390x844 @3x (54 k triangles,
profil allégé automatique, netteté 1,9).

## En ligne

Publié sur GitHub Pages : **https://hsanchezhub.github.io/roadmap-sparta/**
Dépôt public : https://github.com/hsanchezhub/roadmap-sparta

Le déploiement est automatique : tout envoi sur `main` déclenche le workflow
`.github/workflows/pages.yml`, qui publie le contenu de `site/`. Rien d'autre à
faire qu'un `git push`.

```bash
git add -A && git commit -m "..." && git push
```

Deux points à savoir si ça doit être refait ailleurs :

- Pages doit être activé **une fois à la main** dans Settings, Pages, Source :
  GitHub Actions. Le jeton automatique des Actions n'a pas le droit de créer le
  service lui-même, le workflow échoue tant que ce n'est pas fait.
- Le dépôt est **public**, donc la roadmap l'est aussi pour qui connaît
  l'adresse. Le `meta robots noindex` évite le référencement, sans rendre la page
  privée pour autant. Pages depuis un dépôt privé demanderait GitHub Pro.

Tous les chemins du site sont relatifs, il fonctionne donc aussi bien à la racine
d'un domaine que dans un sous-dossier comme ici.

## Livraison

Tout est embarqué : three.js, GSAP, ScrollTrigger, Lenis et les 24 woff2 sont
dans `site/vendor/`. Aucune requête externe, le site tient sans réseau.
