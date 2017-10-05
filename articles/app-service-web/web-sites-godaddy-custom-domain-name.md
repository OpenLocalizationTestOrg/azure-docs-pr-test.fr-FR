---
title: "Configurer un nom de domaine personnalisé dans Azure App Service (GoDaddy)"
description: "Apprenez à utiliser un nom de domaine à partir de GoDaddy avec Azure Web Apps"
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
ms.openlocfilehash: 158c5dc06f83e16633d3c2fbb4eb27d3e8af030c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="22bbc-103">Configurer un nom de domaine personnalisé dans Azure App Service (acheté directement sur GoDaddy)</span><span class="sxs-lookup"><span data-stu-id="22bbc-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="22bbc-104">Si vous avez acheté un domaine via Azure App Service Web Apps, reportez-vous à l’étape finale de l’article [Acheter un domaine pour Web Apps](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="22bbc-104">If you have purchased domain through Azure App Service Web Apps then refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="22bbc-105">Cet article explique comment utiliser un nom de domaine personnalisé acheté directement auprès de [GoDaddy](https://godaddy.com) avec [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="22bbc-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="22bbc-106">Présentation des enregistrements DNS</span><span class="sxs-lookup"><span data-stu-id="22bbc-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="22bbc-107">Ajout d'un enregistrement DNS pour votre domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="22bbc-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="22bbc-108">Pour associer votre domaine personnalisé à une application web dans App Service, vous devez ajouter une nouvelle entrée pour ce domaine dans la table DNS en utilisant les outils fournis par GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="22bbc-108">To associate your custom domain with a web app in App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="22bbc-109">Pour trouver les outils DNS pour GoDaddy.com, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="22bbc-109">Use the following steps to locate the DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="22bbc-110">Connectez-vous à votre compte GoDaddy.com et sélectionnez **My Account**, puis **Manage my domains**.</span><span class="sxs-lookup"><span data-stu-id="22bbc-110">Log on to your account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="22bbc-111">Dans le menu déroulant, sélectionnez le nom de domaine à utiliser avec votre application web Azure, puis sélectionnez **Manage DNS** (Gérer DNS).</span><span class="sxs-lookup"><span data-stu-id="22bbc-111">Select the drop-down menu for the domain name that you wish to use with your Azure web app and select **Manage DNS**.</span></span>
   
    ![page des domaines personnalisés de GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="22bbc-113">Dans la page **Domain details**, faites défiler jusqu’à l’onglet **DNS Zone File**.</span><span class="sxs-lookup"><span data-stu-id="22bbc-113">From the **Domain details** page, scroll to the **DNS Zone File** tab.</span></span> <span data-ttu-id="22bbc-114">Il s'agit de la section qui vous permet d'ajouter et de modifier des enregistrements DNS pour votre nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="22bbc-114">This is the section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![Onglet DNS Zone File](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="22bbc-116">Sélectionnez **Add Record** pour ajouter un enregistrement existant.</span><span class="sxs-lookup"><span data-stu-id="22bbc-116">Select **Add Record** to add an existing record.</span></span>
   
    <span data-ttu-id="22bbc-117">Pour **modifier** un enregistrement existant, sélectionnez l’icône représentant un stylo et du papier à côté de l’enregistrement souhaité.</span><span class="sxs-lookup"><span data-stu-id="22bbc-117">To **edit** an existing record, select the pen & paper icon beside the record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="22bbc-118">Avant d’ajouter de nouveaux enregistrements, notez que GoDaddy a déjà créé des enregistrements DNS pour les sous-domaines populaires (sous **Host** dans l’éditeur), par exemple **email**, **files**, **mail**, etc.</span><span class="sxs-lookup"><span data-stu-id="22bbc-118">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="22bbc-119">Si le nom que vous souhaitez utiliser existe déjà, modifiez l'enregistrement existant plutôt que d'en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="22bbc-119">If the name you wish to use already exists, modify the existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="22bbc-120">Quand vous ajoutez un enregistrement, vous devez d'abord sélectionner son type.</span><span class="sxs-lookup"><span data-stu-id="22bbc-120">When adding a record, you must first select the record type.</span></span>
   
    ![sélectionner le type d'enregistrement](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="22bbc-122">Vous devez ensuite indiquer l’**Host** (domaine ou sous-domaine personnalisé) et sa cible dans **Points to**.</span><span class="sxs-lookup"><span data-stu-id="22bbc-122">Next, you must provide the **Host** (the custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![ajouter un enregistrement de zone](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="22bbc-124">Lorsque vous ajoutez un **enregistrement A (host)**, vous devez attribuer au champ **Hôte** la valeur **@** (correspondant au nom de domaine racine, par exemple **contoso.com**), la valeur * (caractère générique correspondant à plusieurs sous-domaines) ou le sous-domaine à utiliser (par exemple, **www**). Dans le champ **Pointe sur**, indiquez l’adresse IP de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="22bbc-124">When adding an **A (host) record** - you must set the **Host** field to either **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or the sub-domain you wish to use (for example, **www**.) You must set the **Points to** field to the IP address of your Azure web app.</span></span>
   * <span data-ttu-id="22bbc-125">Quand vous ajoutez un **CNAME (alias) record**, vous devez définir le champ **Host** en fonction du sous-domaine à utiliser.</span><span class="sxs-lookup"><span data-stu-id="22bbc-125">When adding a **CNAME (alias) record** - you must set the **Host** field to the sub-domain you wish to use.</span></span> <span data-ttu-id="22bbc-126">Par exemple, **www**.</span><span class="sxs-lookup"><span data-stu-id="22bbc-126">For example, **www**.</span></span> <span data-ttu-id="22bbc-127">Dans le champ **Points to**, indiquez le nom de domaine **.azurewebsites.net** de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="22bbc-127">You must set the **Points to** field to the **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="22bbc-128">Par exemple, **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="22bbc-128">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="22bbc-129">Cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="22bbc-129">Click **Add Another**.</span></span>
5. <span data-ttu-id="22bbc-130">Sélectionnez **TXT** comme type d’enregistrement, puis spécifiez une valeur **Host** de **@** et une valeur **Points to** de **&lt;yourwebappname&gt;.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="22bbc-130">Select **TXT** as the record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="22bbc-131">Cet enregistrement TXT permet à Azure de confirmer que vous possédez le domaine décrit par l’enregistrement A ou le premier enregistrement TXT.</span><span class="sxs-lookup"><span data-stu-id="22bbc-131">This TXT record is used by Azure to validate that you own the domain described by the A record or the first TXT record.</span></span> <span data-ttu-id="22bbc-132">Une fois que le domaine a été mappé à l’application web dans le portail Azure, l’entrée d’enregistrement TXT peut être supprimée.</span><span class="sxs-lookup"><span data-stu-id="22bbc-132">Once the domain has been mapped to the web app in the Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="22bbc-133">Une fois que vous avez fini d'ajouter ou de modifier des enregistrements, cliquez sur **Finish** pour enregistrer les changements.</span><span class="sxs-lookup"><span data-stu-id="22bbc-133">When you have finished adding or modifying records, click **Finish** to save changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-the-domain-name-on-your-web-app"></a><span data-ttu-id="22bbc-134">Activer le nom de domaine sur votre application web</span><span class="sxs-lookup"><span data-stu-id="22bbc-134">Enable the domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="22bbc-135">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="22bbc-135">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="22bbc-136">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="22bbc-136">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="22bbc-137">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="22bbc-137">What's changed</span></span>
* <span data-ttu-id="22bbc-138">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="22bbc-138">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

