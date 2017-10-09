---
title: "aaaConfigure un nom de domaine personnalisé dans Azure App Service (GoDaddy)"
description: "Découvrez comment toouse un domaine nom de GoDaddy avec Azure Web Apps"
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="86e27-103">Configurer un nom de domaine personnalisé dans Azure App Service (acheté directement sur GoDaddy)</span><span class="sxs-lookup"><span data-stu-id="86e27-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="86e27-104">Si vous avez acheté domaine via Azure App Service Web Apps, consultez toohello dernière étape de [acheter un domaine pour les applications Web](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="86e27-104">If you have purchased domain through Azure App Service Web Apps then refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="86e27-105">Cet article explique comment utiliser un nom de domaine personnalisé acheté directement auprès de [GoDaddy](https://godaddy.com) avec [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="86e27-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="86e27-106">Présentation des enregistrements DNS</span><span class="sxs-lookup"><span data-stu-id="86e27-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="86e27-107">Ajout d'un enregistrement DNS pour votre domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="86e27-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="86e27-108">tooassociate votre domaine personnalisé avec une application web dans le Service d’applications, vous devez ajouter une nouvelle entrée dans la table de hello DNS pour votre domaine personnalisé à l’aide des outils fournis par GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="86e27-108">tooassociate your custom domain with a web app in App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="86e27-109">Utilisez hello suite d’outils du DNS hello étapes toolocate à GoDaddy.com</span><span class="sxs-lookup"><span data-stu-id="86e27-109">Use hello following steps toolocate hello DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="86e27-110">Connectez-vous au compte tooyour avec GoDaddy.com, puis sélectionnez **mon compte** , puis **gérer mes domaines**.</span><span class="sxs-lookup"><span data-stu-id="86e27-110">Log on tooyour account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="86e27-111">Menu déroulant de sélection hello hello nom de domaine que vous souhaitez toouse avec votre application web Azure, sélectionnez **gérer DNS**.</span><span class="sxs-lookup"><span data-stu-id="86e27-111">Select hello drop-down menu for hello domain name that you wish toouse with your Azure web app and select **Manage DNS**.</span></span>
   
    ![page des domaines personnalisés de GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="86e27-113">À partir de hello **les détails du domaine** page, faites défiler toohello **fichier de Zone DNS** onglet. Il s’agit de section hello utilisée pour ajouter et modifier des enregistrements DNS pour votre nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="86e27-113">From hello **Domain details** page, scroll toohello **DNS Zone File** tab. This is hello section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![Onglet DNS Zone File](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="86e27-115">Sélectionnez **ajouter un enregistrement** tooadd un enregistrement existant.</span><span class="sxs-lookup"><span data-stu-id="86e27-115">Select **Add Record** tooadd an existing record.</span></span>
   
    <span data-ttu-id="86e27-116">trop**modifier** un enregistrement existant, l’icône de stylet & papier hello select à côté de l’enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="86e27-116">too**edit** an existing record, select hello pen & paper icon beside hello record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="86e27-117">Avant d’ajouter de nouveaux enregistrements, notez que GoDaddy a déjà créé des enregistrements DNS pour les sous-domaines populaires (sous **Host** dans l’éditeur), par exemple **email**, **files**, **mail**, etc.</span><span class="sxs-lookup"><span data-stu-id="86e27-117">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="86e27-118">Si hello nom que vous souhaitez toouse déjà existe, modifier l’enregistrement de hello existant au lieu de créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="86e27-118">If hello name you wish toouse already exists, modify hello existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="86e27-119">Lorsque vous ajoutez un enregistrement, vous devez tout d’abord sélectionner le type d’enregistrement hello.</span><span class="sxs-lookup"><span data-stu-id="86e27-119">When adding a record, you must first select hello record type.</span></span>
   
    ![sélectionner le type d'enregistrement](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="86e27-121">Ensuite, vous devez fournir hello **hôte** (hello domaine personnalisé ou sous-domaine) et ce qu’il **pointe vers**.</span><span class="sxs-lookup"><span data-stu-id="86e27-121">Next, you must provide hello **Host** (hello custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![ajouter un enregistrement de zone](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="86e27-123">Lorsque vous ajoutez un **un enregistrement (hôte)** -vous devez définir hello **hôte** champ tooeither  **@**  (représente le nom de domaine racine, tel que  **Contoso.com**,) * (un caractère générique pour faire correspondre plusieurs sous-domaines,) ou vous souhaitez toouse sous-domaine hello (par exemple, **www**.) Vous devez définir hello **pointe vers** champ d’adresse IP de toohello de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="86e27-123">When adding an **A (host) record** - you must set hello **Host** field tooeither **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or hello sub-domain you wish toouse (for example, **www**.) You must set hello **Points to** field toohello IP address of your Azure web app.</span></span>
   * <span data-ttu-id="86e27-124">Lorsque vous ajoutez un **enregistrement CNAME (alias)** -vous devez définir hello **hôte** champ toohello sous-domaine toouse vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="86e27-124">When adding a **CNAME (alias) record** - you must set hello **Host** field toohello sub-domain you wish toouse.</span></span> <span data-ttu-id="86e27-125">Par exemple, **www**.</span><span class="sxs-lookup"><span data-stu-id="86e27-125">For example, **www**.</span></span> <span data-ttu-id="86e27-126">Vous devez définir hello **pointe vers** champ toohello **. azurewebsites.net** nom de domaine de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="86e27-126">You must set hello **Points to** field toohello **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="86e27-127">Par exemple, **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="86e27-127">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="86e27-128">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="86e27-128">Click **Add Another**.</span></span>
5. <span data-ttu-id="86e27-129">Sélectionnez **TXT** en tant que type d’enregistrement hello, puis spécifiez un **hôte** valeur  **@**  et un **pointe vers** valeur  **&lt;yourwebappname&gt;. azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="86e27-129">Select **TXT** as hello record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="86e27-130">Cet enregistrement TXT est utilisé par Azure toovalidate que vous possédez le domaine de hello décrite par hello un enregistrement TXT premier enregistrement ou hello.</span><span class="sxs-lookup"><span data-stu-id="86e27-130">This TXT record is used by Azure toovalidate that you own hello domain described by hello A record or hello first TXT record.</span></span> <span data-ttu-id="86e27-131">Une fois que le domaine de hello a été mappé toohello web application hello portail Azure, cette entrée de l’enregistrement TXT peut être supprimée.</span><span class="sxs-lookup"><span data-stu-id="86e27-131">Once hello domain has been mapped toohello web app in hello Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="86e27-132">Lorsque vous avez terminé d’ajouter ou modifier des enregistrements, cliquez sur **Terminer** toosave modifications.</span><span class="sxs-lookup"><span data-stu-id="86e27-132">When you have finished adding or modifying records, click **Finish** toosave changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a><span data-ttu-id="86e27-133">Activer le nom de domaine hello sur votre application web</span><span class="sxs-lookup"><span data-stu-id="86e27-133">Enable hello domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="86e27-134">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="86e27-134">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="86e27-135">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="86e27-135">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="86e27-136">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="86e27-136">What's changed</span></span>
* <span data-ttu-id="86e27-137">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="86e27-137">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

