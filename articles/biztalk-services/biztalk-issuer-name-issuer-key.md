---
title: "Nom et clé de l’émetteur dans BizTalk Services | Microsoft Docs"
description: "Découvrez comment récupérer le nom et la clé de l'émetteur pour le bus des services ou le contrôle d'accès (ACS) dans BizTalk Services. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: b9fd985c23558596408e78eadae00dd0f95c4214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="826e2-104">Nom et clé de l'émetteur dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="826e2-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="826e2-105">Azure BizTalk Services utilise le nom et la clé de l'émetteur Service Bus, ainsi que le nom et la clé de l'émetteur Access Control.</span><span class="sxs-lookup"><span data-stu-id="826e2-105">Azure BizTalk Services uses the Service Bus Issuer Name and Issuer Key, and the Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="826e2-106">Plus précisément :</span><span class="sxs-lookup"><span data-stu-id="826e2-106">Specifically:</span></span>

| <span data-ttu-id="826e2-107">Task</span><span class="sxs-lookup"><span data-stu-id="826e2-107">Task</span></span> | <span data-ttu-id="826e2-108">Nom et clé de l'émetteur</span><span class="sxs-lookup"><span data-stu-id="826e2-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="826e2-109">Déploiement de votre application à partir de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="826e2-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="826e2-110">Nom et clé de l'émetteur Access Control</span><span class="sxs-lookup"><span data-stu-id="826e2-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="826e2-111">Configuration du portail Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="826e2-111">Configuring the Azure BizTalk Services Portal</span></span> |<span data-ttu-id="826e2-112">Nom et clé de l'émetteur Access Control</span><span class="sxs-lookup"><span data-stu-id="826e2-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="826e2-113">Création de relais métier avec les services d'adaptateur BizTalk dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="826e2-113">Creating LOB Relays with the BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="826e2-114">Nom et clé de l'émetteur Service Bus</span><span class="sxs-lookup"><span data-stu-id="826e2-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="826e2-115">La présente rubrique répertorie les étapes permettant de récupérer le nom et la clé de l’émetteur.</span><span class="sxs-lookup"><span data-stu-id="826e2-115">This topic lists the steps to retrieve the Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="826e2-116">Nom et clé de l'émetteur Access Control</span><span class="sxs-lookup"><span data-stu-id="826e2-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="826e2-117">Le nom et la clé de l'émetteur Access Control sont utilisés par les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="826e2-117">The Access Control Issuer Name and Issuer Key are used by the following:</span></span>

* <span data-ttu-id="826e2-118">Votre application Azure BizTalk Service créée dans Visual Studio : pour déployer correctement votre application BizTalk Service dans Visual Studio sur Azure, entrez le nom et la clé de l’émetteur Access Control.</span><span class="sxs-lookup"><span data-stu-id="826e2-118">Your Azure BizTalk Service application created in Visual Studio: To successfully deploy your BizTalk Service application in Visual Studio to Azure, you enter the Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="826e2-119">Portail Azure BizTalk Services : lorsque vous créez un service BizTalk et que vous ouvrez le portail BizTalk Services, votre nom et votre clé de l’émetteur Access Control sont automatiquement inscrits pour vos déploiements avec les mêmes valeurs Access Control.</span><span class="sxs-lookup"><span data-stu-id="826e2-119">The Azure BizTalk Services  Portal: When you create a BizTalk Service and open the BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with the same Access Control values.</span></span>

### <a name="get-the-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="826e2-120">Obtenir le nom et la clé de l’émetteur Access Control</span><span class="sxs-lookup"><span data-stu-id="826e2-120">Get the Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="826e2-121">Pour utiliser ACS pour l’authentification et obtenir les valeurs de nom et de clé de l’émetteur, les étapes générales sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="826e2-121">To use ACS for authentication, and get the Issuer Name and Issuer Key values, the overall steps include:</span></span>

1. <span data-ttu-id="826e2-122">Installez les [applets de commande Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="826e2-122">Install the [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="826e2-123">Ajoutez votre compte Azure : `Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="826e2-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="826e2-124">Retournez le nom de votre abonnement : `get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="826e2-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="826e2-125">Sélectionnez votre abonnement : `select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="826e2-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="826e2-126">Créez un espace de noms : `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="826e2-126">Create a new namespace: `new-azuresbnamespace <name for the service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="826e2-127">Exemple :`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="826e2-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="826e2-128">Lorsque le nouvel espace de noms ACS est créé (ce qui peut prendre plusieurs minutes), les valeurs de nom et de clé de l’émetteur sont répertoriées dans la chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="826e2-128">When the new ACS namespace is created (which can take several minutes), the Issuer Name and Issuer Key values are listed in the connection string:</span></span> 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

<span data-ttu-id="826e2-129">Pour résumer :</span><span class="sxs-lookup"><span data-stu-id="826e2-129">To summarize:</span></span>  
<span data-ttu-id="826e2-130">Nom de l’émetteur = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="826e2-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="826e2-131">Clé de l’émetteur = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="826e2-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="826e2-132">Informations complémentaires sur l’applet de commande [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx).</span><span class="sxs-lookup"><span data-stu-id="826e2-132">More on the [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="826e2-133">Nom et clé de l'émetteur Service Bus</span><span class="sxs-lookup"><span data-stu-id="826e2-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="826e2-134">Le nom et la clé de l'émetteur Service Bus sont utilisés par BizTalk Adapter Services.</span><span class="sxs-lookup"><span data-stu-id="826e2-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="826e2-135">Dans votre projet BizTalk Services dans Visual Studio, vous utilisez les services d'adaptateur BizTalk pour vous connecter à un système métier local.</span><span class="sxs-lookup"><span data-stu-id="826e2-135">In your BizTalk Services project in Visual Studio, you use the BizTalk Adapter Services to connect to an on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="826e2-136">Pour vous connecter, vous créez le relais métier et entrez les détails relatifs à votre système métier.</span><span class="sxs-lookup"><span data-stu-id="826e2-136">To connect, you create the LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="826e2-137">À cette occasion, vous entrez également le nom et la clé de l'émetteur Service Bus.</span><span class="sxs-lookup"><span data-stu-id="826e2-137">When doing this, you also enter the Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="to-retrieve-the-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="826e2-138">Pour récupérer le nom et la clé de l'émetteur Service Bus</span><span class="sxs-lookup"><span data-stu-id="826e2-138">To retrieve the Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="826e2-139">Connectez-vous au [portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="826e2-139">Sign in to the [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="826e2-140">Dans le volet de navigation de gauche, sélectionnez **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="826e2-140">In the left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="826e2-141">Sélectionnez votre espace de noms.</span><span class="sxs-lookup"><span data-stu-id="826e2-141">Select your namespace.</span></span> <span data-ttu-id="826e2-142">Dans la barre des tâches, sélectionnez **Informations de connexion**.</span><span class="sxs-lookup"><span data-stu-id="826e2-142">In the task bar, select **Connection Information**.</span></span> <span data-ttu-id="826e2-143">Cette action affiche **l’Émetteur par défaut** (Nom de l’émetteur) et la **Clé par défaut** (Clé de l’émetteur).</span><span class="sxs-lookup"><span data-stu-id="826e2-143">This displays the **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="826e2-144">Leurs valeurs peuvent être copiées.</span><span class="sxs-lookup"><span data-stu-id="826e2-144">Their values can be copied.</span></span>  

<span data-ttu-id="826e2-145">Pour résumer :</span><span class="sxs-lookup"><span data-stu-id="826e2-145">To summarize:</span></span>  
<span data-ttu-id="826e2-146">Nom de l'émetteur = émetteur par défaut</span><span class="sxs-lookup"><span data-stu-id="826e2-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="826e2-147">Clé de l'émetteur = clé par défaut</span><span class="sxs-lookup"><span data-stu-id="826e2-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="826e2-148">Suivant</span><span class="sxs-lookup"><span data-stu-id="826e2-148">Next</span></span>
<span data-ttu-id="826e2-149">Autres rubriques Azure BizTalk Services :</span><span class="sxs-lookup"><span data-stu-id="826e2-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="826e2-150">Installation du Kit de développement logiciel (SDK) Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="826e2-150">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="826e2-151">Didacticiels : Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="826e2-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="826e2-152">Utilisation du Kit de développement logiciel (SDK) Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="826e2-152">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="826e2-153">Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="826e2-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="826e2-154">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="826e2-154">See Also</span></span>
* [<span data-ttu-id="826e2-155">Utilisation du service de gestion ACS pour configurer des identités de service</span><span class="sxs-lookup"><span data-stu-id="826e2-155">How to: Use ACS Management Service to Configure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="826e2-156">Tableau comparatif des éditions Développeur, De base, Standard et Premium de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="826e2-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="826e2-157">BizTalk Services : approvisionnement à l’aide du portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="826e2-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="826e2-158">Tableau comparatif des états d'approvisionnement BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="826e2-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="826e2-159">Onglets Tableau de bord, Surveiller et Mettre à l'échelle dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="826e2-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="826e2-160">Sauvegarde et restauration de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="826e2-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="826e2-161">Limitation dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="826e2-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

