---
title: "Mapper un nom DNS personnalisé existant à des applications web Azure | Microsoft Docs"
description: "Découvrez comment ajouter un nom de domaine DNS (domaine personnel) à une application web, au serveur principal d’une application mobile ou à une application API dans Azure App Service."
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
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 973cda462e8d258cc848e1036891c7f8af043102
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="map-an-existing-custom-dns-name-to-azure-web-apps"></a><span data-ttu-id="52dd7-103">Mapper un nom DNS personnalisé existant à des applications web Azure</span><span class="sxs-lookup"><span data-stu-id="52dd7-103">Map an existing custom DNS name to Azure Web Apps</span></span>

<span data-ttu-id="52dd7-104">[Azure Web Apps](app-service-web-overview.md) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="52dd7-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="52dd7-105">Ce didacticiel vous montre comment mapper un nom DNS personnalisé existant à des applications web Azure.</span><span class="sxs-lookup"><span data-stu-id="52dd7-105">This tutorial shows you how to map an existing custom DNS name to Azure Web Apps.</span></span>

![Navigation au sein du portail pour accéder à l’application Azure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="52dd7-107">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="52dd7-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52dd7-108">Mapper un sous-domaine (par exemple, `www.contoso.com`) à l’aide d’un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="52dd7-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="52dd7-109">Mapper un domaine racine (par exemple, `contoso.com`) à l’aide d’un enregistrement A</span><span class="sxs-lookup"><span data-stu-id="52dd7-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="52dd7-110">Mapper un domaine générique (par exemple, `*.contoso.com`) à l’aide d’un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="52dd7-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="52dd7-111">Automatiser le mappage de domaine à l’aide de scripts</span><span class="sxs-lookup"><span data-stu-id="52dd7-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="52dd7-112">Vous pouvez utiliser un **enregistrement CNAME** ou un **enregistrement A** pour mapper un nom DNS personnalisé à App Service.</span><span class="sxs-lookup"><span data-stu-id="52dd7-112">You can use either a **CNAME record** or an **A record** to map a custom DNS name to App Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="52dd7-113">Nous vous recommandons d’utiliser un enregistrement CNAME pour tous les noms DNS personnalisés, à l’exception d’un domaine racine (par exemple, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="52dd7-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="52dd7-114">Pour migrer un site actif et son nom de domaine DNS vers App Service, voir [Migrer un nom DNS actif vers Azure App Service](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="52dd7-114">To migrate a live site and its DNS domain name to App Service, see [Migrate an active DNS name to Azure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52dd7-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="52dd7-115">Prerequisites</span></span>

<span data-ttu-id="52dd7-116">Pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="52dd7-116">To complete this tutorial:</span></span>

* <span data-ttu-id="52dd7-117">[Créez une application App Service](/azure/app-service/), ou utilisez une application créée pour un autre didacticiel.</span><span class="sxs-lookup"><span data-stu-id="52dd7-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="52dd7-118">Achetez un nom de domaine et assurez-vous que vous avez accès au registre DNS pour votre fournisseur de domaines (par exemple, GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="52dd7-118">Purchase a domain name and make sure you have access to the DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="52dd7-119">Par exemple, pour ajouter des entrées DNS pour `contoso.com` et `www.contoso.com`, vous devez pouvoir configurer les paramètres DNS du domaine racine `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="52dd7-119">For example, to add DNS entries for `contoso.com` and `www.contoso.com`, you must be able to configure the DNS settings for the `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="52dd7-120">Si vous ne disposez d’aucun nom de domaine existant, envisagez d’[acheter un domaine à l’aide du portail Azure](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="52dd7-120">If you don't have an existing domain name, consider [purchasing a domain using the Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-the-app"></a><span data-ttu-id="52dd7-121">Préparer l’application</span><span class="sxs-lookup"><span data-stu-id="52dd7-121">Prepare the app</span></span>

<span data-ttu-id="52dd7-122">Pour mapper un nom DNS personnalisé à une application web, le [plan App Service](https://azure.microsoft.com/pricing/details/app-service/) de l’application web doit être un niveau payant (**Partagé**, **De base**, **Standard** ou **Premium**).</span><span class="sxs-lookup"><span data-stu-id="52dd7-122">To map a custom DNS name to a web app, the web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="52dd7-123">Au cours de cette étape, vous allez vous assurer que l’application App Service se trouve dans le niveau de tarification pris en charge.</span><span class="sxs-lookup"><span data-stu-id="52dd7-123">In this step, you make sure that the App Service app is in the supported pricing tier.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="52dd7-124">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="52dd7-124">Sign in to Azure</span></span>

<span data-ttu-id="52dd7-125">Ouvrez le [portail Azure](https://portal.azure.com) et connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="52dd7-125">Open the [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-to-the-app-in-the-azure-portal"></a><span data-ttu-id="52dd7-126">Accéder à l’application dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="52dd7-126">Navigate to the app in the Azure portal</span></span>

<span data-ttu-id="52dd7-127">Dans le menu de gauche, sélectionnez **App Services**, puis le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="52dd7-127">From the left menu, select **App Services**, and then select the name of the app.</span></span>

![Navigation au sein du portail pour accéder à l’application Azure](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="52dd7-129">La page de gestion de l’application App Service s’affiche.</span><span class="sxs-lookup"><span data-stu-id="52dd7-129">You see the management page of the App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-the-pricing-tier"></a><span data-ttu-id="52dd7-130">Vérification du niveau tarifaire</span><span class="sxs-lookup"><span data-stu-id="52dd7-130">Check the pricing tier</span></span>

<span data-ttu-id="52dd7-131">Dans la navigation gauche de la page de l’application, faites défiler jusqu’à la section **Paramètres** et sélectionnez **Monter en puissance (plan App Service)**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-131">In the left navigation of the app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu Monter en puissance](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="52dd7-133">Le niveau actuel de l’application est encadré d’un rectangle bleu.</span><span class="sxs-lookup"><span data-stu-id="52dd7-133">The app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="52dd7-134">Vérifiez que l’application ne se trouve pas dans le niveau **Gratuit**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-134">Check to make sure that the app is not in the **Free** tier.</span></span> <span data-ttu-id="52dd7-135">Les DNS personnalisés ne sont pas pris en charge dans le niveau **Gratuit**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-135">Custom DNS is not supported in the **Free** tier.</span></span> 

![Vérification du niveau de tarification](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="52dd7-137">Si le plan App Service n’est pas **Gratuit** , fermez la page **Choisir votre niveau de tarification** et passez à [Mapper un enregistrement CNAME](#cname).</span><span class="sxs-lookup"><span data-stu-id="52dd7-137">If the App Service plan is not **Free**, close the **Choose your pricing tier** page and skip to [Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-the-app-service-plan"></a><span data-ttu-id="52dd7-138">Monter en puissance le plan App Service</span><span class="sxs-lookup"><span data-stu-id="52dd7-138">Scale up the App Service plan</span></span>

<span data-ttu-id="52dd7-139">Sélectionnez l’un des niveaux payants (**Partagé**, **De base**, **Standard** ou **Premium**).</span><span class="sxs-lookup"><span data-stu-id="52dd7-139">Select any of the non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="52dd7-140">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-140">Click **Select**.</span></span>

![Vérification du niveau de tarification](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="52dd7-142">Lorsque la notification suivante s’affiche, cela signifie que l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="52dd7-142">When you see the following notification, the scale operation is complete.</span></span>

![Confirmation d’opération de mise à l’échelle](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="52dd7-144">Mapper un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="52dd7-144">Map a CNAME record</span></span>

<span data-ttu-id="52dd7-145">Dans l’exemple de ce didacticiel, vous ajoutez un enregistrement CNAME pour le sous-domaine `www` (`www.contoso.com`, par exemple).</span><span class="sxs-lookup"><span data-stu-id="52dd7-145">In the tutorial example, you add a CNAME record for the `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="52dd7-146">Créer un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="52dd7-146">Create the CNAME record</span></span>

<span data-ttu-id="52dd7-147">Ajoutez un enregistrement CNAME pour mapper un sous-domaine au nom d’hôte par défaut de l’application (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="52dd7-147">Add a CNAME record to map a subdomain to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="52dd7-148">Pour l’exemple de domaine `www.contoso.com`, ajoutez un enregistrement CNAME qui mappe le nom `www` à `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="52dd7-148">For the `www.contoso.com` domain example, add a CNAME record that maps the name `www` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="52dd7-149">Après avoir ajouté l’enregistrement CNAME, la page d’enregistrements DNS ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="52dd7-149">After you add the CNAME, the DNS records page looks like the following example:</span></span>

![Navigation au sein du portail pour accéder à l’application Azure](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-the-cname-record-mapping-in-azure"></a><span data-ttu-id="52dd7-151">Activer le mappage d’enregistrement CNAME dans Azure</span><span class="sxs-lookup"><span data-stu-id="52dd7-151">Enable the CNAME record mapping in Azure</span></span>

<span data-ttu-id="52dd7-152">Dans le volet de navigation gauche de la page d’application du portail Azure, sélectionnez **Domaines personnalisés**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-152">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Menu Domaines personnalisés](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="52dd7-154">Dans la page **Domaines personnalisés** de l’application, ajoutez le nom DNS personnalisé complet (`www.contoso.com`) à la liste.</span><span class="sxs-lookup"><span data-stu-id="52dd7-154">In the **Custom domains** page of the app, add the fully qualified custom DNS name (`www.contoso.com`) to the list.</span></span>

<span data-ttu-id="52dd7-155">Cliquez sur l’icône **+** en regard de **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-155">Select the **+** icon next to **Add hostname**.</span></span>

![Ajouter un nom d’hôte](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="52dd7-157">Tapez le nom de domaine complet que vous avez ajouté pour un enregistrement CNAME, tel que `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="52dd7-157">Type the fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="52dd7-158">Sélectionnez **Valider**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-158">Select **Validate**.</span></span>

<span data-ttu-id="52dd7-159">Le bouton **Ajouter un nom d’hôte** est activé.</span><span class="sxs-lookup"><span data-stu-id="52dd7-159">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="52dd7-160">Assurez-vous que **Type d’enregistrement du nom d’hôte** est défini sur **Enregistrement CNAME (exemple.com ou tout sous-domaine)**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-160">Make sure that **Hostname record type** is set to **CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="52dd7-161">Sélectionnez **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-161">Select **Add hostname**.</span></span>

![Ajouter un nom DNS à l’application](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="52dd7-163">Un certain temps peut être nécessaire pour que le nouveau nom d’hôte soit reflété sur la page **Domaines personnalisés** de votre application.</span><span class="sxs-lookup"><span data-stu-id="52dd7-163">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="52dd7-164">Essayez d’actualiser le navigateur pour mettre à jour les données.</span><span class="sxs-lookup"><span data-stu-id="52dd7-164">Try refreshing the browser to update the data.</span></span>

![Enregistrement CNAME ajouté](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="52dd7-166">Si vous avez raté une étape ou fait une faute de frappe à un endroit, une erreur de vérification peut apparaître au bas de la page.</span><span class="sxs-lookup"><span data-stu-id="52dd7-166">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Erreur de vérification](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="52dd7-168">Mapper un enregistrement A</span><span class="sxs-lookup"><span data-stu-id="52dd7-168">Map an A record</span></span>

<span data-ttu-id="52dd7-169">Dans l’exemple de ce didacticiel, vous ajoutez un enregistrement A pour le domaine racine (par exemple, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="52dd7-169">In the tutorial example, you add an A record for the root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-the-apps-ip-address"></a><span data-ttu-id="52dd7-170">Copier l’adresse IP de l’application</span><span class="sxs-lookup"><span data-stu-id="52dd7-170">Copy the app's IP address</span></span>

<span data-ttu-id="52dd7-171">Pour mapper un enregistrement A, vous avez besoin de l’adresse IP externe de l’application.</span><span class="sxs-lookup"><span data-stu-id="52dd7-171">To map an A record, you need the app's external IP address.</span></span> <span data-ttu-id="52dd7-172">Vous pouvez trouver cette adresse IP sur la page **Domaines personnalisés** de l’application dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="52dd7-172">You can find this IP address in the app's **Custom domains** page in the Azure portal.</span></span>

<span data-ttu-id="52dd7-173">Dans le volet de navigation gauche de la page d’application du portail Azure, sélectionnez **Domaines personnalisés**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-173">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Menu Domaines personnalisés](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="52dd7-175">Dans la page **Domaines personnalisés**, copiez l’adresse IP de l’application.</span><span class="sxs-lookup"><span data-stu-id="52dd7-175">In the **Custom domains** page, copy the app's IP address.</span></span>

![Navigation au sein du portail pour accéder à l’application Azure](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-a-record"></a><span data-ttu-id="52dd7-177">Créer l’enregistrement A</span><span class="sxs-lookup"><span data-stu-id="52dd7-177">Create the A record</span></span>

<span data-ttu-id="52dd7-178">Pour mapper un enregistrement A à une application, App Service a besoin de **deux** enregistrements DNS :</span><span class="sxs-lookup"><span data-stu-id="52dd7-178">To map an A record to an app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="52dd7-179">Un enregistrement **A** pour effectuer un mappage vers l’adresse IP de l’application.</span><span class="sxs-lookup"><span data-stu-id="52dd7-179">An **A** record to map to the app's IP address.</span></span>
- <span data-ttu-id="52dd7-180">Un enregistrement **TXT** pour effectuer un mappage vers le nom d’hôte par défaut de l’application `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="52dd7-180">A **TXT** record to map to the app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="52dd7-181">App Service utilise cet enregistrement uniquement au moment de la configuration, pour vérifier que vous possédez le domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="52dd7-181">App Service uses this record only at configuration time, to verify that you own the custom domain.</span></span> <span data-ttu-id="52dd7-182">Une fois votre domaine personnalisé validé et configuré dans App Service, vous pourrez supprimer cet enregistrement TXT.</span><span class="sxs-lookup"><span data-stu-id="52dd7-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="52dd7-183">Pour l’exemple de domaine `contoso.com`, créez les enregistrements A et TXT d’après le tableau suivant (`@` représente généralement le domaine racine).</span><span class="sxs-lookup"><span data-stu-id="52dd7-183">For the `contoso.com` domain example, create the A and TXT records according to the following table (`@` typically represents the root domain).</span></span> 

| <span data-ttu-id="52dd7-184">Type d’enregistrement</span><span class="sxs-lookup"><span data-stu-id="52dd7-184">Record type</span></span> | <span data-ttu-id="52dd7-185">Host</span><span class="sxs-lookup"><span data-stu-id="52dd7-185">Host</span></span> | <span data-ttu-id="52dd7-186">Valeur</span><span class="sxs-lookup"><span data-stu-id="52dd7-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="52dd7-187">Un </span><span class="sxs-lookup"><span data-stu-id="52dd7-187">A</span></span> | `@` | <span data-ttu-id="52dd7-188">Adresse IP de [Copier l’adresse IP de l’application](#info)</span><span class="sxs-lookup"><span data-stu-id="52dd7-188">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="52dd7-189">TXT</span><span class="sxs-lookup"><span data-stu-id="52dd7-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="52dd7-190">Après avoir ajouté l’enregistrement CNAME, la page d’enregistrements DNS ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="52dd7-190">When the records are added, the DNS records page looks like the following example:</span></span>

![Page Enregistrements DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-the-a-record-mapping-in-the-app"></a><span data-ttu-id="52dd7-192">Activer le mappage d’enregistrement A dans l’application</span><span class="sxs-lookup"><span data-stu-id="52dd7-192">Enable the A record mapping in the app</span></span>

<span data-ttu-id="52dd7-193">De retour sur la page **Domaines personnalisés** de l’application dans le portail Azure, ajoutez à la liste le nom DNS personnalisé complet (par exemple, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="52dd7-193">Back in the app's **Custom domains** page in the Azure portal, add the fully qualified custom DNS name (for example, `contoso.com`) to the list.</span></span>

<span data-ttu-id="52dd7-194">Cliquez sur l’icône **+** en regard de **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-194">Select the **+** icon next to **Add hostname**.</span></span>

![Ajouter un nom d’hôte](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="52dd7-196">Tapez le nom de domaine complet pour lequel vous avez configuré l’enregistrement A, tel que `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="52dd7-196">Type the fully qualified domain name that you configured the A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="52dd7-197">Sélectionnez **Valider**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-197">Select **Validate**.</span></span>

<span data-ttu-id="52dd7-198">Le bouton **Ajouter un nom d’hôte** est activé.</span><span class="sxs-lookup"><span data-stu-id="52dd7-198">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="52dd7-199">Assurez-vous que **Type d’enregistrement du nom d’hôte** est défini sur **Enregistrement A (exemple.com)**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-199">Make sure that **Hostname record type** is set to **A record (example.com)**.</span></span>

<span data-ttu-id="52dd7-200">Sélectionnez **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-200">Select **Add hostname**.</span></span>

![Ajouter un nom DNS à l’application](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="52dd7-202">Un certain temps peut être nécessaire pour que le nouveau nom d’hôte soit reflété sur la page **Domaines personnalisés** de votre application.</span><span class="sxs-lookup"><span data-stu-id="52dd7-202">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="52dd7-203">Essayez d’actualiser le navigateur pour mettre à jour les données.</span><span class="sxs-lookup"><span data-stu-id="52dd7-203">Try refreshing the browser to update the data.</span></span>

![Enregistrement A ajouté](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="52dd7-205">Si vous avez raté une étape ou fait une faute de frappe à un endroit, une erreur de vérification peut apparaître au bas de la page.</span><span class="sxs-lookup"><span data-stu-id="52dd7-205">If you missed a step or made a typo somewhere earlier, you see a verification error at the bottom of the page.</span></span>

![Erreur de vérification](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="52dd7-207">Mapper un domaine générique</span><span class="sxs-lookup"><span data-stu-id="52dd7-207">Map a wildcard domain</span></span>

<span data-ttu-id="52dd7-208">Dans l’exemple du didacticiel, vous mappez un [nom DNS générique](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (par exemple, `*.contoso.com`) vers l’application App Service en ajoutant un enregistrement CNAME.</span><span class="sxs-lookup"><span data-stu-id="52dd7-208">In the tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) to the App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-the-cname-record"></a><span data-ttu-id="52dd7-209">Créer un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="52dd7-209">Create the CNAME record</span></span>

<span data-ttu-id="52dd7-210">Ajoutez un enregistrement CNAME pour mapper un nom générique au nom d’hôte par défaut de l’application (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="52dd7-210">Add a CNAME record to map a wildcard name to the app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="52dd7-211">Pour l’exemple de domaine `*.contoso.com`, l’enregistrement CNAME mappera le nom `*` à `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="52dd7-211">For the `*.contoso.com` domain example, the CNAME record will map the name `*` to `<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="52dd7-212">Après avoir ajouté l’enregistrement CNAME, la page d’enregistrements DNS ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="52dd7-212">When the CNAME is added, the DNS records page looks like the following example:</span></span>

![Navigation au sein du portail pour accéder à l’application Azure](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-the-cname-record-mapping-in-the-app"></a><span data-ttu-id="52dd7-214">Activer le mappage d’enregistrement CNAME dans l’application</span><span class="sxs-lookup"><span data-stu-id="52dd7-214">Enable the CNAME record mapping in the app</span></span>

<span data-ttu-id="52dd7-215">Vous pouvez maintenant ajouter à l’application un sous-domaine qui correspond au nom générique (par exemple, `sub1.contoso.com` et `sub2.contoso.com` correspond à `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="52dd7-215">You can now add any subdomain that matches the wildcard name to the app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="52dd7-216">Dans le volet de navigation gauche de la page d’application du portail Azure, sélectionnez **Domaines personnalisés**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-216">In the left navigation of the app page in the Azure portal, select **Custom domains**.</span></span> 

![Menu Domaines personnalisés](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="52dd7-218">Cliquez sur l’icône **+** en regard de **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-218">Select the **+** icon next to **Add hostname**.</span></span>

![Ajouter un nom d’hôte](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="52dd7-220">Tapez un nom de domaine complet qui correspond au domaine générique (par exemple, `sub1.contoso.com`), puis sélectionnez **Valider**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-220">Type a fully qualified domain name that matches the wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="52dd7-221">Le bouton **Ajouter un nom d’hôte** est activé.</span><span class="sxs-lookup"><span data-stu-id="52dd7-221">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="52dd7-222">Assurez-vous que le **Type d’enregistrement du nom d’hôte** est défini sur **Enregistrement CNAME (exemple.com ou tout sous-domaine)**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-222">Make sure that **Hostname record type** is set to **CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="52dd7-223">Sélectionnez **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="52dd7-223">Select **Add hostname**.</span></span>

![Ajouter un nom DNS à l’application](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="52dd7-225">Un certain temps peut être nécessaire pour que le nouveau nom d’hôte soit reflété sur la page **Domaines personnalisés** de votre application.</span><span class="sxs-lookup"><span data-stu-id="52dd7-225">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="52dd7-226">Essayez d’actualiser le navigateur pour mettre à jour les données.</span><span class="sxs-lookup"><span data-stu-id="52dd7-226">Try refreshing the browser to update the data.</span></span>

<span data-ttu-id="52dd7-227">Cliquez de nouveau sur l’icône **+** pour ajouter un autre nom d’hôte qui correspond au domaine générique.</span><span class="sxs-lookup"><span data-stu-id="52dd7-227">Select the **+** icon again to add another hostname that matches the wildcard domain.</span></span> <span data-ttu-id="52dd7-228">Par exemple, ajoutez `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="52dd7-228">For example, add `sub2.contoso.com`.</span></span>

![Enregistrement CNAME ajouté](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="52dd7-230">Test dans le navigateur</span><span class="sxs-lookup"><span data-stu-id="52dd7-230">Test in browser</span></span>

<span data-ttu-id="52dd7-231">Dans votre navigateur, accédez aux noms DNS que vous avez configurés précédemment (par exemple, `contoso.com`, `www.contoso.com`,`sub1.contoso.com` et `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="52dd7-231">Browse to the DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Navigation au sein du portail pour accéder à l’application Azure](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="52dd7-233">Automatiser des tâches à l’aide de scripts</span><span class="sxs-lookup"><span data-stu-id="52dd7-233">Automate with scripts</span></span>

<span data-ttu-id="52dd7-234">Vous pouvez automatiser la gestion des domaines personnalisés à l’aide de scripts, en utilisant [Azure CLI](/cli/azure/install-azure-cli) ou [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="52dd7-234">You can automate management of custom domains with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="52dd7-235">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="52dd7-235">Azure CLI</span></span> 

<span data-ttu-id="52dd7-236">La commande suivante ajoute un nom DNS personnalisé configuré à une application App Service.</span><span class="sxs-lookup"><span data-stu-id="52dd7-236">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="52dd7-237">Pour plus d’informations, consultez [Mapper un nom de domaine personnalisé à une application web](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="52dd7-237">For more information, see [Map a custom domain to a web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="52dd7-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="52dd7-238">Azure PowerShell</span></span> 

<span data-ttu-id="52dd7-239">La commande suivante ajoute un nom DNS personnalisé configuré à une application App Service.</span><span class="sxs-lookup"><span data-stu-id="52dd7-239">The following command adds a configured custom DNS name to an App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="52dd7-240">Pour plus d’informations, consultez [Attribuer un domaine personnalisé à une application web](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="52dd7-240">For more information, see [Assign a custom domain to a web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="52dd7-241">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="52dd7-241">Next steps</span></span>

<span data-ttu-id="52dd7-242">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="52dd7-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52dd7-243">Mapper un sous-domaine à l’aide d’un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="52dd7-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="52dd7-244">Mapper un domaine racine à l’aide d’un enregistrement A</span><span class="sxs-lookup"><span data-stu-id="52dd7-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="52dd7-245">Mapper un domaine générique à l’aide d’un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="52dd7-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="52dd7-246">Automatiser le mappage de domaine à l’aide de scripts</span><span class="sxs-lookup"><span data-stu-id="52dd7-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="52dd7-247">Passez au didacticiel suivant pour découvrir comment lier un certificat SSL personnalisé à une application web.</span><span class="sxs-lookup"><span data-stu-id="52dd7-247">Advance to the next tutorial to learn how to bind a custom SSL certificate to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52dd7-248">Lier un certificat SSL existant à des applications web Azure</span><span class="sxs-lookup"><span data-stu-id="52dd7-248">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
