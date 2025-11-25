README · Portfolio Joueur (HTML/CSS/JS) — Palette Bleue

Portfolio statique haut de gamme pour joueurs d’académie (U16–U19) orienté visibilité scouting / mercato.
Stack ultra-simple : HTML (one-pager), CSS (fichier séparé), JS vanilla (fichier séparé), Tailwind via CDN pour l’utilitaire, Chart.js pour le radar.
Aucun build, aucun backend requis. Le formulaire utilise mailto: et ouvre WhatsApp avec un message prérempli.

⸻

1. Prérequis
   • Git (ou télécharger le dossier en .zip)
   • Un serveur statique local (au choix) :
   • VS Code Live Server (recommandé)
   • python3 -m http.server 8080 puis ouvrir http://localhost:8080
   • npx serve -l 8080

Astuce : sur macOS/Linux, open http://localhost:8080 (ou xdg-open sous Linux).

⸻

2. Cloner & lancer (développement local)

# 1) Cloner le repo

git clone <VOTRE_REPO_URL> football-portfolio-blue
cd football-portfolio-blue

# 2) Lancer un serveur local (au choix)

python3 -m http.server 8080

# ou

npx serve -l 8080

# 3) Ouvrir le site

# http://localhost:8080

# ou juste double clic sur index.html

⸻

3. Structure du projet

.
├─ index.html # One-pager du joueur
├─ assets/
│ ├─ css/
│ │ └─ style.css # Palette bleue, boutons, glass, pitch grid, etc.
│ ├─ js/
│ │ └─ app.js # Thème clair/sombre, formulaires, filtres, radar
│ ├─ images/ # Visuels (placeholders à remplacer)
│ │ ├─ portrait.svg
│ │ ├─ action1.svg … action6.svg
│ │ └─ ball.svg
│ ├─ CV_Joueur.pdf # Placeholder (remplacer par le vrai CV)
│ ├─ Press_Kit.pdf # Placeholder (press kit)
│ └─ Dossier_Mercato_Pack_FR.xlsx# Placeholder (pack mercato)
└─ README.md

⸻

4. Où modifier les données joueur

4.1 Constantes & liens (en haut de assets/js/app.js)

const PLAYER_NAME = 'Prénom NOM';
const ACADEMY_NAME = 'Académie X U19';

const RECEIVING_EMAIL = 'contact@joueur.com'; // email destinataire (mailto)
const WHATSAPP_NUMBER_INTL = '+32465807642'; // format E.164 (ex: +33601020304)

const HIGHLIGHTS_URL = 'https://youtu.be/xxxx';
const FULL_MATCH_1 = 'https://exemple.com/fullmatch1';
const FULL_MATCH_2 = 'https://exemple.com/fullmatch2';

4.2 Métadonnées / SEO (dans <head> de index.html)
• <title>, meta name="description", meta property="og:\*", meta name="theme-color"
• Facultatif : remplacer l’OG image par une bannière hébergée en HTTPS.

4.3 Texte & sections (dans index.html)
• Bio, parcours, compétences, téléchargements, liens officiels
• Statistiques : remplir le tableau (ajouter/supprimer des <tr>)
• Logs match : tableau par match (date, compétition, poste, min, G/PD, lien vidéo)

4.4 Images (dans assets/images/)
• Remplacer les SVG par des photos réelles (même nom de fichier ou adapter index.html)
• Recommandations :
• Portrait 4:5 (p. ex. 900×1125 px)
• Galerie 1:1 (≥800×800 px)
• Poids cible : ≤ 250 Ko / image (TinyPNG, Squoosh, etc.)

⸻

5. Thème clair/sombre & palette bleue

Le thème est persistant via localStorage (bouton 🌙/☀️ dans l’en-tête).

Ajuster la palette dans assets/css/style.css :

:root{
--bg:#ffffff; --text:#0b1220; --muted:#5b6b83;
--card:rgba(255,255,255,.88); --border:rgba(11,18,32,.10);
--line:rgba(96,165,250,.22);
--accent:#3b82f6; /_ blue-500 _/
--accent-2:#06b6d4; /_ cyan-500 _/
}
.dark:root{
--bg:#0b1220; --text:#e5eaf1; --muted:#a5b4c7;
--card:rgba(15,23,42,.72); --border:rgba(255,255,255,.10);
--line:rgba(96,165,250,.15);
--accent:#60a5fa; /_ blue-400 _/
--accent-2:#22d3ee; /_ cyan-400 _/
}

⸻

6. Créer un nouveau profil joueur (sans backend)

Option A — Monoprofil (un seul joueur)

Modifier index.html, assets/js/app.js, les images et documents. Déployer.

Option B — Multiprofils (duplication statique recommandée)

Créer un dossier par joueur en dupliquant le projet :

mkdir -p profiles
cp -R ./ profiles/prenom-nom/

# (ou rsync si vous préférez)

# rsync -a --exclude ".git" ./ profiles/prenom-nom/

Dans profiles/prenom-nom/ :
• Mettre à jour les constantes (app.js)
• Adapter SEO (index.html)
• Remplacer images / PDF / Excel
• Déployer chaque profil sur une URL distincte (ex. /profiles/prenom-nom/)

Avantage : chaque profil est isolé (pas de collisions JS).
Inconvénient : duplication des assets (acceptable pour vitrines statiques).

Option C — (Facultatif) Mode Data-Driven via JSON

Si vous voulez éviter la duplication : 1. Créez assets/data/<slug>.json par joueur (nom, bio, stats, logs, liens). 2. Adaptez app.js pour fetch le JSON selon ?player=<slug> et hydrater le DOM. 3. Gardez en tête qu’un serveur statique autorisant fetch local sera nécessaire.

(Non implémenté par défaut pour rester “no build / no backend”.)

⸻

7. Formulaire email + WhatsApp
   • Email : ouverture du client via mailto: (destinataire = RECEIVING_EMAIL)
   • WhatsApp : ouverture de wa.me/<numero> avec le message prérempli (cocher “Envoyer aussi sur WhatsApp”)
   • Le bouton Prévisualiser ouvre un modal avec le contenu généré.

Pour un envoi e-mail 100 % fiable sans mailto, intégrer un service (Netlify Forms / Formspree / serverless) — non inclus ici.

⸻

8. Qualité & conformité (données réelles)
   • Mineur (16 ans) : obtenir autorisation parentale écrite (images/vidéos/données).
   • Données sensibles : ne publier que le nécessaire (éviter adresse, école, etc.).
   • Droits d’image : vérifier l’autorisation pour les médias (club/ligue/photographe).
   • SEO : titre, description, OG image — cohérents et à jour.

Checklist mercato
• Portrait pro (4:5) et galerie actions (1:1), compressées
• Highlights YouTube + 1–2 matchs complets (liens privés si besoin)
• Stats saison (M/Min/Buts/PD/xG/xA) réelles et datées
• Logs match (adversaire, compet, poste, min, G/PD, lien)
• CV sportif (PDF), Press Kit (PDF), Dossier mercato (Excel/CSV)
• Contacts valides (email, WhatsApp au format E.164)

⸻

9. Tests rapides (QA)
   • Responsive : mobile (360 px), tablette, desktop
   • Thème : bascule clair/sombre + persistance
   • Formulaire : champs requis, mailto, WhatsApp, prévisualisation
   • Liens : highlights / full matches / socials / téléchargements
   • Performance : poids des images, lazy-loading iframe YouTube

⸻

10. Déploiement
    • GitHub Pages : servir la racine (ou profiles/prenom-nom/)
    • Netlify / Vercel : drag-and-drop du dossier, aucun build
    • FTP / Nginx / Apache : copier les fichiers vers l’hébergement

Si vous utilisez des profils multiples, déployez chaque dossier dans un sous-chemin dédié.

⸻

11. Contribution
    • Branches : feat/xxx, fix/xxx
    • Commits : style concis (feat(stats): add per90 calc)
    • PR : test rapide mobile/desktop, vérifier liens et formulaires

⸻

12. Roadmap (suggestions)
    • Mode JSON multi-joueurs + routing ?player=slug
    • Backend forms (Netlify Forms / serverless)
    • Export PDF de la page (styles print CSS)
    • Accessibilité renforcée (labels, focus, contrastes AAA)

⸻

13. Licence & crédits
    • Code : vous pouvez l’adapter au besoin pour les portfolios de joueurs.
    • Remplacez tous les médias de démo par images autorisées et documents réels.
    • Respectez les droits d’auteur et le RGPD (mineurs).

Bon build ! ⚽
