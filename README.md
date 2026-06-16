# ✅ Todo App — Vue.js

Une application de gestion de tâches réalisée pour apprendre les bases de **Vue 3** avec la Composition API.

## 🚀 Stack

- [Vue 3](https://vuejs.org/) — Composition API avec `<script setup>`
- [Vite](https://vitejs.dev/) — Bundler
- TypeScript

## ✨ Fonctionnalités

- Ajouter une tâche (via bouton ou touche Entrée)
- Supprimer une tâche
- Marquer une tâche comme terminée
- Compteur dynamique des tâches restantes

## 🧠 Concepts Vue.js appris

| Concept | Usage |
|---|---|
| `ref()` | État réactif (liste de tâches, input) |
| `computed()` | Compteur dynamique basé sur `tasks.length` |
| `v-for` | Affichage de la liste |
| `v-model` | Liaison de l'input texte |
| `:class` | Style conditionnel selon `task.done` |
| `@click` / `@keyup.enter` | Gestion des événements |
| `@click.stop` | Arrêt de la propagation d'événement |

## 📦 Installation

```bash
# Cloner le dépôt
git clone https://github.com/ton-pseudo/todo-vue.git
cd todo-vue

# Installer les dépendances
npm install

# Lancer le serveur de développement
npm run dev
```

## 🗺️ Améliorations prévues

- [ ] Filtres Toutes / Actives / Terminées
- [ ] Modification d'une tâche existante
- [ ] Persistance avec `localStorage`
- [ ] Découpage en composants (`TodoItem.vue`, `TodoFilter.vue`)
- [ ] Connexion à une API Symfony

## 📚 Ressources

- [Documentation Vue.js](https://vuejs.org/guide/introduction.html)
- [Documentation Vite](https://vitejs.dev/guide/)
