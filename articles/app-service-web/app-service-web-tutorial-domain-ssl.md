---
title: "application web de domaine personnalisé d’aaaAdd et SSL tooan Azure | Documents Microsoft"
description: "Découvrez comment tooprepare votre Azure web production de toogo application en ajoutant la marque de votre société. Mapper hello domaine personnalisé nom (domaine personnel) tooyour web app et sécurisez-le avec un certificat SSL personnalisé."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a><span data-ttu-id="471b5-104">Ajouter des domaines personnalisés et SSL tooan Azure web app</span><span class="sxs-lookup"><span data-stu-id="471b5-104">Add custom domain and SSL tooan Azure web app</span></span>

<span data-ttu-id="471b5-105">Ce didacticiel vous montre comment tooquickly mapper une application web Azure de domaine personnalisé nom tooyour et sécuriser avec un certificat SSL personnalisé.</span><span class="sxs-lookup"><span data-stu-id="471b5-105">This tutorial shows you how tooquickly map a custom domain name tooyour Azure web app and then secure it with a custom SSL certificate.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="471b5-106">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="471b5-106">Before you begin</span></span>

<span data-ttu-id="471b5-107">Avant d’exécuter cet exemple, installez hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) localement.</span><span class="sxs-lookup"><span data-stu-id="471b5-107">Before running this sample, install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) locally.</span></span>

<span data-ttu-id="471b5-108">Vous devez également la page de configuration d’un accès administratif toohello DNS pour votre fournisseur de leur domaine respectif.</span><span class="sxs-lookup"><span data-stu-id="471b5-108">You also need administrative access toohello DNS configuration page for your respective domain provider.</span></span> <span data-ttu-id="471b5-109">Par exemple, tooadd `www.contoso.com`, vous devez toobe tooconfigure en mesure des entrées DNS pour `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="471b5-109">For example, tooadd `www.contoso.com`, you need toobe able tooconfigure DNS entries for `contoso.com`.</span></span>

<span data-ttu-id="471b5-110">Enfin, vous devez valide. Le fichier PFX _et_ son mot de passe pour le certificat SSL de hello souhaité tooupload et établir une liaison.</span><span class="sxs-lookup"><span data-stu-id="471b5-110">Lastly, you need a valid .PFX file _and_ its password for hello SSL certificate you want tooupload and bind.</span></span> <span data-ttu-id="471b5-111">Ce certificat SSL doit être le nom de domaine personnalisé configuré toosecure hello souhaité.</span><span class="sxs-lookup"><span data-stu-id="471b5-111">This SSL certificate should be configured toosecure hello custom domain name you want.</span></span> <span data-ttu-id="471b5-112">Bonjour exemple ci-dessus, votre certificat SSL doit sécuriser `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="471b5-112">In hello above example, your SSL certificate should secure `www.contoso.com`.</span></span> 

## <a name="step-1---create-an-azure-web-app"></a><span data-ttu-id="471b5-113">Étape 1 : Créer une application web Azure</span><span class="sxs-lookup"><span data-stu-id="471b5-113">Step 1 - Create an Azure web app</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="471b5-114">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="471b5-114">Log in tooAzure</span></span>

<span data-ttu-id="471b5-115">Nous sommes maintenant continu toouse hello Azure CLI 2.0 dans un fenêtre de terminal toocreate hello des ressources nécessaires toohost notre application Node.js dans Azure.</span><span class="sxs-lookup"><span data-stu-id="471b5-115">We are now going toouse hello Azure CLI 2.0 in a terminal window toocreate hello resources needed toohost our Node.js app in Azure.</span></span>  <span data-ttu-id="471b5-116">Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran.</span><span class="sxs-lookup"><span data-stu-id="471b5-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="471b5-117">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="471b5-117">Create a resource group</span></span>   
<span data-ttu-id="471b5-118">Créer un groupe de ressources avec hello [az groupe créer](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="471b5-118">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="471b5-119">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure comme les applications web, les bases de données et les comptes de stockage sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="471b5-119">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

<span data-ttu-id="471b5-120">toosee quel possible les valeurs que vous pouvez utiliser pour `---location`, utilisez hello `az appservice list-locations` commande CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="471b5-120">toosee what possible values you can use for `---location`, use hello `az appservice list-locations` Azure CLI command.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="471b5-121">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="471b5-121">Create an App Service plan</span></span>

<span data-ttu-id="471b5-122">Créer un plan App Service avec hello [création d’un plan de az](/cli/azure/appservice/plan#create) commande.</span><span class="sxs-lookup"><span data-stu-id="471b5-122">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="471b5-123">Hello exemple suivant crée un plan App Service nommé `myAppServicePlan` à l’aide de hello **base** niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="471b5-123">hello following example creates an App Service plan named `myAppServicePlan` using hello **Basic** pricing tier.</span></span>

<span data-ttu-id="471b5-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span><span class="sxs-lookup"><span data-stu-id="471b5-124">az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1</span></span>

<span data-ttu-id="471b5-125">Lorsque hello plan App Service a été créé, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="471b5-125">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a><span data-ttu-id="471b5-126">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="471b5-126">Create a web app</span></span>

<span data-ttu-id="471b5-127">Maintenant qu’un plan App Service a été créé, créez une application web au sein de hello `myAppServicePlan` plan App Service.</span><span class="sxs-lookup"><span data-stu-id="471b5-127">Now that an App Service plan has been created, create a web app within hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="471b5-128">fournit les application Hello web vous êtes un hébergement toodeploy d’espace de votre code et fournit aussi une URL pour vous tooview hello déployé l’application.</span><span class="sxs-lookup"><span data-stu-id="471b5-128">hello web app gives your a hosting space toodeploy your code as well as provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="471b5-129">Hello d’utilisation [web du service d’applications az créer](/cli/azure/appservice/web#create) commande toocreate hello web app.</span><span class="sxs-lookup"><span data-stu-id="471b5-129">Use hello [az appservice web create](/cli/azure/appservice/web#create) command toocreate hello web app.</span></span> 

<span data-ttu-id="471b5-130">Dans la commande de hello ci-dessous, remplacez par votre propre nom d’application unique dans lequel vous consultez hello `<app_name>` espace réservé.</span><span class="sxs-lookup"><span data-stu-id="471b5-130">In hello command below, please substitute your own unique app name where you see hello `<app_name>` placeholder.</span></span> <span data-ttu-id="471b5-131">Ce nom unique servira en tant que partie hello hello par défaut du nom de domaine pour l’application web de hello, par conséquent, le nom de hello doit toobe unique entre toutes les applications dans Azure.</span><span class="sxs-lookup"><span data-stu-id="471b5-131">This unique name will be used as hello part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="471b5-132">Vous pouvez mapper plus tard de n’importe quelle application web du toohello personnalisée DNS entrée avant de vous exposez tooyour utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="471b5-132">You can later map any custom DNS entry toohello web app before you expose it tooyour users.</span></span> 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

<span data-ttu-id="471b5-133">Lorsque l’application hello web a été créée, hello CLI d’Azure affiche des informations similaires toohello est l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="471b5-133">When hello web app has been created, hello Azure CLI shows information similar toohello following example.</span></span> 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

<span data-ttu-id="471b5-134">À partir de la sortie JSON, de hello `defaultHostName` affiche le nom de domaine par défaut de votre application web.</span><span class="sxs-lookup"><span data-stu-id="471b5-134">From hello JSON output, `defaultHostName` shows your web app's default domain name.</span></span> <span data-ttu-id="471b5-135">Dans votre navigateur, accédez à toothis adresse.</span><span class="sxs-lookup"><span data-stu-id="471b5-135">In your browser, navigate toothis address.</span></span>

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a><span data-ttu-id="471b5-137">Étape 2 : Configurer le mappage DNS</span><span class="sxs-lookup"><span data-stu-id="471b5-137">Step 2 - Configure DNS mapping</span></span>

<span data-ttu-id="471b5-138">Dans cette étape, vous ajoutez un mappage de nom de domaine tooyour de domaine personnalisé d’une application de web par défaut, `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="471b5-138">In this step, you add a mapping from a custom domain tooyour web app's default domain name, `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="471b5-139">En général, vous effectuez cette étape sur le site web du fournisseur de votre domaine.</span><span class="sxs-lookup"><span data-stu-id="471b5-139">Typically, you perform this step in your domain provider's website.</span></span> <span data-ttu-id="471b5-140">Comme le site web de chaque bureau d’enregistrement des domaines est légèrement différent, vous devez consulter la documentation de votre fournisseur.</span><span class="sxs-lookup"><span data-stu-id="471b5-140">Every domain registrar's website is slightly different, so you should consult your provider's documentation.</span></span> <span data-ttu-id="471b5-141">Voici néanmoins quelques recommandations générales.</span><span class="sxs-lookup"><span data-stu-id="471b5-141">However, here are some general guidelines.</span></span> 

### <a name="navigate-tootoodns-management-page"></a><span data-ttu-id="471b5-142">Parcourir la page de gestion tootooDNS</span><span class="sxs-lookup"><span data-stu-id="471b5-142">Navigate tootooDNS management page</span></span>

<span data-ttu-id="471b5-143">Tout d’abord, ouvrez une session dans le site Web de tooyour de domaines.</span><span class="sxs-lookup"><span data-stu-id="471b5-143">First, log in tooyour domain registrar's website.</span></span>  

<span data-ttu-id="471b5-144">Recherchez la page de hello pour la gestion des enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="471b5-144">Then, find hello page for managing DNS records.</span></span> <span data-ttu-id="471b5-145">Recherchez des liens ou des zones du site hello étiqueté **nom de domaine**, **DNS**, ou **gestion des noms de serveur**.</span><span class="sxs-lookup"><span data-stu-id="471b5-145">Look for links or areas of hello site labeled **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="471b5-146">Souvent, vous pouvez trouver hello lien en affichant les informations de votre compte et puis recherchez un lien comme **mes domaines**.</span><span class="sxs-lookup"><span data-stu-id="471b5-146">Often, you can find hello link by viewing your account information, and then looking for a link such as **My domains**.</span></span>

<span data-ttu-id="471b5-147">Une fois que vous avez trouvé la page, recherchez un lien vous permettant d’ajouter ou de modifier des enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="471b5-147">Once you find this page, look for a link that lets you add or edit DNS records.</span></span> <span data-ttu-id="471b5-148">Il s’agit probablement d’un lien de **fichier de zone** ou d’**enregistrements DNS**, ou encore d’un lien de **configuration avancé**.</span><span class="sxs-lookup"><span data-stu-id="471b5-148">This might be a **Zone file** or **DNS Records** link, or an **Advanced configuration** link.</span></span>

### <a name="create-a-cname-record"></a><span data-ttu-id="471b5-149">Créer un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="471b5-149">Create a CNAME record</span></span>

<span data-ttu-id="471b5-150">Ajoutez un enregistrement CNAME qui mappe le nom de domaine hello sous-domaine souhaitée nom tooyour l’application web par défaut (`<app_name>.azurewebsites.net`, où `<app_name>` est le nom unique de votre application).</span><span class="sxs-lookup"><span data-stu-id="471b5-150">Add a CNAME record that maps hello desired subdomain name tooyour web app's default domain name (`<app_name>.azurewebsites.net`, where `<app_name>` is your app's unique name).</span></span>

<span data-ttu-id="471b5-151">Pourquoi `www.contoso.com` exemple, vous créez un enregistrement CNAME qui mappe hello `www` nom d’hôte trop`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="471b5-151">For hello `www.contoso.com` example, you create a CNAME that maps hello `www` hostname too`<app_name>.azurewebsites.net`.</span></span>

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a><span data-ttu-id="471b5-152">Étape 3 : configurer un domaine personnalisé de hello sur votre application web</span><span class="sxs-lookup"><span data-stu-id="471b5-152">Step 3 - Configure hello custom domain on your web app</span></span>

<span data-ttu-id="471b5-153">Lorsque vous avez terminé la configuration d’une correspondance de nom d’hôte hello dans le site Web du fournisseur de votre domaine, vous êtes domaine personnalisé de prêt tooconfigure hello sur votre application web.</span><span class="sxs-lookup"><span data-stu-id="471b5-153">When you finish configuring hello hostname mapping in your domain provider's website, you're ready tooconfigure hello custom domain on your web app.</span></span> <span data-ttu-id="471b5-154">Hello d’utilisation [az app service web config hostname ajouter](/cli/azure/appservice/web/config/hostname#add) commande tooadd cette configuration.</span><span class="sxs-lookup"><span data-stu-id="471b5-154">Use hello [az appservice web config hostname add](/cli/azure/appservice/web/config/hostname#add) command tooadd this configuration.</span></span> 

<span data-ttu-id="471b5-155">Dans la commande hello ci-dessous, remplacez `<app_name>` avec votre nom d’application unique et < your_custom_domain > avec le nom de domaine personnalisé complet hello (par exemple, `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="471b5-155">In hello command below, please substitute `<app_name>` with your unique app name, and <your_custom_domain> with hello fully qualified custom domain name (e.g. `www.contoso.com`).</span></span> 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

<span data-ttu-id="471b5-156">domaine personnalisé de Hello est maintenant entièrement mappé tooyour l’application web.</span><span class="sxs-lookup"><span data-stu-id="471b5-156">hello custom domain now is fully mapped tooyour web app.</span></span> <span data-ttu-id="471b5-157">Dans votre navigateur, accédez à nom de domaine personnalisé toohello.</span><span class="sxs-lookup"><span data-stu-id="471b5-157">In your browser, navigate toohello custom domain name.</span></span> <span data-ttu-id="471b5-158">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="471b5-158">For example:</span></span>

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a><span data-ttu-id="471b5-160">Étape 4 : lier une application du web tooyour de certificat SSL personnalisée</span><span class="sxs-lookup"><span data-stu-id="471b5-160">Step 4 - Bind a custom SSL certificate tooyour web app</span></span>

<span data-ttu-id="471b5-161">Vous disposez maintenant d’une application web Azure, avec le nom de domaine hello souhaité dans la barre d’adresses du navigateur hello.</span><span class="sxs-lookup"><span data-stu-id="471b5-161">You now have an Azure web app, with hello domain name you want in hello browser's address bar.</span></span> <span data-ttu-id="471b5-162">Toutefois, si vous accédez toohello `https://<your_custom_domain>` maintenant, vous obtenez une erreur de certificat.</span><span class="sxs-lookup"><span data-stu-id="471b5-162">However, if you navigate toohello `https://<your_custom_domain>` now, you get a certificate error.</span></span> 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

<span data-ttu-id="471b5-164">Cette erreur est due au fait que votre application web ne dispose pas encore d’une liaison de certificat SSL correspondant à votre nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="471b5-164">This error occurs because your web app doesn't yet have an SSL certificate binding that matches your custom domain name.</span></span> <span data-ttu-id="471b5-165">Toutefois, vous n’obtenez une erreur si vous accédez trop`https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="471b5-165">However, you don't get an error if you navigate too`https://<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="471b5-166">C’est parce que votre application, ainsi que toutes les applications de Service d’applications Azure, est sécurisé avec un certificat SSL pour hello hello `*.azurewebsites.net` domaine générique par défaut.</span><span class="sxs-lookup"><span data-stu-id="471b5-166">This is because your app, as well as all Azure App Service apps, is secured with hello SSL certificate for hello `*.azurewebsites.net` wildcard domain by default.</span></span> 

<span data-ttu-id="471b5-167">Dans commande tooaccess votre application web par le nom de votre domaine personnalisé, vous devez certificat SSL de hello toobind pour votre application web de toohello domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="471b5-167">In order tooaccess your web app by your custom domain name, you need toobind hello SSL certificate for your custom domain toohello web app.</span></span> <span data-ttu-id="471b5-168">Vous le ferez lors de cette étape.</span><span class="sxs-lookup"><span data-stu-id="471b5-168">You will do it in this step.</span></span> 

### <a name="upload-hello-ssl-certificate"></a><span data-ttu-id="471b5-169">Télécharger le certificat SSL de hello</span><span class="sxs-lookup"><span data-stu-id="471b5-169">Upload hello SSL certificate</span></span>

<span data-ttu-id="471b5-170">Télécharger le certificat SSL de hello pour votre application web de tooyour domaine personnalisé à l’aide de hello [le téléchargement ssl config az app service web](/cli/azure/appservice/web/config/ssl#upload) commande.</span><span class="sxs-lookup"><span data-stu-id="471b5-170">Upload hello SSL certificate for your custom domain tooyour web app by using hello [az appservice web config ssl upload](/cli/azure/appservice/web/config/ssl#upload) command.</span></span>

<span data-ttu-id="471b5-171">Dans la commande hello ci-dessous, remplacez `<app_name>` avec le nom de votre application unique, `<path_to_ptx_file>` avec tooyour de chemin d’accès hello. Le fichier PFX, et `<password>` avec mot de passe de votre certificat.</span><span class="sxs-lookup"><span data-stu-id="471b5-171">In hello command below, please substitute `<app_name>` with your unique app name, `<path_to_ptx_file>` with hello path tooyour .PFX file, and `<password>` with your certificate's password.</span></span> 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

<span data-ttu-id="471b5-172">Lorsque le certificat de hello est téléchargé, hello CLI d’Azure s’affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="471b5-172">When hello certificate is uploaded, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

<span data-ttu-id="471b5-173">À partir de la sortie JSON, de hello `thumbprint` affiche l’empreinte numérique de votre certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="471b5-173">From hello JSON output, `thumbprint` shows your uploaded certificate's thumbprint.</span></span> <span data-ttu-id="471b5-174">Copiez sa valeur pour l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="471b5-174">Copy its value for hello next step.</span></span>

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a><span data-ttu-id="471b5-175">Lier l’application web toohello hello téléchargé SSL certificat</span><span class="sxs-lookup"><span data-stu-id="471b5-175">Bind hello uploaded SSL certificate toohello web app</span></span>

<span data-ttu-id="471b5-176">Votre application web a maintenant le nom de domaine personnalisé hello souhaité, et il possède également un certificat SSL qui sécurise de ce domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="471b5-176">Your web app now has hello custom domain name you want, and it also has a SSL certificate that secures that custom domain.</span></span> <span data-ttu-id="471b5-177">Bonjour chose uniquement les toodo gauche est l’application web toohello toobind hello certificat téléchargé.</span><span class="sxs-lookup"><span data-stu-id="471b5-177">hello only thing left toodo is toobind hello uploaded certificate toohello web app.</span></span> <span data-ttu-id="471b5-178">Pour cela, vous devez utiliser hello [liaison ssl de az app service web config](/cli/azure/appservice/web/config/ssl#bind) commande.</span><span class="sxs-lookup"><span data-stu-id="471b5-178">You do this by using hello [az appservice web config ssl bind](/cli/azure/appservice/web/config/ssl#bind) command.</span></span>

<span data-ttu-id="471b5-179">Dans la commande hello ci-dessous, remplacez `<app_name>` avec le nom de votre application unique et `<thumbprint-from-previous-output>` avec l’empreinte numérique du certificat hello que vous obtenez à partir de la commande précédente hello.</span><span class="sxs-lookup"><span data-stu-id="471b5-179">In hello command below, please substitute `<app_name>` with your unique app name and `<thumbprint-from-previous-output>` with hello certificate thumbprint that you get from hello previous command.</span></span> 

<span data-ttu-id="471b5-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span><span class="sxs-lookup"><span data-stu-id="471b5-180">az appservice web config ssl bind --name <app_name> --resource-group myResourceGroup --certificate-thumbprint <thumbprint-from-previous-output> --ssl-type SNI</span></span>

<span data-ttu-id="471b5-181">Lorsque les certificats hello sont lié tooyour web app, hello CLI d’Azure s’affiche des informations similaires toohello est l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="471b5-181">When hello certificate is bound tooyour web app, hello Azure CLI shows information similar toohello following example:</span></span>

<span data-ttu-id="471b5-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span><span class="sxs-lookup"><span data-stu-id="471b5-182">{ "availabilityState": "Normal", "clientAffinityEnabled": true, "clientCertEnabled": false, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "<app_name>.azurewebsites.net", "enabled": true, "enabledHostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net", "<app_name>.scm.azurewebsites.net" ], "gatewaySiteName": null, "hostNameSslStates": [ { "hostType": "Standard", "name": "<app_name>.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Repository", "name": "<app_name>.scm.azurewebsites.net", "sslState": "Disabled", "thumbprint": null, "toUpdate": null, "virtualIp": null }, { "hostType": "Standard", "name": "www.contoso.com", "sslState": "SniEnabled", "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "virtualIp": null } ], "hostNames": [ "www.contoso.com", "<app_name>.azurewebsites.net" ], "hostNamesDisabled": false, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s/<app_name>", "isDefaultContainer": null, "kind": "WebApp", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "location": "West Europe", "maxNumberOfWorkers": null, "microService": "false", "name": "<app_name>", "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "<app_name>", "reserved": false, "resourceGroup": "myResourceGroup", "scmSiteAlsoStopped": false, "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "state": "Running", "suspendedTill": null, "tags": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal" }</span></span>

<span data-ttu-id="471b5-183">Dans votre navigateur, accédez à tooHTTPS de point de terminaison de votre nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="471b5-183">In your browser, navigate tooHTTPS endpoint of your custom domain name.</span></span> <span data-ttu-id="471b5-184">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="471b5-184">For example:</span></span>

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a><span data-ttu-id="471b5-186">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="471b5-186">More resources</span></span>

<span data-ttu-id="471b5-187">[Acheter et configurer un nom de domaine personnalisé dans Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[acheter et configurer un certificat SSL pour votre service Azure App Service](web-sites-purchase-ssl-web-site.md)</span><span class="sxs-lookup"><span data-stu-id="471b5-187">[Buy and Configure a custom domain name in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[Buy and Configure an SSL Certificate for your Azure App Service](web-sites-purchase-ssl-web-site.md)</span></span>
