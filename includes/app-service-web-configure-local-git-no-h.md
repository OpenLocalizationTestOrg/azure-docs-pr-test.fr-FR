Configurer Git déploiement toohello l’application web locale avec hello [source liée à un déploiement de webapp dans az-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) commande.

Service d’applications prend en charge plusieurs façons toodeploy tooa contenu application web, tels que FTP, Git local, GitHub, Visual Studio Team Services et Bitbucket. Pour ce démarrage rapide, vous effectuez le déploiement à l’aide de Git local. Cela signifie que vous déployez à l’aide d’un toopush de commande Git à partir d’un référentiel tooa local dans Azure. 

Bonjour suivant de commande, remplacez  *\<nom_application >* avec le nom de votre application web.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

sortie de Hello a hello suivant le format :

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

Hello `<username>` est hello [utilisateur du déploiement](#configure-a-deployment-user) que vous avez créé à l’étape précédente.

Copiez hello URI affichée ; vous allez l’utiliser dans l’étape suivante de hello.
