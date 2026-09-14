# 🧙‍♂️ Le Royaume de Maxremi

> API de jeu de rôle façon Donjons & Dragons — création de personnages, gestion de monstres/objets/quêtes et système de rôles Joueur / Maître du Jeu, connectée à l'API SRD de D&D 5e.

![Node.js](https://img.shields.io/badge/Node.js-backend-339933?logo=nodedotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?logo=typescript)
![Express](https://img.shields.io/badge/Express-API-000000?logo=express)
![Prisma](https://img.shields.io/badge/Prisma-ORM-2D3748?logo=prisma)
![Neon](https://img.shields.io/badge/Neon-PostgreSQL-00E599?logo=postgresql&logoColor=white)
![React](https://img.shields.io/badge/React-frontend-61DAFB?logo=react&logoColor=black)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-styling-06B6D4?logo=tailwindcss&logoColor=white)
![JWT](https://img.shields.io/badge/Auth-JWT-black?logo=jsonwebtokens)
<br>

## 📸 Aperçu

<table>
<tr>
<td width="50%">

**Page d'accueil**
![Accueil](./documentation/images/image.png)

</td>
<td width="50%">

**Affichage public des monstres**
![Monstres](./documentation/images/image-11.png)

</td>
</tr>
<tr>
<td width="50%">

**Création de personnage**
![Création de personnage](./documentation/images/image-5.png)

</td>
<td width="50%">

**Panneau d'administration — quêtes**
![Admin quêtes](./documentation/images/image-25.png)

</td>
</tr>
</table>

<br>

## 🖼️ Fonctionnalités en images

### 🐉 Bestiaire filtrable
Recherche et filtres par type (Dragon, Orc...), taille et alignement.

<p>
<img src="./documentation/images/image-10.png" width="32%" />
<img src="./documentation/images/image-12.png" width="32%" />
<img src="./documentation/images/image-14.png" width="32%" />
</p>

### 🛡️ Objets et boutique
Affichage public avec filtres (type d'arme, rareté, tri par prix).

<p>
<img src="./documentation/images/image-16.png" width="32%" />
<img src="./documentation/images/image-17.png" width="32%" />
<img src="./documentation/images/image-18.png" width="32%" />
</p>

### 🔐 Authentification & administration
Inscription, connexion et gestion des utilisateurs par le MDJ.

<p>
<img src="./documentation/images/image-1.png" width="32%" />
<img src="./documentation/images/image-19.png" width="32%" />
<img src="./documentation/images/image-21.png" width="32%" />
</p>

### ⚔️ Recherche de monstres via l'API D&D 5e
Le MDJ peut chercher un monstre directement dans le SRD officiel et l'ajouter au bestiaire.

<p>
<img src="./documentation/images/image-32.png" width="49%" />
<img src="./documentation/images/image-34.png" width="49%" />
</p>

<br>

## 🛠️ Stack technique

| Couche | Technologie |
|---|---|
| Backend | Node.js, Express, TypeScript |
| Base de données | PostgreSQL (Neon) via Prisma ORM |
| Authentification | JWT + bcrypt |
| Requêtes externes | Axios (API SRD D&D 5e) |
| Frontend | React, TailwindCSS |
| API tierce | [dnd5eapi.co](https://www.dnd5eapi.co/) |

<br>

## 🚀 Installation et lancement

**Prérequis**
- Node.js
- Une instance de base de données Neon (gratuit sur [neon.com](https://neon.com))

### Backend

```bash
git clone https://github.com/clementlaflamme/royaume-maxremi.git
cd royaume-maxremi/backend
npm install

# Créer un fichier .env à la racine du backend (voir .env.example)
# et y ajouter le lien de connexion Neon

npx prisma generate
npx prisma migrate dev --name init

npm run dev
```

### Frontend

```bash
# Dans un nouveau terminal
cd royaume-maxremi/frontend
npm install
npm run dev
```

L'interface est ensuite disponible sur `http://localhost:5173`.

<br>

## 🛣️ Routes de l'API

<details>
<summary>Voir la liste complète des routes (cliquer pour développer)</summary>

> L'adresse de base pour toutes les requêtes est `http://localhost:3000`. Certaines routes nécessitent un token JWT dans l'en-tête `Authorization`.

### Authentification

| Méthode | Route | Description | Accès |
|---|---|---|---|
| `POST` | `/auth/register` | Création de compte (Utilisateur ou Admin) | Public |
| `POST` | `/auth/login` | Connexion et obtention du token JWT | Public |
| `GET` | `/auth/me` | Infos de l'utilisateur connecté | Authentifié |

### Monstres

| Méthode | Route | Description | Accès |
|---|---|---|---|
| `GET` | `/monstre/` | Liste tous les monstres | Public |
| `GET` | `/monstre/:nom` | Détail d'un monstre par son nom | Public |
| `POST` | `/monstre/ajouter/:nom` | Ajoute un nouveau monstre | MDJ |
| `PATCH` | `/monstre/:id` | Modifie un monstre existant | MDJ |
| `DELETE` | `/monstre/supprimer/:id` | Supprime un monstre | MDJ |
| `GET` | `/recherche/:nom` | Recherche un monstre dans l'API D&D | MDJ |

### Objets

| Méthode | Route | Description | Accès |
|---|---|---|---|
| `GET` | `/objet/` | Liste tous les objets | Public |
| `GET` | `/objet/:nom` | Détail d'un objet par son nom | Public |
| `POST` | `/objet/creer` | Crée un nouvel objet | MDJ |
| `PATCH` | `/objet/:id` | Modifie un objet existant | MDJ |
| `DELETE` | `/objet/supprimer/:id` | Supprime un objet | MDJ |

### Quêtes

| Méthode | Route | Description | Accès |
|---|---|---|---|
| `GET` | `/quete` | Liste les quêtes (filtre `?difficulte=X`) | Public |
| `GET` | `/quete/:nom` | Détail d'une quête par son nom | Public |
| `POST` | `/quete/creer` | Crée une nouvelle quête | MDJ |
| `PATCH` | `/quete/:id` | Modifie une quête existante | MDJ |
| `DELETE` | `/quete/supprimer/:id` | Supprime une quête | MDJ |

### Utilisateurs & personnages

| Méthode | Route | Description | Accès |
|---|---|---|---|
| `POST` | `/utilisateur/creer` | Crée un compte utilisateur | MDJ |
| `GET` | `/utilisateur/recuperer/:id` | Récupère les infos utilisateur | MDJ |
| `PATCH` | `/utilisateur/modifier/:id` | Modifie un utilisateur | MDJ |
| `DELETE` | `/utilisateur/supprimer/:id` | Supprime un utilisateur | MDJ |
| `POST` | `/personnage/creer` | Crée un personnage | Joueur |
| `GET` | `/personnage/recuperer/:id` | Affiche le personnage | Joueur |
| `PATCH` | `/personnage/modifier/:id` | Modifie un personnage | MDJ |
| `DELETE` | `/personnage/supprimer/:id` | Supprime un personnage | Joueur |

### Journal de quêtes & inventaire

| Méthode | Route | Description | Accès |
|---|---|---|---|
| `POST` | `/persoquete/ajouter` | Ajoute une quête au journal du perso | Joueur |
| `GET` | `/persoquete/:idPerso` | Affiche le journal de quêtes | Joueur |
| `PATCH` | `/persoquete/journal/reussir/:id` | Valide une quête | Joueur |
| `PATCH` | `/persoquete/journal/echouer/:id` | Échoue une quête | Joueur |
| `DELETE` | `/persoquete/journal/abandonner/:id` | Abandonne une quête | Joueur |
| `GET` | `/inventaire/:idPerso` | Récupère l'inventaire | Joueur |
| `POST` | `/inventaire/ajouter` | Ajoute un objet à l'inventaire | Joueur |
| `DELETE` | `/inventaire/retirer` | Retire un objet de l'inventaire | Joueur |

**Tests** : le fichier `test.rest` à la racine du backend permet de tester chaque route individuellement (nécessite de renseigner des UUID valides pour `@uuidPerso`, `@uuidQuete`, `@uuidPersoQuete`, `@uuidUser`).

</details>

<br>

## 👤 Auteurs

- Clément Laflamme
- Francis Boisvert
- Mathieu Gosselin
- Pascale Mercier *(TP1)*
