# Configuration Cloudinary pour Heroku

## Problème résolu

L'erreur `KeyError: Missing configuration for the cloudinary Active Storage service` a été corrigée en :

1. ✅ Ajout de la section `production` dans `config/storage.yml`
2. ✅ Ajout de la gem `cloudinary` dans le `Gemfile`

## Configuration requise sur Heroku

### Étape 1 : Obtenir vos identifiants Cloudinary

1. Connectez-vous à votre compte Cloudinary : https://cloudinary.com/users/login
2. Allez dans le Dashboard
3. Copiez votre **Cloudinary URL** qui ressemble à :
   ```
   cloudinary://API_KEY:API_SECRET@CLOUD_NAME
   ```

### Étape 2 : Configurer la variable d'environnement sur Heroku

**Commande à exécuter dans votre terminal :**

```bash
heroku config:set CLOUDINARY_URL=cloudinary://API_KEY:API_SECRET@CLOUD_NAME
```

**Exemple concret :**
```bash
heroku config:set CLOUDINARY_URL=cloudinary://123456789012345:abcdefghijklmnopqrstuvwxyz@your-cloud-name
```

### Étape 3 : Vérifier la configuration

```bash
# Vérifier que la variable est bien configurée
heroku config:get CLOUDINARY_URL

# OU voir toutes les variables d'environnement
heroku config
```

### Étape 4 : Redémarrer l'application

```bash
heroku restart
```

## Séquence complète de déploiement

```bash
# 1. Installer la gem localement
bundle install

# 2. Commiter les changements
git add Gemfile Gemfile.lock config/storage.yml
git commit -m "Add Cloudinary configuration for production storage"

# 3. Configurer Cloudinary sur Heroku (remplacez par votre URL)
heroku config:set CLOUDINARY_URL=cloudinary://VOTRE_API_KEY:VOTRE_API_SECRET@VOTRE_CLOUD_NAME

# 4. Déployer
git push heroku master

# 5. Redémarrer
heroku restart

# 6. Vérifier les logs
heroku logs --tail
```

## Alternative : Utiliser l'addon Heroku Cloudinary (recommandé)

Si vous préférez, vous pouvez utiliser l'addon officiel Heroku :

```bash
# Installer l'addon Cloudinary (gratuit jusqu'à 25GB)
heroku addons:create cloudinary:starter

# L'addon configure automatiquement CLOUDINARY_URL
```

## Vérification

Après configuration, votre application devrait démarrer sans erreur. Vérifiez avec :

```bash
heroku logs --tail
```

Vous ne devriez plus voir l'erreur `KeyError: Missing configuration for the cloudinary Active Storage service`.
