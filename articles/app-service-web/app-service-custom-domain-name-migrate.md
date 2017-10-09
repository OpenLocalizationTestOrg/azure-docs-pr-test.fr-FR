---
title: "aaaMigrate un DNS active nom tooAzure du Service d’applications | Documents Microsoft"
description: "Découvrez comment toomigrate un nom de domaine DNS personnalisé qui est déjà affecté tooa live tooAzure de site du Service d’applications sans interruption de service."
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
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a><span data-ttu-id="374fc-103">Migrer un active tooAzure de nom DNS du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="374fc-103">Migrate an active DNS name tooAzure App Service</span></span>

<span data-ttu-id="374fc-104">Cet article explique comment toomigrate un DNS active Nom trop[Azure App Service](../app-service/app-service-value-prop-what-is.md) sans interruption de service.</span><span class="sxs-lookup"><span data-stu-id="374fc-104">This article shows you how toomigrate an active DNS name too[Azure App Service](../app-service/app-service-value-prop-what-is.md) without any downtime.</span></span>

<span data-ttu-id="374fc-105">Lorsque vous migrez un site actif et son tooApp de nom de domaine DNS Service, ce nom DNS sert déjà le trafic dynamique.</span><span class="sxs-lookup"><span data-stu-id="374fc-105">When you migrate a live site and its DNS domain name tooApp Service, that DNS name is already serving live traffic.</span></span> <span data-ttu-id="374fc-106">Vous pouvez éviter des temps d’arrêt dans la résolution DNS pendant la migration de hello en hello active DNS nom tooyour application de Service d’applications de liaison de manière préemptive.</span><span class="sxs-lookup"><span data-stu-id="374fc-106">You can avoid downtime in DNS resolution during hello migration by binding hello active DNS name tooyour App Service app preemptively.</span></span>

<span data-ttu-id="374fc-107">Si vous n’êtes pas inquiet de temps d’arrêt dans la résolution DNS, consultez [mapper un tooAzure de nom DNS personnalisé existant Web Apps](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="374fc-107">If you're not worried about downtime in DNS resolution, see [Map an existing custom DNS name tooAzure Web Apps](app-service-web-tutorial-custom-domain.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="374fc-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="374fc-108">Prerequisites</span></span>

<span data-ttu-id="374fc-109">toocomplete ce procédure :</span><span class="sxs-lookup"><span data-stu-id="374fc-109">toocomplete this how-to:</span></span>

- <span data-ttu-id="374fc-110">[Vérifiez que votre application App Service n’est pas au niveau Gratuit](app-service-web-tutorial-custom-domain.md#checkpricing).</span><span class="sxs-lookup"><span data-stu-id="374fc-110">[Make sure that your App Service app is not in FREE tier](app-service-web-tutorial-custom-domain.md#checkpricing).</span></span>

## <a name="bind-hello-domain-name-preemptively"></a><span data-ttu-id="374fc-111">Lier le nom de domaine hello manière préemptive</span><span class="sxs-lookup"><span data-stu-id="374fc-111">Bind hello domain name preemptively</span></span>

<span data-ttu-id="374fc-112">Lorsque vous liez un domaine personnalisé de manière préemptive, vous effectuez les deux suivantes hello avant d’apporter des modifications à vos enregistrements DNS :</span><span class="sxs-lookup"><span data-stu-id="374fc-112">When you bind a custom domain preemptively, you accomplish both of hello following before making any changes to your DNS records:</span></span>

- <span data-ttu-id="374fc-113">Vérifier la propriété du domaine</span><span class="sxs-lookup"><span data-stu-id="374fc-113">Verify domain ownership</span></span>
- <span data-ttu-id="374fc-114">Activer le nom de domaine hello pour votre application</span><span class="sxs-lookup"><span data-stu-id="374fc-114">Enable hello domain name for your app</span></span>

<span data-ttu-id="374fc-115">Lorsque vous migrez enfin votre nom DNS personnalisé à partir de hello ancien site toohello application de Service de l’application, il n’y aura aucun temps d’arrêt dans la résolution DNS.</span><span class="sxs-lookup"><span data-stu-id="374fc-115">When you finally migrate your custom DNS name from hello old site toohello App Service app, there will be no downtime in DNS resolution.</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a><span data-ttu-id="374fc-116">Créer un enregistrement de vérification de domaine</span><span class="sxs-lookup"><span data-stu-id="374fc-116">Create domain verification record</span></span>

<span data-ttu-id="374fc-117">la propriété du domaine tooverify, ajouter un TXT enregistrer.</span><span class="sxs-lookup"><span data-stu-id="374fc-117">tooverify domain ownership, Add a TXT record.</span></span> <span data-ttu-id="374fc-118">Hello enregistrement TXT est mappé à partir de _awverify.&lt; sous-domaine >_ too_&lt;appname >. azurewebsites.net_.</span><span class="sxs-lookup"><span data-stu-id="374fc-118">hello TXT record maps from _awverify.&lt;subdomain>_ too_&lt;appname>.azurewebsites.net_.</span></span> 

<span data-ttu-id="374fc-119">Hello enregistrement TXT que vous avez besoin dépend hello enregistrement DNS que vous souhaitez toomigrate.</span><span class="sxs-lookup"><span data-stu-id="374fc-119">hello TXT record you need depends on hello DNS record you want toomigrate.</span></span> <span data-ttu-id="374fc-120">Pour obtenir des exemples, consultez hello tableau suivant (`@` généralement représente hello domaine racine) :</span><span class="sxs-lookup"><span data-stu-id="374fc-120">For examples, see hello following table (`@` typically represents hello root domain):</span></span>  

| <span data-ttu-id="374fc-121">Exemple d’enregistrement DNS</span><span class="sxs-lookup"><span data-stu-id="374fc-121">DNS record example</span></span> | <span data-ttu-id="374fc-122">Hôte TXT</span><span class="sxs-lookup"><span data-stu-id="374fc-122">TXT Host</span></span> | <span data-ttu-id="374fc-123">Valeur TXT</span><span class="sxs-lookup"><span data-stu-id="374fc-123">TXT Value</span></span> |
| - | - | - |
| <span data-ttu-id="374fc-124">@ (racine)</span><span class="sxs-lookup"><span data-stu-id="374fc-124">@ (root)</span></span> | <span data-ttu-id="374fc-125">_awverify_</span><span class="sxs-lookup"><span data-stu-id="374fc-125">_awverify_</span></span> | <span data-ttu-id="374fc-126">_&lt;nomapplication&gt;.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="374fc-126">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="374fc-127">www (sous-domaine)</span><span class="sxs-lookup"><span data-stu-id="374fc-127">www (sub)</span></span> | <span data-ttu-id="374fc-128">_awverify.www_</span><span class="sxs-lookup"><span data-stu-id="374fc-128">_awverify.www_</span></span> | <span data-ttu-id="374fc-129">_&lt;nomapplication&gt;.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="374fc-129">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="374fc-130">\* (caractère générique)</span><span class="sxs-lookup"><span data-stu-id="374fc-130">\* (wildcard)</span></span> | <span data-ttu-id="374fc-131">_awverify.\*_</span><span class="sxs-lookup"><span data-stu-id="374fc-131">_awverify.\*_</span></span> | <span data-ttu-id="374fc-132">_&lt;nomapplication&gt;.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="374fc-132">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="374fc-133">Dans votre page d’enregistrements DNS, notez le type d’enregistrement de hello nom DNS que vous souhaitez toomigrate hello.</span><span class="sxs-lookup"><span data-stu-id="374fc-133">In your DNS records page, note hello record type of hello DNS name you want toomigrate.</span></span> <span data-ttu-id="374fc-134">App Service prend en charge les mappages d’enregistrements CNAME et A.</span><span class="sxs-lookup"><span data-stu-id="374fc-134">App Service supports mappings from CNAME and A records.</span></span>

### <a name="enable-hello-domain-for-your-app"></a><span data-ttu-id="374fc-135">Activer le domaine hello pour votre application</span><span class="sxs-lookup"><span data-stu-id="374fc-135">Enable hello domain for your app</span></span>

<span data-ttu-id="374fc-136">Bonjour [portail Azure](https://portal.azure.com)hello du volet de navigation gauche de la page de l’application hello, dans Sélectionnez **les domaines personnalisés**.</span><span class="sxs-lookup"><span data-stu-id="374fc-136">In hello [Azure portal](https://portal.azure.com), in hello left navigation of hello app page, select **Custom domains**.</span></span> 

![Menu Domaines personnalisés](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="374fc-138">Bonjour **les domaines personnalisés** page, sélectionnez hello  **+**  icône suivant trop**ajouter le nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="374fc-138">In hello **Custom domains** page, select hello **+** icon next too**Add hostname**.</span></span>

![Ajouter un nom d’hôte](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="374fc-140">Nom de domaine complet de hello type que vous avez ajouté enregistrement TXT de hello, tel que `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="374fc-140">Type hello fully qualified domain name that you added hello TXT record for, such as `www.contoso.com`.</span></span> <span data-ttu-id="374fc-141">Pour un domaine de caractère générique (comme \*. contoso.com), vous pouvez utiliser n’importe quel nom DNS qui correspond au domaine de caractère générique hello.</span><span class="sxs-lookup"><span data-stu-id="374fc-141">For a wildcard domain (like \*.contoso.com), you can use any DNS name that matches hello wildcard domain.</span></span> 

<span data-ttu-id="374fc-142">Sélectionnez **Valider**.</span><span class="sxs-lookup"><span data-stu-id="374fc-142">Select **Validate**.</span></span>

<span data-ttu-id="374fc-143">Hello **ajouter le nom d’hôte** bouton est activé.</span><span class="sxs-lookup"><span data-stu-id="374fc-143">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="374fc-144">Assurez-vous que **type d’enregistrement de nom d’hôte** a la valeur toohello type d’enregistrement DNS vous souhaitez toomigrate.</span><span class="sxs-lookup"><span data-stu-id="374fc-144">Make sure that **Hostname record type** is set toohello DNS record type you want toomigrate.</span></span>

<span data-ttu-id="374fc-145">Sélectionnez **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="374fc-145">Select **Add hostname**.</span></span>

![Ajouter une application de toohello nom DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="374fc-147">Il peut prendre un certain temps pour hello nouveau nom d’hôte toobe est répercutée dans l’application hello **les domaines personnalisés** page.</span><span class="sxs-lookup"><span data-stu-id="374fc-147">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="374fc-148">Essayez d’actualiser les données de salutation navigateur tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="374fc-148">Try refreshing hello browser tooupdate hello data.</span></span>

![Enregistrement CNAME ajouté](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="374fc-150">Votre nom DNS personnalisé est à présent activé dans votre application Azure.</span><span class="sxs-lookup"><span data-stu-id="374fc-150">Your custom DNS name is now enabled in your Azure app.</span></span> 

## <a name="remap-hello-active-dns-name"></a><span data-ttu-id="374fc-151">Remapper les nom DNS active hello</span><span class="sxs-lookup"><span data-stu-id="374fc-151">Remap hello active DNS name</span></span>

<span data-ttu-id="374fc-152">Hello chose uniquement les toodo gauche est le remappage votre tooApp de toopoint enregistrement DNS Service actif.</span><span class="sxs-lookup"><span data-stu-id="374fc-152">hello only thing left toodo is remapping your active DNS record toopoint tooApp Service.</span></span> <span data-ttu-id="374fc-153">Droit à présent, il continue de pointer tooyour ancien site.</span><span class="sxs-lookup"><span data-stu-id="374fc-153">Right now, it still points tooyour old site.</span></span>

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a><span data-ttu-id="374fc-154">Copiez l’adresse IP de l’application hello (enregistrement uniquement)</span><span class="sxs-lookup"><span data-stu-id="374fc-154">Copy hello app's IP address (A record only)</span></span>

<span data-ttu-id="374fc-155">Si vous remappez un enregistrement CNAME, ignorez cette section.</span><span class="sxs-lookup"><span data-stu-id="374fc-155">If you are remapping a CNAME record, skip this section.</span></span> 

<span data-ttu-id="374fc-156">tooremap un un enregistrement, vous avez besoin d’adresse IP externe de l’application de Service de l’application hello, qui est affichée dans hello **les domaines personnalisés** page.</span><span class="sxs-lookup"><span data-stu-id="374fc-156">tooremap an A record, you need hello App Service app's external IP address, which is shown in hello **Custom domains** page.</span></span>

<span data-ttu-id="374fc-157">Fermer hello **ajouter le nom d’hôte** page en sélectionnant **X** dans le coin supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="374fc-157">Close hello **Add hostname** page by selecting **X** in hello upper-right corner.</span></span> 

<span data-ttu-id="374fc-158">Bonjour **les domaines personnalisés** page, copiez l’adresse IP de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="374fc-158">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a><span data-ttu-id="374fc-160">Mettre à jour un enregistrement DNS hello</span><span class="sxs-lookup"><span data-stu-id="374fc-160">Update hello DNS record</span></span>

<span data-ttu-id="374fc-161">Dans la page d’enregistrements hello DNS de votre fournisseur de domaine, sélectionnez tooremap enregistrement DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="374fc-161">Back in hello DNS records page of your domain provider, select hello DNS record tooremap.</span></span>

<span data-ttu-id="374fc-162">Pourquoi `contoso.com` racine d’exemple de domaine, de remapper l’enregistrement A ou CNAME de hello comme exemples hello Bonjour tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="374fc-162">For hello `contoso.com` root domain example, remap hello A or CNAME record like hello examples in hello following table:</span></span> 

| <span data-ttu-id="374fc-163">Exemple de nom de domaine complet</span><span class="sxs-lookup"><span data-stu-id="374fc-163">FQDN example</span></span> | <span data-ttu-id="374fc-164">Type d’enregistrement</span><span class="sxs-lookup"><span data-stu-id="374fc-164">Record type</span></span> | <span data-ttu-id="374fc-165">Host</span><span class="sxs-lookup"><span data-stu-id="374fc-165">Host</span></span> | <span data-ttu-id="374fc-166">Valeur</span><span class="sxs-lookup"><span data-stu-id="374fc-166">Value</span></span> |
| - | - | - | - |
| <span data-ttu-id="374fc-167">contoso.com (racine)</span><span class="sxs-lookup"><span data-stu-id="374fc-167">contoso.com (root)</span></span> | <span data-ttu-id="374fc-168">A</span><span class="sxs-lookup"><span data-stu-id="374fc-168">A</span></span> | `@` | <span data-ttu-id="374fc-169">Adresse IP à partir de [adresse IP de l’application hello de copie](#info)</span><span class="sxs-lookup"><span data-stu-id="374fc-169">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="374fc-170">www.contoso.com (sous-domaine)</span><span class="sxs-lookup"><span data-stu-id="374fc-170">www.contoso.com (sub)</span></span> | <span data-ttu-id="374fc-171">CNAME</span><span class="sxs-lookup"><span data-stu-id="374fc-171">CNAME</span></span> | `www` | <span data-ttu-id="374fc-172">_&lt;nomapplication&gt;.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="374fc-172">_&lt;appname>.azurewebsites.net_</span></span> |
| <span data-ttu-id="374fc-173">\*.contoso.com (caractère générique)</span><span class="sxs-lookup"><span data-stu-id="374fc-173">\*.contoso.com (wildcard)</span></span> | <span data-ttu-id="374fc-174">CNAME</span><span class="sxs-lookup"><span data-stu-id="374fc-174">CNAME</span></span> | _\*_ | <span data-ttu-id="374fc-175">_&lt;nomapplication&gt;.azurewebsites.net_</span><span class="sxs-lookup"><span data-stu-id="374fc-175">_&lt;appname>.azurewebsites.net_</span></span> |

<span data-ttu-id="374fc-176">Enregistrez vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="374fc-176">Save your settings.</span></span>

<span data-ttu-id="374fc-177">Requêtes DNS doivent commencer à résoudre les tooyour application de Service de l’application immédiatement après que la propagation DNS se produit.</span><span class="sxs-lookup"><span data-stu-id="374fc-177">DNS queries should start resolving tooyour App Service app immediately after DNS propagation happens.</span></span>

## <a name="next-steps"></a><span data-ttu-id="374fc-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="374fc-178">Next steps</span></span>

<span data-ttu-id="374fc-179">Découvrez comment toobind une SSL personnalisée certificat tooApp Service.</span><span class="sxs-lookup"><span data-stu-id="374fc-179">Learn how toobind a custom SSL certificate tooApp Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="374fc-180">Lier un tooAzure de certificat SSL personnalisé existant Web Apps</span><span class="sxs-lookup"><span data-stu-id="374fc-180">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
