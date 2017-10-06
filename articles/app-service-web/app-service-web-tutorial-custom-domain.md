---
title: "aaaMap un DNS personnalisé existant nom tooAzure Web Apps | Documents Microsoft"
description: "Découvrez comment tooadd un domaine DNS personnalisé existant nom d’application web de tooa (domaine personnel), serveur principal d’application mobile ou application API dans Azure App Service."
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
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a><span data-ttu-id="44d75-103">Mapper une tooAzure de nom DNS personnalisé existant Web Apps</span><span class="sxs-lookup"><span data-stu-id="44d75-103">Map an existing custom DNS name tooAzure Web Apps</span></span>

<span data-ttu-id="44d75-104">[Azure Web Apps](app-service-web-overview.md) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="44d75-104">[Azure Web Apps](app-service-web-overview.md) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="44d75-105">Ce didacticiel vous montre comment toomap un DNS personnalisé existant nom tooAzure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="44d75-105">This tutorial shows you how toomap an existing custom DNS name tooAzure Web Apps.</span></span>

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

<span data-ttu-id="44d75-107">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="44d75-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="44d75-108">Mapper un sous-domaine (par exemple, `www.contoso.com`) à l’aide d’un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="44d75-108">Map a subdomain (for example, `www.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="44d75-109">Mapper un domaine racine (par exemple, `contoso.com`) à l’aide d’un enregistrement A</span><span class="sxs-lookup"><span data-stu-id="44d75-109">Map a root domain (for example, `contoso.com`) by using an A record</span></span>
> * <span data-ttu-id="44d75-110">Mapper un domaine générique (par exemple, `*.contoso.com`) à l’aide d’un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="44d75-110">Map a wildcard domain (for example, `*.contoso.com`) by using a CNAME record</span></span>
> * <span data-ttu-id="44d75-111">Automatiser le mappage de domaine à l’aide de scripts</span><span class="sxs-lookup"><span data-stu-id="44d75-111">Automate domain mapping with scripts</span></span>

<span data-ttu-id="44d75-112">Vous pouvez utiliser un **enregistrement CNAME** ou **un enregistrement** toomap DNS personnalisé nom tooApp Service.</span><span class="sxs-lookup"><span data-stu-id="44d75-112">You can use either a **CNAME record** or an **A record** toomap a custom DNS name tooApp Service.</span></span> 

> [!NOTE]
> <span data-ttu-id="44d75-113">Nous vous recommandons d’utiliser un enregistrement CNAME pour tous les noms DNS personnalisés, à l’exception d’un domaine racine (par exemple, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="44d75-113">We recommend that you use a CNAME for all custom DNS names except a root domain (for example, `contoso.com`).</span></span>

<span data-ttu-id="44d75-114">toomigrate un site actif et son tooApp de nom de domaine DNS Service, consultez [migrer une tooAzure de nom DNS du Service d’applications active](app-service-custom-domain-name-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="44d75-114">toomigrate a live site and its DNS domain name tooApp Service, see [Migrate an active DNS name tooAzure App Service](app-service-custom-domain-name-migrate.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44d75-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="44d75-115">Prerequisites</span></span>

<span data-ttu-id="44d75-116">toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="44d75-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="44d75-117">[Créez une application App Service](/azure/app-service/), ou utilisez une application créée pour un autre didacticiel.</span><span class="sxs-lookup"><span data-stu-id="44d75-117">[Create an App Service app](/azure/app-service/), or use an app that you created for another tutorial.</span></span>
* <span data-ttu-id="44d75-118">Acheter un nom de domaine et assurez-vous que vous disposez du Registre de l’accès toohello DNS de votre fournisseur de domaine (par exemple, GoDaddy).</span><span class="sxs-lookup"><span data-stu-id="44d75-118">Purchase a domain name and make sure you have access toohello DNS registry for your domain provider (such as GoDaddy).</span></span>

  <span data-ttu-id="44d75-119">Par exemple, les entrées DNS tooadd pour `contoso.com` et `www.contoso.com`, vous devez être en mesure de tooconfigure paramètres de DNS hello pour hello `contoso.com` domaine racine.</span><span class="sxs-lookup"><span data-stu-id="44d75-119">For example, tooadd DNS entries for `contoso.com` and `www.contoso.com`, you must be able tooconfigure hello DNS settings for hello `contoso.com` root domain.</span></span>

  > [!NOTE]
  > <span data-ttu-id="44d75-120">Si vous n’avez un domaine existant nom, envisagez de [achat d’un domaine à l’aide de hello Azure portal](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="44d75-120">If you don't have an existing domain name, consider [purchasing a domain using hello Azure portal](custom-dns-web-site-buydomains-web-app.md).</span></span> 

## <a name="prepare-hello-app"></a><span data-ttu-id="44d75-121">Préparer l’application hello</span><span class="sxs-lookup"><span data-stu-id="44d75-121">Prepare hello app</span></span>

<span data-ttu-id="44d75-122">toomap une personnalisé DNS nom tooa l’application web, l’application web hello [plan App Service](https://azure.microsoft.com/pricing/details/app-service/) doit être un niveau payant (**Shared**, **base**, **Standard**, ou  **Premium**).</span><span class="sxs-lookup"><span data-stu-id="44d75-122">toomap a custom DNS name tooa web app, hello web app's [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be a paid tier (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> <span data-ttu-id="44d75-123">Dans cette étape, vous vérifiez que ce Service d’applications app est Bonjour hello pris en charge le niveau de tarification.</span><span class="sxs-lookup"><span data-stu-id="44d75-123">In this step, you make sure that hello App Service app is in hello supported pricing tier.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="44d75-124">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="44d75-124">Sign in tooAzure</span></span>

<span data-ttu-id="44d75-125">Ouvrez hello [portail Azure](https://portal.azure.com) et connectez-vous avec votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="44d75-125">Open hello [Azure portal](https://portal.azure.com) and sign in with your Azure account.</span></span>

### <a name="navigate-toohello-app-in-hello-azure-portal"></a><span data-ttu-id="44d75-126">Accédez application toohello Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="44d75-126">Navigate toohello app in hello Azure portal</span></span>

<span data-ttu-id="44d75-127">Dans le menu de gauche hello, sélectionnez **des Services d’application**, puis sélectionnez le nom hello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="44d75-127">From hello left menu, select **App Services**, and then select hello name of hello app.</span></span>

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/select-app.png)

<span data-ttu-id="44d75-129">Page de gestion hello Hello application de Service de l’application s’affiche.</span><span class="sxs-lookup"><span data-stu-id="44d75-129">You see hello management page of hello App Service app.</span></span>  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="44d75-130">Vérifier le niveau tarifaire de hello</span><span class="sxs-lookup"><span data-stu-id="44d75-130">Check hello pricing tier</span></span>

<span data-ttu-id="44d75-131">Bonjour barre de navigation de page de l’application hello gauche, faites défiler toohello **paramètres** section et sélectionnez **montée en puissance (plan App Service)**.</span><span class="sxs-lookup"><span data-stu-id="44d75-131">In hello left navigation of hello app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu Monter en puissance](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

<span data-ttu-id="44d75-133">niveau actuel de l’application Hello est mis en surbrillance d’une bordure bleue.</span><span class="sxs-lookup"><span data-stu-id="44d75-133">hello app's current tier is highlighted by a blue border.</span></span> <span data-ttu-id="44d75-134">Vérifiez que cette application hello n’est pas hello de toomake **libre** couche.</span><span class="sxs-lookup"><span data-stu-id="44d75-134">Check toomake sure that hello app is not in hello **Free** tier.</span></span> <span data-ttu-id="44d75-135">DNS personnalisé n’est pas pris en charge dans hello **libre** couche.</span><span class="sxs-lookup"><span data-stu-id="44d75-135">Custom DNS is not supported in hello **Free** tier.</span></span> 

![Vérification du niveau de tarification](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

<span data-ttu-id="44d75-137">Si hello plan App Service n’est pas **libre**, fermez hello **choisir votre niveau tarifaire** page et ignorer trop[mapper un enregistrement CNAME](#cname).</span><span class="sxs-lookup"><span data-stu-id="44d75-137">If hello App Service plan is not **Free**, close hello **Choose your pricing tier** page and skip too[Map a CNAME record](#cname).</span></span>

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a><span data-ttu-id="44d75-138">Montée en puissance hello plan App Service</span><span class="sxs-lookup"><span data-stu-id="44d75-138">Scale up hello App Service plan</span></span>

<span data-ttu-id="44d75-139">Sélectionnez un des niveaux de hello occupé (**Shared**, **base**, **Standard**, ou **Premium**).</span><span class="sxs-lookup"><span data-stu-id="44d75-139">Select any of hello non-free tiers (**Shared**, **Basic**, **Standard**, or **Premium**).</span></span> 

<span data-ttu-id="44d75-140">Cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="44d75-140">Click **Select**.</span></span>

![Vérification du niveau de tarification](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

<span data-ttu-id="44d75-142">Lorsque vous voyez hello suivant la notification, l’opération de mise à l’échelle de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="44d75-142">When you see hello following notification, hello scale operation is complete.</span></span>

![Confirmation d’opération de mise à l’échelle](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a><span data-ttu-id="44d75-144">Mapper un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="44d75-144">Map a CNAME record</span></span>

<span data-ttu-id="44d75-145">Dans l’exemple de didacticiel hello, vous ajoutez un enregistrement CNAME pour hello `www` sous-domaine (par exemple, `www.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="44d75-145">In hello tutorial example, you add a CNAME record for hello `www` subdomain (for example, `www.contoso.com`).</span></span>

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="44d75-146">Créer l’enregistrement CNAME de hello</span><span class="sxs-lookup"><span data-stu-id="44d75-146">Create hello CNAME record</span></span>

<span data-ttu-id="44d75-147">Ajouter un toomap enregistrement CNAME nom d’hôte par défaut de l’application de toohello un sous-domaine (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="44d75-147">Add a CNAME record toomap a subdomain toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="44d75-148">Pourquoi `www.contoso.com` exemple de domaine, ajoutez un enregistrement CNAME qui mappe le nom hello `www` trop`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="44d75-148">For hello `www.contoso.com` domain example, add a CNAME record that maps hello name `www` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="44d75-149">Après avoir ajouté hello CNAME, page d’enregistrements DNS hello ressemble hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="44d75-149">After you add hello CNAME, hello DNS records page looks like hello following example:</span></span>

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a><span data-ttu-id="44d75-151">Activer le mappage d’enregistrement CNAME hello dans Azure</span><span class="sxs-lookup"><span data-stu-id="44d75-151">Enable hello CNAME record mapping in Azure</span></span>

<span data-ttu-id="44d75-152">Bonjour gauche de navigation de page de l’application hello Bonjour portail Azure, sélectionnez **les domaines personnalisés**.</span><span class="sxs-lookup"><span data-stu-id="44d75-152">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menu Domaines personnalisés](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="44d75-154">Bonjour **les domaines personnalisés** page de l’application hello, ajoutez hello complet nom DNS personnalisé (`www.contoso.com`) toohello liste.</span><span class="sxs-lookup"><span data-stu-id="44d75-154">In hello **Custom domains** page of hello app, add hello fully qualified custom DNS name (`www.contoso.com`) toohello list.</span></span>

<span data-ttu-id="44d75-155">Sélectionnez hello  **+**  icône suivant trop**ajouter le nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="44d75-155">Select hello **+** icon next too**Add hostname**.</span></span>

![Ajouter un nom d’hôte](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="44d75-157">Nom de domaine complet de hello type que vous avez ajouté un enregistrement CNAME pour, tel que `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="44d75-157">Type hello fully qualified domain name that you added a CNAME record for, such as `www.contoso.com`.</span></span> 

<span data-ttu-id="44d75-158">Sélectionnez **Valider**.</span><span class="sxs-lookup"><span data-stu-id="44d75-158">Select **Validate**.</span></span>

<span data-ttu-id="44d75-159">Hello **ajouter le nom d’hôte** bouton est activé.</span><span class="sxs-lookup"><span data-stu-id="44d75-159">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="44d75-160">Assurez-vous que **type d’enregistrement de nom d’hôte** est défini trop**CNAME (www.example.com ou tout sous-domaine)**.</span><span class="sxs-lookup"><span data-stu-id="44d75-160">Make sure that **Hostname record type** is set too**CNAME (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="44d75-161">Sélectionnez **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="44d75-161">Select **Add hostname**.</span></span>

![Ajouter une application de toohello nom DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

<span data-ttu-id="44d75-163">Il peut prendre un certain temps pour hello nouveau nom d’hôte toobe est répercutée dans l’application hello **les domaines personnalisés** page.</span><span class="sxs-lookup"><span data-stu-id="44d75-163">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="44d75-164">Essayez d’actualiser les données de salutation navigateur tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="44d75-164">Try refreshing hello browser tooupdate hello data.</span></span>

![Enregistrement CNAME ajouté](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

<span data-ttu-id="44d75-166">Si vous manqué une étape ou que vous faites une faute de frappe quelque part précédemment, vous voyez une erreur de vérification bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="44d75-166">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Erreur de vérification](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a><span data-ttu-id="44d75-168">Mapper un enregistrement A</span><span class="sxs-lookup"><span data-stu-id="44d75-168">Map an A record</span></span>

<span data-ttu-id="44d75-169">Dans l’exemple de didacticiel hello, vous ajoutez un enregistrement A pour le domaine racine de hello (par exemple, `contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="44d75-169">In hello tutorial example, you add an A record for hello root domain (for example, `contoso.com`).</span></span> 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a><span data-ttu-id="44d75-170">Copiez l’adresse IP de l’application hello</span><span class="sxs-lookup"><span data-stu-id="44d75-170">Copy hello app's IP address</span></span>

<span data-ttu-id="44d75-171">toomap un un enregistrement, vous devez adresse IP externe de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="44d75-171">toomap an A record, you need hello app's external IP address.</span></span> <span data-ttu-id="44d75-172">Vous pouvez trouver cette adresse IP de l’application hello **les domaines personnalisés** page Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="44d75-172">You can find this IP address in hello app's **Custom domains** page in hello Azure portal.</span></span>

<span data-ttu-id="44d75-173">Bonjour gauche de navigation de page de l’application hello Bonjour portail Azure, sélectionnez **les domaines personnalisés**.</span><span class="sxs-lookup"><span data-stu-id="44d75-173">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menu Domaines personnalisés](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="44d75-175">Bonjour **les domaines personnalisés** page, copiez l’adresse IP de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="44d75-175">In hello **Custom domains** page, copy hello app's IP address.</span></span>

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a><span data-ttu-id="44d75-177">Créer l’enregistrement A de hello</span><span class="sxs-lookup"><span data-stu-id="44d75-177">Create hello A record</span></span>

<span data-ttu-id="44d75-178">requiert l’application Service toomap un un enregistrement tooan application, **deux** enregistrements DNS :</span><span class="sxs-lookup"><span data-stu-id="44d75-178">toomap an A record tooan app, App Service requires **two** DNS records:</span></span>

- <span data-ttu-id="44d75-179">Un **A** enregistrer l’adresse IP de l’application toomap toohello.</span><span class="sxs-lookup"><span data-stu-id="44d75-179">An **A** record toomap toohello app's IP address.</span></span>
- <span data-ttu-id="44d75-180">A **TXT** enregistrer le nom d’hôte par défaut de l’application toomap toohello `<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="44d75-180">A **TXT** record toomap toohello app's default hostname `<app_name>.azurewebsites.net`.</span></span> <span data-ttu-id="44d75-181">Service d’applications utilise cet enregistrement uniquement au moment de la configuration, tooverify que vous possédez le domaine personnalisé de hello.</span><span class="sxs-lookup"><span data-stu-id="44d75-181">App Service uses this record only at configuration time, tooverify that you own hello custom domain.</span></span> <span data-ttu-id="44d75-182">Une fois votre domaine personnalisé validé et configuré dans App Service, vous pourrez supprimer cet enregistrement TXT.</span><span class="sxs-lookup"><span data-stu-id="44d75-182">After your custom domain is validated and configured in App Service, you can delete this TXT record.</span></span> 

<span data-ttu-id="44d75-183">Pourquoi `contoso.com` exemple de domaine, créer des enregistrements A et TXT hello selon toohello tableau suivant (`@` généralement représente hello domaine racine).</span><span class="sxs-lookup"><span data-stu-id="44d75-183">For hello `contoso.com` domain example, create hello A and TXT records according toohello following table (`@` typically represents hello root domain).</span></span> 

| <span data-ttu-id="44d75-184">Type d’enregistrement</span><span class="sxs-lookup"><span data-stu-id="44d75-184">Record type</span></span> | <span data-ttu-id="44d75-185">Host</span><span class="sxs-lookup"><span data-stu-id="44d75-185">Host</span></span> | <span data-ttu-id="44d75-186">Valeur</span><span class="sxs-lookup"><span data-stu-id="44d75-186">Value</span></span> |
| - | - | - |
| <span data-ttu-id="44d75-187">A</span><span class="sxs-lookup"><span data-stu-id="44d75-187">A</span></span> | `@` | <span data-ttu-id="44d75-188">Adresse IP à partir de [adresse IP de l’application hello de copie](#info)</span><span class="sxs-lookup"><span data-stu-id="44d75-188">IP address from [Copy hello app's IP address](#info)</span></span> |
| <span data-ttu-id="44d75-189">TXT</span><span class="sxs-lookup"><span data-stu-id="44d75-189">TXT</span></span> | `@` | `<app_name>.azurewebsites.net` |

<span data-ttu-id="44d75-190">Lorsque les enregistrements de hello sont ajoutés, hello page d’enregistrements DNS se présente comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="44d75-190">When hello records are added, hello DNS records page looks like hello following example:</span></span>

![Page Enregistrements DNS](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a><span data-ttu-id="44d75-192">Activer hello un mappage d’enregistrements dans l’application hello</span><span class="sxs-lookup"><span data-stu-id="44d75-192">Enable hello A record mapping in hello app</span></span>

<span data-ttu-id="44d75-193">Dans l’application hello **les domaines personnalisés** Bonjour portail Azure, ajoutez hello complet nom DNS personnalisé (par exemple, `contoso.com`) toohello liste.</span><span class="sxs-lookup"><span data-stu-id="44d75-193">Back in hello app's **Custom domains** page in hello Azure portal, add hello fully qualified custom DNS name (for example, `contoso.com`) toohello list.</span></span>

<span data-ttu-id="44d75-194">Sélectionnez hello  **+**  icône suivant trop**ajouter le nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="44d75-194">Select hello **+** icon next too**Add hostname**.</span></span>

![Ajouter un nom d’hôte](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

<span data-ttu-id="44d75-196">Nom de domaine complet de hello type que vous avez configuré comme enregistrement hello A, `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="44d75-196">Type hello fully qualified domain name that you configured hello A record for, such as `contoso.com`.</span></span>

<span data-ttu-id="44d75-197">Sélectionnez **Valider**.</span><span class="sxs-lookup"><span data-stu-id="44d75-197">Select **Validate**.</span></span>

<span data-ttu-id="44d75-198">Hello **ajouter le nom d’hôte** bouton est activé.</span><span class="sxs-lookup"><span data-stu-id="44d75-198">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="44d75-199">Assurez-vous que **type d’enregistrement de nom d’hôte** est défini trop**un enregistrement (example.com)**.</span><span class="sxs-lookup"><span data-stu-id="44d75-199">Make sure that **Hostname record type** is set too**A record (example.com)**.</span></span>

<span data-ttu-id="44d75-200">Sélectionnez **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="44d75-200">Select **Add hostname**.</span></span>

![Ajouter une application de toohello nom DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

<span data-ttu-id="44d75-202">Il peut prendre un certain temps pour hello nouveau nom d’hôte toobe est répercutée dans l’application hello **les domaines personnalisés** page.</span><span class="sxs-lookup"><span data-stu-id="44d75-202">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="44d75-203">Essayez d’actualiser les données de salutation navigateur tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="44d75-203">Try refreshing hello browser tooupdate hello data.</span></span>

![Enregistrement A ajouté](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

<span data-ttu-id="44d75-205">Si vous manqué une étape ou que vous faites une faute de frappe quelque part précédemment, vous voyez une erreur de vérification bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="44d75-205">If you missed a step or made a typo somewhere earlier, you see a verification error at hello bottom of hello page.</span></span>

![Erreur de vérification](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a><span data-ttu-id="44d75-207">Mapper un domaine générique</span><span class="sxs-lookup"><span data-stu-id="44d75-207">Map a wildcard domain</span></span>

<span data-ttu-id="44d75-208">Dans l’exemple de didacticiel hello, vous mappez un [nom DNS de caractère générique](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (par exemple, `*.contoso.com`) toohello application de Service de l’application en ajoutant un enregistrement CNAME.</span><span class="sxs-lookup"><span data-stu-id="44d75-208">In hello tutorial example, you map a [wildcard DNS name](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (for example, `*.contoso.com`) toohello App Service app by adding a CNAME record.</span></span> 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a><span data-ttu-id="44d75-209">Créer l’enregistrement CNAME de hello</span><span class="sxs-lookup"><span data-stu-id="44d75-209">Create hello CNAME record</span></span>

<span data-ttu-id="44d75-210">Ajouter un toomap enregistrement CNAME nom d’hôte par défaut de nom de caractère générique d’une application de toohello (`<app_name>.azurewebsites.net`).</span><span class="sxs-lookup"><span data-stu-id="44d75-210">Add a CNAME record toomap a wildcard name toohello app's default hostname (`<app_name>.azurewebsites.net`).</span></span>

<span data-ttu-id="44d75-211">Pourquoi `*.contoso.com` exemple de domaine, hello enregistrement CNAME mappera les nom hello `*` trop`<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="44d75-211">For hello `*.contoso.com` domain example, hello CNAME record will map hello name `*` too`<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="44d75-212">Lorsque hello CNAME est ajouté, hello page d’enregistrements DNS se présente comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="44d75-212">When hello CNAME is added, hello DNS records page looks like hello following example:</span></span>

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a><span data-ttu-id="44d75-214">Activer le mappage d’enregistrement CNAME hello dans l’application hello</span><span class="sxs-lookup"><span data-stu-id="44d75-214">Enable hello CNAME record mapping in hello app</span></span>

<span data-ttu-id="44d75-215">Vous pouvez maintenant ajouter un sous-domaine qui correspond au nom toohello application de hello génériques (par exemple, `sub1.contoso.com` et `sub2.contoso.com` correspond à `*.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="44d75-215">You can now add any subdomain that matches hello wildcard name toohello app (for example, `sub1.contoso.com` and `sub2.contoso.com` match `*.contoso.com`).</span></span> 

<span data-ttu-id="44d75-216">Bonjour gauche de navigation de page de l’application hello Bonjour portail Azure, sélectionnez **les domaines personnalisés**.</span><span class="sxs-lookup"><span data-stu-id="44d75-216">In hello left navigation of hello app page in hello Azure portal, select **Custom domains**.</span></span> 

![Menu Domaines personnalisés](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

<span data-ttu-id="44d75-218">Sélectionnez hello  **+**  icône suivant trop**ajouter le nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="44d75-218">Select hello **+** icon next too**Add hostname**.</span></span>

![Ajouter un nom d’hôte](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

<span data-ttu-id="44d75-220">Tapez un nom de domaine complet qui correspond au domaine de hello générique (par exemple, `sub1.contoso.com`), puis sélectionnez **Validate**.</span><span class="sxs-lookup"><span data-stu-id="44d75-220">Type a fully qualified domain name that matches hello wildcard domain (for example, `sub1.contoso.com`), and then select **Validate**.</span></span>

<span data-ttu-id="44d75-221">Hello **ajouter le nom d’hôte** bouton est activé.</span><span class="sxs-lookup"><span data-stu-id="44d75-221">hello **Add hostname** button is activated.</span></span> 

<span data-ttu-id="44d75-222">Assurez-vous que **type d’enregistrement de nom d’hôte** est défini trop**enregistrement CNAME (www.example.com ou tout sous-domaine)**.</span><span class="sxs-lookup"><span data-stu-id="44d75-222">Make sure that **Hostname record type** is set too**CNAME record (www.example.com or any subdomain)**.</span></span>

<span data-ttu-id="44d75-223">Sélectionnez **Ajouter un nom d’hôte**.</span><span class="sxs-lookup"><span data-stu-id="44d75-223">Select **Add hostname**.</span></span>

![Ajouter une application de toohello nom DNS](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

<span data-ttu-id="44d75-225">Il peut prendre un certain temps pour hello nouveau nom d’hôte toobe est répercutée dans l’application hello **les domaines personnalisés** page.</span><span class="sxs-lookup"><span data-stu-id="44d75-225">It might take some time for hello new hostname toobe reflected in hello app's **Custom domains** page.</span></span> <span data-ttu-id="44d75-226">Essayez d’actualiser les données de salutation navigateur tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="44d75-226">Try refreshing hello browser tooupdate hello data.</span></span>

<span data-ttu-id="44d75-227">Sélectionnez hello  **+**  icône tooadd à nouveau un autre nom d’hôte qui correspond au domaine de caractère générique hello.</span><span class="sxs-lookup"><span data-stu-id="44d75-227">Select hello **+** icon again tooadd another hostname that matches hello wildcard domain.</span></span> <span data-ttu-id="44d75-228">Par exemple, ajoutez `sub2.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="44d75-228">For example, add `sub2.contoso.com`.</span></span>

![Enregistrement CNAME ajouté](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a><span data-ttu-id="44d75-230">Test dans le navigateur</span><span class="sxs-lookup"><span data-stu-id="44d75-230">Test in browser</span></span>

<span data-ttu-id="44d75-231">Rechercher les noms DNS toohello que vous avez configuré précédemment (par exemple, `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, et `sub2.contoso.com`).</span><span class="sxs-lookup"><span data-stu-id="44d75-231">Browse toohello DNS name(s) that you configured earlier (for example, `contoso.com`,  `www.contoso.com`, `sub1.contoso.com`, and `sub2.contoso.com`).</span></span>

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a><span data-ttu-id="44d75-233">Automatiser des tâches à l’aide de scripts</span><span class="sxs-lookup"><span data-stu-id="44d75-233">Automate with scripts</span></span>

<span data-ttu-id="44d75-234">Vous pouvez automatiser la gestion des domaines personnalisés avec des scripts, à l’aide de hello [CLI d’Azure](/cli/azure/install-azure-cli) ou [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="44d75-234">You can automate management of custom domains with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="azure-cli"></a><span data-ttu-id="44d75-235">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="44d75-235">Azure CLI</span></span> 

<span data-ttu-id="44d75-236">Hello commande suivante ajoute un tooan de nom DNS personnalisé configuré application de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="44d75-236">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

<span data-ttu-id="44d75-237">Pour plus d’informations, consultez [mapper une domaine personnalisé l’application web tooa](scripts/app-service-cli-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="44d75-237">For more information, see [Map a custom domain tooa web app](scripts/app-service-cli-configure-custom-domain.md).</span></span> 

### <a name="azure-powershell"></a><span data-ttu-id="44d75-238">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="44d75-238">Azure PowerShell</span></span> 

<span data-ttu-id="44d75-239">Hello commande suivante ajoute un tooan de nom DNS personnalisé configuré application de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="44d75-239">hello following command adds a configured custom DNS name tooan App Service app.</span></span> 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

<span data-ttu-id="44d75-240">Pour plus d’informations, consultez [affecter une application web de tooa domaine personnalisé](scripts/app-service-powershell-configure-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="44d75-240">For more information, see [Assign a custom domain tooa web app](scripts/app-service-powershell-configure-custom-domain.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="44d75-241">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="44d75-241">Next steps</span></span>

<span data-ttu-id="44d75-242">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="44d75-242">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="44d75-243">Mapper un sous-domaine à l’aide d’un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="44d75-243">Map a subdomain by using a CNAME record</span></span>
> * <span data-ttu-id="44d75-244">Mapper un domaine racine à l’aide d’un enregistrement A</span><span class="sxs-lookup"><span data-stu-id="44d75-244">Map a root domain by using an A record</span></span>
> * <span data-ttu-id="44d75-245">Mapper un domaine générique à l’aide d’un enregistrement CNAME</span><span class="sxs-lookup"><span data-stu-id="44d75-245">Map a wildcard domain by using a CNAME record</span></span>
> * <span data-ttu-id="44d75-246">Automatiser le mappage de domaine à l’aide de scripts</span><span class="sxs-lookup"><span data-stu-id="44d75-246">Automate domain mapping with scripts</span></span>

<span data-ttu-id="44d75-247">Avancer toolearn de didacticiel suivant toohello comment toobind une SSL personnalisée certificat tooa l’application web.</span><span class="sxs-lookup"><span data-stu-id="44d75-247">Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="44d75-248">Lier un tooAzure de certificat SSL personnalisé existant Web Apps</span><span class="sxs-lookup"><span data-stu-id="44d75-248">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-ssl.md)
