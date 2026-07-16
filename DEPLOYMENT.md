# Mise en ligne de Pop’s Car

La maquette est prête à être déployée comme application Node.js. Le serveur sert les pages HTML/CSS/JS, les images locales et l’endpoint Popsy.

## Option recommandée : hébergeur Node

Déployez le contenu du dossier `outputs` comme service web Node avec les paramètres suivants :

- Installation : `npm install --omit=dev`
- Démarrage : `npm start`
- Port : utiliser la variable `PORT` fournie par l’hébergeur
- Health check : `/health`

Variables à ajouter dans les secrets de l’hébergeur :

```text
OPENAI_API_KEY=...
OPENAI_MODEL=gpt-5.5
```

Le domaine devra pointer vers l’hébergeur et l’HTTPS doit être activé avant d’ouvrir le site au public.

## Option Docker

Depuis le dossier `outputs` :

```bash
docker build -t popscar .
docker run --rm -p 8787:8787 \
  -e OPENAI_API_KEY="votre_cle" \
  -e OPENAI_MODEL="gpt-5.5" \
  popscar
```

Le site sera disponible sur `http://localhost:8787` et la vérification serveur sur `http://localhost:8787/health`.

## Important avant une vraie ouverture des réservations

Le paiement, les pièces d’identité et le permis restent volontairement en démonstration dans cette maquette. Pour la production, il faudra connecter :

1. une base de données pour les disponibilités et réservations ;
2. un prestataire de paiement certifié, sans faire transiter les numéros de carte par ce serveur ;
3. un stockage privé et chiffré pour les justificatifs ;
4. un service d’envoi d’emails pour les confirmations et notifications.

La clé OpenAI ne doit jamais être placée dans `script.js`, dans un fichier HTML ou dans le dépôt public.
