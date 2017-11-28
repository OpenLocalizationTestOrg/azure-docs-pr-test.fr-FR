---
title: Migrer un Nom DNS actif vers Azure App Service | Microsoft Docs
description: "Découvrez comment migrer sans temps d’arrêt vers Azure App Service un nom de domaine personnalisé déjà affecté à un site actif."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: 89308c1c684a639950467b72d26703cc07c50c14
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-an-active-dns-name-to-azure-app-service"></a><span data-ttu-id="7e5ca-103">Migrer un nom DNS actif vers Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7e5ca-103">Migrate an active DNS name to Azure App Service</span></span>

<span data-ttu-id="7e5ca-104">Cet article montre comment migrer un nom DNS actif vers [Azure App Service](../app-service/app-service-value-prop-what-is.md) sans temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-104">This article shows you how to migrate an active DNS name to [Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="7e5ca-105">Lorsque vous migrez un site actif et son nom de domaine DNS vers App Service, ce nom DNS sert déjà un trafic actif.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-105">When you migrate a live site and its DNS domain name to App Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="7e5ca-106">Vous pouvez éviter tout temps d’arrêt dans la résolution DNS lors de la migration en liant à l’avance le nom DNS actif à votre application App Service.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-106">You can avoid downtime in DNS resolution during the migration by binding the active DNS name to your App Service app preemptively.</span></span>

<span data-ttu-id="7e5ca-107">Si vous ne vous inquiétez pas des temps d’arrêt durant la résolution DNS, voir [Mapper un nom DNS personnalisé existant vers Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="7e5ca-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name to Azure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e5ca-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7e5ca-108">Prerequisites</span></span>

<span data-ttu-id="7e5ca-109">Pour suivre cette procédure :</span><span class="sxs-lookup"><span data-stu-id="7e5ca-109">To complete this how-to:</span></span>

- <span data-ttu-id="7e5ca-110">[Vérifiez que votre application App Service n’est pas au niveau Gratuit](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="7e5ca-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-the-domain-name-preemptively"></a><span data-ttu-id="7e5ca-111">Lier le nom de domaine de manière préemptive</span><span class="sxs-lookup"><span data-stu-id="7e5ca-111">Bind the domain name preemptively</span></span>

<span data-ttu-id="7e5ca-112">Lorsque vous liez un domaine personnalisé de manière préemptive, vous effectuez les deux opérations suivantes avant d’apporter des modifications à vos enregistrements DNS :</span><span class="sxs-lookup"><span data-stu-id="7e5ca-112">When you bind a custom domain preemptively, you accomplish both of the following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="7e5ca-113">Vérifier la propriété du domaine</span><span class="sxs-lookup"><span data-stu-id="7e5ca-113">Verify domain ownership</span></span>
- <span data-ttu-id="7e5ca-114">Activer le nom de domaine de votre application</span><span class="sxs-lookup"><span data-stu-id="7e5ca-114">Enable the domain name for your app</span></span>

<span data-ttu-id="7e5ca-115">Lorsque vous migrez finalement votre nom DNS personnalisé de l’ancien site à l’application App Service, il n’y a aucun temps d’arrêt durant la résolution DNS.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-115">When you finally migrate your custom DNS name from the old site to the App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="7e5ca-116">Créer un enregistrement de vérification de domaine</span><span class="sxs-lookup"><span data-stu-id="7e5ca-116">Create domain verification record</span></span>

<span data-ttu-id="7e5ca-117">Pour vérifier la propriété du domaine, ajoutez un enregistrement TXT.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-117">To verify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="7e5ca-118">L’enregistrement TXT mappe de _awverify.&lt;sousdomaine>_ à _&lt;nomapplication>.azurewebsites.net_.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-118">The TXT record maps from _awverify.&lt;subdomain>_ to _&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="7e5ca-119">L’enregistrement TXT dont vous avez besoin dépend de l’enregistrement DNS que vous souhaitez migrer.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-119">The TXT record you need depends on the DNS record you want to migrate.</span></span> <span data-ttu-id="7e5ca-120">Pour des exemples, consultez le tableau suivant (`@` représente généralement le domaine racine) :</span><span class="sxs-lookup"><span data-stu-id="7e5ca-120">For examples, see the following table (`@` typically represents the root domain):</span></span>  

| <span data-ttu-id="7e5ca-121">Exemple d’enregistrement DNS</span><span class="sxs-lookup"><span data-stu-id="7e5ca-121">DNS record example</span></span> | <span data-ttu-id="7e5ca-122">Hôte TXT</span><span class="sxs-lookup"><span data-stu-id="7e5ca-122">TXT Host</span></span> | <span data-ttu-id="7e5ca-123">Valeur TXT</span><span class="sxs-lookup"><span data-stu-id="7e5ca-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="7e5ca-124">@ (racine)</span><span class="sxs-lookup"><span data-stu-id="7e5ca-124">@ (root)</span></span> | <span data-ttu-id="7e5ca-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="7e5ca-125">_awverify_</span></span> | <span data-ttu-id="7e5ca-126">_&lt;nomapplication>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="7e5ca-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="7e5ca-127">www (sous-domaine)</span><span class="sxs-lookup"><span data-stu-id="7e5ca-127">www (sub)</span></span> | <span data-ttu-id="7e5ca-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="7e5ca-128">_awverify.www_</span></span> | <span data-ttu-id="7e5ca-129">_&lt;nomapplication>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="7e5ca-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="7e5ca-130">\* (caractère générique)</span><span class="sxs-lookup"><span data-stu-id="7e5ca-130">\* (wildcard)</span></span> | <span data-ttu-id="7e5ca-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="7e5ca-131">_awverify.\*_</span></span> | <span data-ttu-id="7e5ca-132">_&lt;nomapplication>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="7e5ca-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="7e5ca-133">Dans la page des enregistrements DNS, notez le type d’enregistrement du nom DNS que vous souhaitez migrer.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-133">In your DNS records page, note the record type of the DNS name you want to migrate.</span></span> <span data-ttu-id="7e5ca-134">App Service prend en charge les mappages d’enregistrements CNAME et A.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-the-domain-for-your-app"></a><span data-ttu-id="7e5ca-135">Activer le domaine pour votre application</span><span class="sxs-lookup"><span data-stu-id="7e5ca-135">Enable the domain for your app</span></span>

<span data-ttu-id="7e5ca-136">Dans le [portail Azure](https://portal.azure.com), dans le volet de navigation gauche de la page de l’application, sélectionnez **Domaines personnalisés**.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-136">In the [Azure portal](https://portal.azure.com), in the left navigation of the app page, select **Custom domains**.</span></span> 

![Menu Domaines personnalisés](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="7e5ca-138">Dans la page **Domaines personnalisés**, sélectionnez l’icône **+** en regard de **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-138">In the **Custom domains** page, select the **+** icon next to **Add hostname**.</span></span>

![Ajouter un nom d’hôte](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="7e5ca-140">Tapez le nom de domaine complet (FQDN) pour lequel vous avez ajouté l’enregistrement TXT, tel que `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-140">Type the fully qualified domain name that you added the TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="7e5ca-141">Pour un domaine contenant un caractère générique (tel que \*. contoso.com), vous pouvez utiliser n’importe quel nom DNS correspondant à ce domaine contenant un caractère générique.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches the wildcard domain.</span></span> 

<span data-ttu-id="7e5ca-142">Sélectionnez **Valider**.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-142">Select **Validate**.</span></span>

<span data-ttu-id="7e5ca-143">Le bouton **Ajouter un nom d’hôte** est activé.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-143">The **Add hostname** button is activated.</span></span> 

<span data-ttu-id="7e5ca-144">Assurez-vous que l’option **Type d’enregistrement du nom d’hôte** est bien définie sur le type d’enregistrement DNS que vous voulez migrer.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-144">Make sure that **Hostname record type** is set to the DNS record type you want to migrate.</span></span>

<span data-ttu-id="7e5ca-145">Sélectionnez **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-145">Select **Add hostname**.</span></span>

![Ajouter un nom DNS à l’application](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="7e5ca-147">Un certain temps peut être nécessaire pour que le nouveau nom d’hôte soit reflété sur la page **Domaines personnalisés** de votre application.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-147">It might take some time for the new hostname to be reflected in the app's **Custom domains** page.</span></span> <span data-ttu-id="7e5ca-148">Essayez d’actualiser le navigateur pour mettre à jour les données.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-148">Try refreshing the browser to update the data.</span></span>

![Enregistrement CNAME ajouté](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="7e5ca-150">Votre nom DNS personnalisé est à présent activé dans votre application Azure.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-the-active-dns-name"></a><span data-ttu-id="7e5ca-151">Remapper le nom DNS actif</span><span class="sxs-lookup"><span data-stu-id="7e5ca-151">Remap the active DNS name</span></span>

<span data-ttu-id="7e5ca-152">Il ne vous reste plus qu’à remapper votre enregistrement DNS actif pour qu’il pointe vers App Service.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-152">The only thing left to do is remapping your active DNS record to point to App Service.</span></span> <span data-ttu-id="7e5ca-153">En ce moment précis, il pointe encore sur votre ancien site.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-153">Right now, it still points to your old site.</span></span>

<a name="info"></a>

### <a name="copy-the-apps-ip-address-a-record-only"></a><span data-ttu-id="7e5ca-154">Copier l’adresse IP de l’application (un enregistrement uniquement)</span><span class="sxs-lookup"><span data-stu-id="7e5ca-154">Copy the app's IP address (A record only)</span></span>

<span data-ttu-id="7e5ca-155">Si vous remappez un enregistrement CNAME, ignorez cette section.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="7e5ca-156">Pour remapper un enregistrement A, vous avez besoin de l’adresse IP externe de l’application App Service. Celle-ci est affichée dans la page **Domaines personnalisés**.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-156">To remap an A record, you need the App Service app's external IP address, which is shown in the **Custom domains** page.</span></span>

<span data-ttu-id="7e5ca-157">Fermez la page **Ajouter un nom d’hôte** en sélectionnant **X** dans l’angle supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-157">Close the **Add hostname** page by selecting **X** in the upper-right corner.</span></span> 

<span data-ttu-id="7e5ca-158">Dans la page **Domaines personnalisés**, copiez l’adresse IP de l’application.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-158">In the **Custom domains** page, copy the app's IP address.</span></span>

![Navigation au sein du portail pour accéder à l’application Azure](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-the-dns-record"></a><span data-ttu-id="7e5ca-160">Mettre à jour l’enregistrement DNS</span><span class="sxs-lookup"><span data-stu-id="7e5ca-160">Update the DNS record</span></span>

<span data-ttu-id="7e5ca-161">Dans la page des enregistrements DNS de votre fournisseur de domaine, sélectionnez l’enregistrement DNS à remapper.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-161">Back in the DNS records page of your domain provider, select the DNS record to remap.</span></span>

<span data-ttu-id="7e5ca-162">Pour l’exemple de domaine racine `contoso.com`, remappez l’enregistrement A ou CNAME, comme dans les exemples fournis dans le tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="7e5ca-162">For the `contoso.com` root domain example, remap the A or CNAME record like the examples in the following table:</span></span> 

| <span data-ttu-id="7e5ca-163">Exemple de nom de domaine complet</span><span class="sxs-lookup"><span data-stu-id="7e5ca-163">FQDN example</span></span> | <span data-ttu-id="7e5ca-164">Type d’enregistrement</span><span class="sxs-lookup"><span data-stu-id="7e5ca-164">Record type</span></span> | <span data-ttu-id="7e5ca-165">Host</span><span class="sxs-lookup"><span data-stu-id="7e5ca-165">Host</span></span> | <span data-ttu-id="7e5ca-166">Valeur</span><span class="sxs-lookup"><span data-stu-id="7e5ca-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="7e5ca-167">contoso.com (racine)</span><span class="sxs-lookup"><span data-stu-id="7e5ca-167">contoso.com (root)</span></span> | <span data-ttu-id="7e5ca-168">A</span><span class="sxs-lookup"><span data-stu-id="7e5ca-168">A</span></span> | `@` | <span data-ttu-id="7e5ca-169">Adresse IP de [Copier l’adresse IP de l’application](#info)</span><span class="sxs-lookup"><span data-stu-id="7e5ca-169">IP address from [Copy the app's IP address](#info)</span></span> |
| <span data-ttu-id="7e5ca-170">www.contoso.com (sous-domaine)</span><span class="sxs-lookup"><span data-stu-id="7e5ca-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="7e5ca-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="7e5ca-171">CNAME</span></span> | `www` | <span data-ttu-id="7e5ca-172">_&lt;nomapplication>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="7e5ca-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="7e5ca-173">\*.contoso.com (caractère générique)</span><span class="sxs-lookup"><span data-stu-id="7e5ca-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="7e5ca-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="7e5ca-174">CNAME</span></span> | _\*_ | <span data-ttu-id="7e5ca-175">_&lt;nomapplication>.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="7e5ca-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="7e5ca-176">Enregistrez vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-176">Save your settings.</span></span>

<span data-ttu-id="7e5ca-177">Les requêtes DNS doivent commencer à trouver votre application App Service immédiatement après la propagation DNS.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-177">DNS queries should start resolving to your App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e5ca-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7e5ca-178">Next steps</span></span>

<span data-ttu-id="7e5ca-179">Découvrez comment lier un certificat SSL personnalisé à App Service.</span><span class="sxs-lookup"><span data-stu-id="7e5ca-179">Learn how to bind a custom SSL certificate to App Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7e5ca-180">Lier un certificat SSL existant à des applications web Azure</span><span class="sxs-lookup"><span data-stu-id="7e5ca-180">Bind an existing custom SSL certificate to Azure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
