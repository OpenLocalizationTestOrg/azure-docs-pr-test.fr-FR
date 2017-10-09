## <a name="push-tooazure-from-git"></a><span data-ttu-id="cb86f-101">TooAzure par émission de données à partir de Git</span><span class="sxs-lookup"><span data-stu-id="cb86f-101">Push tooAzure from Git</span></span>

<span data-ttu-id="cb86f-102">Ajouter un référentiel Git Azure tooyour à distance.</span><span class="sxs-lookup"><span data-stu-id="cb86f-102">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="cb86f-103">Push toohello Azure toodeploy à distance de votre application.</span><span class="sxs-lookup"><span data-stu-id="cb86f-103">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="cb86f-104">Vous êtes invité au mot de passe hello que vous avez créé précédemment lors de la création d’utilisateur du déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="cb86f-104">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="cb86f-105">Assurez-vous que vous entrez le mot de passe hello créé dans [configurer un utilisateur de déploiement](#configure-a-deployment-user), pas hello mot de passe toolog dans toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cb86f-105">Make sure that you enter hello password you created in [Configure a deployment user](#configure-a-deployment-user), not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```

<span data-ttu-id="cb86f-106">Hello précédant la commande affiche des informations similaires toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="cb86f-106">hello preceding command displays information similar toohello following example:</span></span>
