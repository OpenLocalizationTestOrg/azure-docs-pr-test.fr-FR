<span data-ttu-id="d1c4e-101">Configurer Git déploiement toohello l’application web locale avec hello [source liée à un déploiement de webapp dans az-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) commande.</span><span class="sxs-lookup"><span data-stu-id="d1c4e-101">Configure local Git deployment toohello web app with hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="d1c4e-102">Service d’applications prend en charge plusieurs façons toodeploy tooa contenu application web, tels que FTP, Git local, GitHub, Visual Studio Team Services et Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="d1c4e-102">App Service supports several ways toodeploy content tooa web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="d1c4e-103">Pour ce démarrage rapide, vous effectuez le déploiement à l’aide de Git local.</span><span class="sxs-lookup"><span data-stu-id="d1c4e-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="d1c4e-104">Cela signifie que vous déployez à l’aide d’un toopush de commande Git à partir d’un référentiel tooa local dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d1c4e-104">That means you deploy by using a Git command toopush from a local repository tooa repository in Azure.</span></span> 

<span data-ttu-id="d1c4e-105">Bonjour suivant de commande, remplacez  *\<nom_application >* avec le nom de votre application web.</span><span class="sxs-lookup"><span data-stu-id="d1c4e-105">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="d1c4e-106">sortie de Hello a hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="d1c4e-106">hello output has hello following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="d1c4e-107">Hello `<username>` est hello [utilisateur du déploiement](#configure-a-deployment-user) que vous avez créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="d1c4e-107">hello `<username>` is hello [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="d1c4e-108">Copiez hello URI affichée ; vous allez l’utiliser dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="d1c4e-108">Copy hello URI shown; you'll use it in hello next step.</span></span>
