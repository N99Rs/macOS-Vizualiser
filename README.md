# macOS Big Sur — Simulation de bureau (HTML/CSS/JS)

Simulation interactive d'un bureau macOS Big Sur, entièrement autonome (un seul fichier HTML, sans dépendance externe, sans build).

**Fichier principal :** `macos_desktop.html`

---

## Aperçu

Ce projet reproduit l'interface visuelle et un sous-ensemble des interactions d'un bureau macOS : barre de menu, Dock avec magnétisme, fenêtres d'applications, Launchpad, Mission Control, Spotlight, Centre de notifications, Centre de contrôle, écran de veille et séquence d'extinction.

Il s'agit d'une **démo d'interface** à but visuel/pédagogique : aucune donnée n'est persistée, aucune app ne fonctionne réellement (pas de vraie navigation web, pas de vrais e-mails, etc.).

---

## Utilisation

Ouvrir simplement `macos_desktop.html` dans un navigateur récent (Chrome, Safari, Firefox, Edge). Aucune installation, aucun serveur requis.

---

## Fonctionnalités

### Barre de menu
- Horloge en temps réel (mise à jour toutes les 15s), format français.
- Menus déroulants fonctionnels (Finder, File, Edit, View, Go, Window, Help) qui s'ouvrent au clic et se survolent entre eux une fois un menu ouvert.
- Le nom de l'app affiché à gauche change dynamiquement selon la fenêtre active au premier plan.
- Icônes de droite : Spotlight, Centre de contrôle, Centre de notifications — tous cliquables.
- Menu Pomme avec "Mettre en veille", "Redémarrer…", "Éteindre…" (déclenchent de vraies séquences animées).

### Dock
- **Magnétisme progressif** : les icônes grossissent selon la distance réelle au curseur (calcul JS, pas juste un `:hover` CSS), avec effet de vague sur les icônes voisines — reproduit le comportement du vrai Dock macOS.
- Rebond (bounce) au clic sur une icône.
- Tooltip du nom de l'app au survol.
- Icônes dessinées en SVG (pas des emojis) pour un rendu plus fidèle.
- **Glisser une icône vers le bas** la retire du Dock (comportement réel macOS).
- Support tactile (mobile/tablette) sur le magnétisme.
- Taille responsive selon la largeur d'écran.

### Fenêtres & gestion multi-fenêtres
- Chaque app du Dock ouvre sa propre fenêtre (Finder, Safari, Mail, Messages, Calendrier, Photos, FaceTime, Contacts, Wallet, Notes, Musique, Podcasts, App Store, Préférences Système, etc.).
- Fenêtres déplaçables (glisser la barre de titre) et redimensionnables sur les **8 directions** (bords + coins).
- Gestion du focus : cliquer sur une fenêtre la ramène au premier plan et estompe visuellement les autres (titre grisé, ombre plus légère) — comme sur un vrai Mac.
- **Split View** : glisser une fenêtre vers le bord gauche ou droit de l'écran affiche un aperçu bleu, puis ancre la fenêtre sur la moitié de l'écran au relâchement.
- Boutons de la jauge (rouge/jaune/vert) : fermeture animée, réduction.

### Launchpad
- Vue plein écran avec flou du fond d'écran, grille d'icônes SVG, fermeture au clic en dehors ou touche Échap.

### Mission Control
- Affiche toutes les fenêtres ouvertes sous forme de vignettes ; cliquer sur une vignette la ramène au premier plan.

### Spotlight
- Recherche en direct dans une liste factice d'apps/fichiers.
- **Calculatrice intégrée** : taper une expression simple (`2+2`, `10*4`) affiche directement le résultat.

### Centre de contrôle & Centre de notifications
- Panneaux avec Wi-Fi, Bluetooth, luminosité, volume (Centre de contrôle).
- Notifications factices (Mail, Messages, Rappels, mise à jour système), accessible via l'icône dédiée ou le bord droit de l'écran.

### Bureau
- Icônes Time Machine, Storage, Movies — sélectionnables au clic, ouverture du Finder au double-clic.
- **Clic droit** sur le bureau ou sur une icône ouvre un menu contextuel (Nouveau dossier, Obtenir des informations, Mettre à la corbeille…).
- Widgets Météo et Calendrier avec date réelle.

### Système
- **Raccourcis clavier** : `⌘Tab` (ou `Ctrl+Tab`) ouvre le sélecteur d'applications façon macOS ; `⌘W` et `⌘Q` ferment la fenêtre active.
- Écran de veille après ~45 secondes d'inactivité (horloge flottante), se ferme au clic/touche.
- Sons de clic discrets synthétisés en JavaScript (Web Audio API) — aucun fichier audio externe.
- Séquence d'extinction/redémarrage animée depuis le menu Pomme.

---

## Structure technique

Tout est contenu dans un seul fichier `macos_desktop.html` :
- **CSS** dans `<style>` : mise en page, effets de flou (`backdrop-filter`), animations, thème visuel.
- **SVG** inline pour le fond d'écran (dégradés multi-stops façon vagues Big Sur) et les icônes du Dock/Launchpad.
- **JavaScript vanilla** (aucune librairie) : gestion d'état des fenêtres, magnétisme du Dock, menus, panneaux, raccourcis clavier.

Aucune dépendance, aucun build, aucun serveur : le fichier peut être ouvert directement ou déployé tel quel sur n'importe quel hébergement statique.

---

## Limites connues

- Simulation visuelle uniquement : aucune app ne fonctionne réellement (pas de navigation web, pas d'envoi d'e-mails, etc.).
- Aucune persistance des données (positions de fenêtres, icônes supprimées du Dock, etc.) — tout est réinitialisé au rechargement de la page.
- Testé principalement sur navigateurs desktop ; le support tactile couvre le Dock et l'écran de veille mais pas l'ensemble des interactions (drag de fenêtre, redimensionnement).
- `backdrop-filter` (effets de flou) peut ne pas être supporté sur d'anciens navigateurs.

## Pistes d'amélioration possibles

- Vraies icônes skeuomorphiques avec reflets/biseaux plus poussés.
- Persistance de l'état (position des fenêtres, icônes du Dock) via `localStorage` en dehors du contexte artifact.
- Glisser-déposer de fichiers entre le Finder et le Dock.
- Curseurs contextuels (texte, lien, redimensionnement) sur davantage d'éléments.
- Séparation du CSS/JS en fichiers distincts si le projet doit être réutilisé au-delà d'un fichier unique.
