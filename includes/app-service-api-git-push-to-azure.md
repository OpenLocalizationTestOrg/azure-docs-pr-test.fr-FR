Utilisez les URL de déploiement à distance de hello CLI d’Azure tooget hello pour votre application API. Bonjour suivant de commande, remplacez  *\<nom_application >* avec le nom de votre application web.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

Configurez votre local Git déploiement toobe toopush en mesure de toohello à distance.

```bash
git remote add azure <URI from previous step>
```

Push toohello Azure toodeploy à distance de votre application. Vous êtes invité au mot de passe hello que vous avez créé précédemment lors de la création d’utilisateur du déploiement hello. Assurez-vous que vous entrez hello mot de passe créé dans démarrage rapide de hello et pas hello vous utilisez toolog dans toohello portail Azure.

```bash
git push azure master
```
