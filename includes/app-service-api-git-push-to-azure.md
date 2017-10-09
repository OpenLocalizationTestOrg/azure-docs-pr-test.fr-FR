<span data-ttu-id="3d1d3-101">Utilisez les URL de déploiement à distance de hello CLI d’Azure tooget hello pour votre application API.</span><span class="sxs-lookup"><span data-stu-id="3d1d3-101">Use hello Azure CLI tooget hello remote deployment URL for your API App.</span></span> <span data-ttu-id="3d1d3-102">Bonjour suivant de commande, remplacez  *\<nom_application >* avec le nom de votre application web.</span><span class="sxs-lookup"><span data-stu-id="3d1d3-102">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="3d1d3-103">Configurez votre local Git déploiement toobe toopush en mesure de toohello à distance.</span><span class="sxs-lookup"><span data-stu-id="3d1d3-103">Configure your local Git deployment toobe able toopush toohello remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="3d1d3-104">Push toohello Azure toodeploy à distance de votre application.</span><span class="sxs-lookup"><span data-stu-id="3d1d3-104">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="3d1d3-105">Vous êtes invité au mot de passe hello que vous avez créé précédemment lors de la création d’utilisateur du déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="3d1d3-105">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="3d1d3-106">Assurez-vous que vous entrez hello mot de passe créé dans démarrage rapide de hello et pas hello vous utilisez toolog dans toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3d1d3-106">Make sure that you enter hello password you created in earlier in hello quickstart, and not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```
