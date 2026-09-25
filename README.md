# PDF Store Pro

Version full-stack avec :
- comptes clients (inscription/connexion)
- sessions
- tableau de bord client
- tableau de bord vendeur
- ajout/suppression de PDF
- base SQLite
- paiements Stripe Checkout
- webhook Stripe pour confirmer le paiement
- liens de téléchargement non publics
- téléchargement uniquement après paiement confirmé

## Installation

1. Installe Node.js 20+.
2. Dans ce dossier :
   npm install
3. Copie `.env.example` vers `.env`.
4. Configure `SESSION_SECRET`, `ADMIN_EMAIL`, `ADMIN_PASSWORD`, `BASE_URL`.
5. Ajoute tes clés Stripe dans `STRIPE_SECRET_KEY` et `STRIPE_WEBHOOK_SECRET`.
6. Lance :
   npm start
7. Ouvre http://localhost:3000

## PDF privés

Les PDF vendus doivent rester dans `private-pdfs/`. Ne mets jamais les PDF payants dans `public/`.

Le vendeur ajoute les PDF depuis `/admin.html`. Les fichiers sont stockés hors du dossier public et sont servis uniquement via `/api/download/:token` après paiement confirmé.

## Important pour la production

- Utiliser HTTPS.
- Remplacer la session MemoryStore par Redis ou une base adaptée.
- Configurer le webhook Stripe avec une URL HTTPS.
- Utiliser un vrai secret de session aléatoire.
- Mettre des sauvegardes de la base.
- Ajouter rate limiting, validation stricte et protection CSRF selon l'architecture retenue.
- Vérifier que le moyen de paiement choisi est disponible pour le pays et le compte marchand du vendeur.
- Pour le Congo-Brazzaville, si Stripe n'est pas disponible pour ton compte, remplacer le module de paiement par un prestataire réellement disponible localement (Mobile Money, agrégateur, etc.) et faire confirmer le paiement côté serveur avant de délivrer le PDF.
