---
title: "aaaIssuer nom et clé de l’émetteur dans BizTalk Services | Documents Microsoft"
description: "Découvrez comment tooretrieve nom de l’émetteur et la clé de l’émetteur pour Service Bus ou Access Control (ACS) dans les Services BizTalk. MABS, WABS"
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
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a><span data-ttu-id="a0524-104">Nom et clé de l'émetteur dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="a0524-104">BizTalk Services: Issuer Name and Issuer Key</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="a0524-105">Les Services BizTalk Azure utilise hello nom de l’émetteur de Bus de Service et clé de l’émetteur et hello nom de l’émetteur de contrôle de l’accès et clé de l’émetteur.</span><span class="sxs-lookup"><span data-stu-id="a0524-105">Azure BizTalk Services uses hello Service Bus Issuer Name and Issuer Key, and hello Access Control Issuer Name and Issuer Key.</span></span> <span data-ttu-id="a0524-106">Plus précisément :</span><span class="sxs-lookup"><span data-stu-id="a0524-106">Specifically:</span></span>

| <span data-ttu-id="a0524-107">Task</span><span class="sxs-lookup"><span data-stu-id="a0524-107">Task</span></span> | <span data-ttu-id="a0524-108">Nom et clé de l'émetteur</span><span class="sxs-lookup"><span data-stu-id="a0524-108">Which Issuer Name and Issuer Key</span></span> |
| --- | --- |
| <span data-ttu-id="a0524-109">Déploiement de votre application à partir de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a0524-109">Deploying your application from Visual Studio</span></span> |<span data-ttu-id="a0524-110">Nom et clé de l'émetteur Access Control</span><span class="sxs-lookup"><span data-stu-id="a0524-110">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="a0524-111">Configuration hello le portail Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="a0524-111">Configuring hello Azure BizTalk Services Portal</span></span> |<span data-ttu-id="a0524-112">Nom et clé de l'émetteur Access Control</span><span class="sxs-lookup"><span data-stu-id="a0524-112">Access Control Issuer Name and Issuer Key</span></span> |
| <span data-ttu-id="a0524-113">Création de relais LOB avec hello Services de l’adaptateur BizTalk dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a0524-113">Creating LOB Relays with hello BizTalk Adapter Services in Visual Studio</span></span> |<span data-ttu-id="a0524-114">Nom et clé de l'émetteur Service Bus</span><span class="sxs-lookup"><span data-stu-id="a0524-114">Service Bus Issuer Name and Issuer Key</span></span> |

<span data-ttu-id="a0524-115">Cette rubrique répertorie hello étapes tooretrieve hello nom de l’émetteur et la clé de l’émetteur.</span><span class="sxs-lookup"><span data-stu-id="a0524-115">This topic lists hello steps tooretrieve hello Issuer Name and Issuer Key.</span></span> 

## <a name="access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="a0524-116">Nom et clé de l'émetteur Access Control</span><span class="sxs-lookup"><span data-stu-id="a0524-116">Access Control Issuer Name and Issuer Key</span></span>
<span data-ttu-id="a0524-117">Hello, nom de l’émetteur de contrôle de l’accès et la clé d’émetteur sont utilisés par suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="a0524-117">hello Access Control Issuer Name and Issuer Key are used by hello following:</span></span>

* <span data-ttu-id="a0524-118">Votre application Azure BizTalk Service créée dans Visual Studio : toosuccessfully déployer votre application de BizTalk Service dans Visual Studio tooAzure, vous entrez hello nom de l’émetteur de contrôle de l’accès et la clé de l’émetteur.</span><span class="sxs-lookup"><span data-stu-id="a0524-118">Your Azure BizTalk Service application created in Visual Studio: toosuccessfully deploy your BizTalk Service application in Visual Studio tooAzure, you enter hello Access Control Issuer Name and Issuer Key.</span></span> 
* <span data-ttu-id="a0524-119">Hello le portail Azure BizTalk Services : lorsque vous créez un BizTalk Service et ouvrez hello portail BizTalk Services, votre nom de l’émetteur de contrôle de l’accès et la clé de l’émetteur sont automatiquement enregistrés pour vos déploiements avec hello les mêmes valeurs de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="a0524-119">hello Azure BizTalk Services  Portal: When you create a BizTalk Service and open hello BizTalk Services Portal, your Access Control Issuer Name and Issuer Key are automatically registered for your deployments with hello same Access Control values.</span></span>

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a><span data-ttu-id="a0524-120">Obtenir hello du nom de l’émetteur de contrôle de l’accès et la clé de l’émetteur</span><span class="sxs-lookup"><span data-stu-id="a0524-120">Get hello Access Control Issuer Name and Issuer Key</span></span>

<span data-ttu-id="a0524-121">ACS toouse pour l’authentification et get hello les valeurs de nom de l’émetteur et la clé de l’émetteur, hello étapes incluent :</span><span class="sxs-lookup"><span data-stu-id="a0524-121">toouse ACS for authentication, and get hello Issuer Name and Issuer Key values, hello overall steps include:</span></span>

1. <span data-ttu-id="a0524-122">Installer hello [applets de commande Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="a0524-122">Install hello [Azure Powershell cmdlets](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
2. <span data-ttu-id="a0524-123">Ajoutez votre compte Azure : `Add-AzureAccount`</span><span class="sxs-lookup"><span data-stu-id="a0524-123">Add your Azure account: `Add-AzureAccount`</span></span>
3. <span data-ttu-id="a0524-124">Retournez le nom de votre abonnement : `get-azuresubscription`</span><span class="sxs-lookup"><span data-stu-id="a0524-124">Return your subscription name: `get-azuresubscription`</span></span>
4. <span data-ttu-id="a0524-125">Sélectionnez votre abonnement : `select-azuresubscription <name of your subscription>`</span><span class="sxs-lookup"><span data-stu-id="a0524-125">Select your subscription: `select-azuresubscription <name of your subscription>`</span></span> 
5. <span data-ttu-id="a0524-126">Créez un espace de noms : `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="a0524-126">Create a new namespace: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>

    <span data-ttu-id="a0524-127">Exemple :`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span><span class="sxs-lookup"><span data-stu-id="a0524-127">Example:    `new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`</span></span>
      
5. <span data-ttu-id="a0524-128">Lors de la création d’espace de noms ACS de hello (qui peut prendre plusieurs minutes), les valeurs de nom de l’émetteur et la clé de l’émetteur de hello sont répertoriées dans la chaîne de connexion hello :</span><span class="sxs-lookup"><span data-stu-id="a0524-128">When hello new ACS namespace is created (which can take several minutes), hello Issuer Name and Issuer Key values are listed in hello connection string:</span></span> 

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

<span data-ttu-id="a0524-129">toosummarize :</span><span class="sxs-lookup"><span data-stu-id="a0524-129">toosummarize:</span></span>  
<span data-ttu-id="a0524-130">Nom de l’émetteur = SharedSecretIssuer</span><span class="sxs-lookup"><span data-stu-id="a0524-130">Issuer Name = SharedSecretIssuer</span></span>  
<span data-ttu-id="a0524-131">Clé de l’émetteur = SharedSecretKey</span><span class="sxs-lookup"><span data-stu-id="a0524-131">Issuer Key = SharedSecretKey</span></span>

<span data-ttu-id="a0524-132">D’autres informations sur hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="a0524-132">More on hello [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet.</span></span> 

## <a name="service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="a0524-133">Nom et clé de l'émetteur Service Bus</span><span class="sxs-lookup"><span data-stu-id="a0524-133">Service Bus Issuer Name and Issuer Key</span></span>
<span data-ttu-id="a0524-134">Le nom et la clé de l'émetteur Service Bus sont utilisés par BizTalk Adapter Services.</span><span class="sxs-lookup"><span data-stu-id="a0524-134">Service Bus Issuer Name and Issuer Key are used by BizTalk Adapter Services.</span></span> <span data-ttu-id="a0524-135">Dans votre projet BizTalk Services dans Visual Studio, vous utilisez système de hello Services de l’adaptateur BizTalk tooconnect tooan local de métier (LOB).</span><span class="sxs-lookup"><span data-stu-id="a0524-135">In your BizTalk Services project in Visual Studio, you use hello BizTalk Adapter Services tooconnect tooan on-premises Line-of-Business (LOB) system.</span></span> <span data-ttu-id="a0524-136">tooconnect, vous créez des hello relais LOB et entrez les détails de votre système métier.</span><span class="sxs-lookup"><span data-stu-id="a0524-136">tooconnect, you create hello LOB Relay and enter your LOB system details.</span></span> <span data-ttu-id="a0524-137">Ce faisant, vous entrez également hello nom de l’émetteur de Bus de Service et la clé de l’émetteur.</span><span class="sxs-lookup"><span data-stu-id="a0524-137">When doing this, you also enter hello Service Bus Issuer Name and Issuer Key.</span></span>

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a><span data-ttu-id="a0524-138">tooretrieve hello nom de l’émetteur de Bus de Service et la clé de l’émetteur</span><span class="sxs-lookup"><span data-stu-id="a0524-138">tooretrieve hello Service Bus Issuer Name and Issuer Key</span></span>
1. <span data-ttu-id="a0524-139">Connectez-vous à toohello [portail Azure classic](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="a0524-139">Sign in toohello [Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="a0524-140">Dans le volet de navigation gauche hello, sélectionnez **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="a0524-140">In hello left navigation pane, select **Service Bus**.</span></span>
3. <span data-ttu-id="a0524-141">Sélectionnez votre espace de noms.</span><span class="sxs-lookup"><span data-stu-id="a0524-141">Select your namespace.</span></span> <span data-ttu-id="a0524-142">Dans la barre des tâches hello, sélectionnez **les informations de connexion**.</span><span class="sxs-lookup"><span data-stu-id="a0524-142">In hello task bar, select **Connection Information**.</span></span> <span data-ttu-id="a0524-143">Cela affiche hello **émetteur par défaut** (nom de l’émetteur) et **clé par défaut** (clé d’émetteur).</span><span class="sxs-lookup"><span data-stu-id="a0524-143">This displays hello **Default Issuer** (Issuer Name) and **Default Key** (Issuer Key).</span></span> <span data-ttu-id="a0524-144">Leurs valeurs peuvent être copiées.</span><span class="sxs-lookup"><span data-stu-id="a0524-144">Their values can be copied.</span></span>  

<span data-ttu-id="a0524-145">toosummarize :</span><span class="sxs-lookup"><span data-stu-id="a0524-145">toosummarize:</span></span>  
<span data-ttu-id="a0524-146">Nom de l'émetteur = émetteur par défaut</span><span class="sxs-lookup"><span data-stu-id="a0524-146">Issuer Name = Default Issuer</span></span>  
<span data-ttu-id="a0524-147">Clé de l'émetteur = clé par défaut</span><span class="sxs-lookup"><span data-stu-id="a0524-147">Issuer Key = Default Key</span></span>

## <a name="next"></a><span data-ttu-id="a0524-148">Suivant</span><span class="sxs-lookup"><span data-stu-id="a0524-148">Next</span></span>
<span data-ttu-id="a0524-149">Autres rubriques Azure BizTalk Services :</span><span class="sxs-lookup"><span data-stu-id="a0524-149">Additional Azure BizTalk Services topics:</span></span>

* [<span data-ttu-id="a0524-150">Lors de l’installation Bonjour Azure BizTalk Services SDK</span><span class="sxs-lookup"><span data-stu-id="a0524-150">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="a0524-151">Didacticiels : Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="a0524-151">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="a0524-152">Comment puis-je démarrer à l’aide de hello SDK des Services BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="a0524-152">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="a0524-153">Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="a0524-153">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="a0524-154">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a0524-154">See Also</span></span>
* [<span data-ttu-id="a0524-155">Comment : utiliser le Service Gestion des services ACS tooConfigure identités de Service</span><span class="sxs-lookup"><span data-stu-id="a0524-155">How to: Use ACS Management Service tooConfigure Service Identities</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [<span data-ttu-id="a0524-156">Tableau comparatif des éditions Développeur, De base, Standard et Premium de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="a0524-156">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="a0524-157">BizTalk Services : approvisionnement à l’aide du portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="a0524-157">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="a0524-158">Tableau comparatif des états d'approvisionnement BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="a0524-158">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="a0524-159">Onglets Tableau de bord, Surveiller et Mettre à l'échelle dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="a0524-159">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="a0524-160">Sauvegarde et restauration de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="a0524-160">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="a0524-161">Limitation dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="a0524-161">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

