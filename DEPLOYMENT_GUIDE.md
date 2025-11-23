# Guide de Déploiement Heroku - Rails Watch List

## Étape 1 : Vérification locale en production

### 1.1 Précompiler les assets
```bash
RAILS_ENV=production bundle exec rails assets:precompile
```

### 1.2 Tester le démarrage en production locale (optionnel)
```bash
RAILS_ENV=production bundle exec rails server
```
Puis visitez `http://localhost:3000` pour vérifier que tout fonctionne.

**Note :** Pour arrêter le serveur, utilisez `Ctrl+C`.

## Étape 2 : Préparation Git

### 2.1 Vérifier l'état du dépôt
```bash
git status
```

### 2.2 Ajouter tous les fichiers modifiés
```bash
git add .
```

### 2.3 Commiter les changements
```bash
git commit -m "Fix: Add missing _flashes partial, fix application.scss, and correct link_to syntax"
```

## Étape 3 : Déploiement sur Heroku

### 3.1 Vérifier que le remote Heroku est configuré
```bash
git remote -v
```

Si Heroku n'est pas configuré, ajoutez-le :
```bash
heroku git:remote -a rails-watch-list-18f600c5b229
```

### 3.2 Pousser vers Heroku
```bash
git push heroku master
```

**OU** si vous utilisez la branche `main` :
```bash
git push heroku main
```

## Étape 4 : Vérification post-déploiement

### 4.1 Vérifier les logs Heroku
```bash
heroku logs --tail
```

### 4.2 Vérifier les logs en temps réel (recommandé)
```bash
heroku logs --tail --app rails-watch-list-18f600c5b229
```

### 4.3 Ouvrir l'application dans le navigateur
```bash
heroku open
```

## Étape 5 : Commandes de diagnostic (si erreurs)

### 5.1 Vérifier la configuration Heroku
```bash
heroku config
```

### 5.2 Vérifier les dynos
```bash
heroku ps
```

### 5.3 Exécuter une console Rails sur Heroku
```bash
heroku run rails console
```

### 5.4 Vérifier les assets précompilés sur Heroku
```bash
heroku run rails assets:precompile
```

## Commandes complètes (copier-coller)

```bash
# 1. Précompiler les assets
RAILS_ENV=production bundle exec rails assets:precompile

# 2. Vérifier l'état Git
git status

# 3. Ajouter et commiter (si nécessaire)
git add .
git commit -m "Fix: Add missing _flashes partial, fix application.scss, and correct link_to syntax"

# 4. Pousser vers Heroku
git push heroku master

# 5. Vérifier les logs
heroku logs --tail
```

## Notes importantes

- **Assets en production :** Heroku précompile automatiquement les assets lors du déploiement, mais vous pouvez le faire manuellement si nécessaire.
- **Master Key :** Assurez-vous que `config/master.key` est présent et que Heroku a la variable d'environnement `RAILS_MASTER_KEY` configurée.
- **Base de données :** Si vous avez des migrations en attente, exécutez `heroku run rails db:migrate` après le déploiement.
