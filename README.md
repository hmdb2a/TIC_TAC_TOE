# Morpion multijoueur en réseau (client / serveur, Raspberry Pi)

Jeu de morpion à deux joueurs en réseau, développé en Python avec une architecture client / serveur sur sockets TCP. Le projet a été déployé sur trois Raspberry Pi reliés par un réseau Wi-Fi ad hoc : un serveur qui héberge la partie et deux clients, un par joueur.

Projet du module Réseau de la Licence Informatique (Université Paris-Saclay), réalisé en équipe de trois.

## Fonctionnement

- **Serveur** (`Server.py`) : ouvre un socket TCP, accepte deux joueurs, leur attribue un rôle (X ou O) au hasard et gère chaque client dans un thread dédié. Il valide les coups, détecte la victoire ou le match nul, et diffuse l'état de la partie aux deux joueurs. Un troisième client reçoit le message `[SERVER FULL]`.
- **Client** (`Client.py`) : se connecte au serveur, affiche la grille et envoie les coups du joueur.

## Technologies

- Python 3 : `socket`, `threading`
- Raspberry Pi, point d'accès Wi-Fi créé sur le Raspberry Pi serveur

## Lancer le jeu

1. Renseigner la même adresse IP et le même port (`SERVER` et `PORT`) dans `Server.py` et `Client.py`. Par défaut : `localhost`, port `8888`.
2. Lancer le serveur :
   ```bash
   python3 Server.py
   ```
3. Dans deux autres terminaux, ou sur deux autres machines du réseau, lancer un client :
   ```bash
   python3 Client.py
   ```
4. Pour jouer, saisir le numéro de ligne puis le numéro de colonne, séparés par un espace (par exemple `0 2`).

## Difficulté technique principale

Les messages envoyés à la suite par le serveur pouvaient arriver fusionnés côté client, car TCP transmet un flux d'octets et non des messages séparés. Nous avons contourné le problème en espaçant les envois. Une amélioration possible serait de délimiter chaque message (préfixe de longueur ou caractère de fin).

## Contenu du dépôt

| Fichier | Contenu |
|---|---|
| `Server.py` | Serveur de jeu |
| `Client.py` | Client joueur |
| `docs/Rapport.pdf` | Rapport du projet |
| `docs/Slides.pdf` | Support de soutenance |

## Auteurs

Ahmed Baaroun, Dalia Sellami, Dyhia Medjouti
