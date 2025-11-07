# Poomsae V10 – Firebase Scoring System

## 🎯 Objectif
Cette application web permet de gérer un système de notation pour les compétitions de Poomsae (Taekwondo).  
Elle fonctionne en ligne via **GitHub Pages** et utilise **Firebase Firestore** pour stocker les notes en temps réel.

---

## 🚀 Fonctionnalités
- **Juges (J1–J5)** : connexion avec un code, saisie des notes (ACC + PRES pour Poomsae 1 et 2).
- **Admin** : 
  - gestion des athlètes,
  - visualisation des moyennes P1, P2 et finales,
  - exportation des résultats au format CSV.
- **Affichage public** : classement en direct des athlètes, basé sur les moyennes des juges.
- **Firebase Firestore** : stockage et synchronisation des scores en temps réel.

---

## 🔑 Configuration Firebase
Avant utilisation, tu dois :
1. Créer un projet Firebase et activer **Firestore Database**.
2. Récupérer ta configuration (clé API, projectId, etc.).
3. Remplacer la section `const firebaseConfig = { ... }` dans `index.html` par tes propres valeurs.

---

## 🌐 Hébergement
L’application est conçue pour être hébergée gratuitement via **GitHub Pages** :
1. Crée un dépôt GitHub (ex. `poomsae-v10`).
2. Ajoute les fichiers (`index.html`, `README.md`).
3. Active GitHub Pages dans les paramètres du dépôt.
4. Accède à ton application via l’URL fournie par GitHub.

---

## 📝 Exemple de flux d’utilisation
1. **Admin** ajoute les athlètes (ex. A1, A2, A3).  
2. Chaque **juge** se connecte (J1…J5) et saisit ses notes.  
3. L’**admin** voit les moyennes calculées automatiquement.  
4. L’**affichage public** montre le classement en temps réel.  
5. L’**admin** peut exporter les résultats en CSV.

---

## ⚠️ Sécurité Firestore
Par défaut, Firestore est en mode test.  
👉 Il est recommandé de configurer des règles de sécurité pour limiter l’écriture aux seuls juges (J1–J5).  
Exemple de règle minimale :
```js
match /scores/{docId} {
  allow read: if true;
  allow write: if request.resource.data.judge in ["J1","J2","J3","J4","J5"];
}
