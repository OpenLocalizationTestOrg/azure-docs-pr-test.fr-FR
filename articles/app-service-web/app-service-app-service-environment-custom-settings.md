---
title: "paramètres d’aaaCustom pour les environnements de Service d’application"
description: "Paramètres de configuration personnalisés pour les environnements App Service"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 1d1d85f3-6cc6-4d57-ae1a-5b37c642d812
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2016
ms.author: stefsch
ms.openlocfilehash: 3d140688c88b389e71bfdd465c418339cccab3a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="8ee1d-103">Paramètres de configuration personnalisés pour les environnements App Service</span><span class="sxs-lookup"><span data-stu-id="8ee1d-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="8ee1d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="8ee1d-104">Overview</span></span>
<span data-ttu-id="8ee1d-105">Environnements de Service d’application étant tooa isolé un seul client, il existe certains des paramètres de configuration qui peuvent être appliqués tooApp exclusivement les environnements de Service.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-105">Because App Service Environments are isolated tooa single customer, there are certain configuration settings that can be applied exclusively tooApp Service Environments.</span></span> <span data-ttu-id="8ee1d-106">Ce article les documents hello différentes personnalisations spécifiques qui sont disponibles pour les environnements de Service d’application.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-106">This article documents hello various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="8ee1d-107">Si vous n’avez pas d’un environnement App Service, consultez [comment tooCreate un environnement App Service](app-service-web-how-to-create-an-app-service-environment.md).</span><span class="sxs-lookup"><span data-stu-id="8ee1d-107">If you do not have an App Service Environment, see [How tooCreate an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="8ee1d-108">Vous pouvez stocker les personnalisations de l’environnement App Service en utilisant un tableau Bonjour nouvelle **clusterSettings** attribut.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-108">You can store App Service Environment customizations by using an array in hello new **clusterSettings** attribute.</span></span> <span data-ttu-id="8ee1d-109">Cet attribut est trouvé dans le dictionnaire de « Propriétés » hello Hello *hostingEnvironments* entité d’Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-109">This attribute is found in hello "Properties" dictionary of hello *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="8ee1d-110">Hello abrégé Gestionnaire de ressources du modèle extrait de code suivant montre hello **clusterSettings** attribut :</span><span class="sxs-lookup"><span data-stu-id="8ee1d-110">hello following abbreviated Resource Manager template snippet shows hello **clusterSettings** attribute:</span></span>

    "resources": [
    {
       "apiVersion": "2015-08-01",
       "type": "Microsoft.Web/hostingEnvironments",
       "name": ...,
       "location": ...,
       "properties": {
          "clusterSettings": [
             {
                 "name": "nameOfCustomSetting",
                 "value": "valueOfCustomSetting"
             }
          ],
          "workerPools": [ ...],
          etc...
       }
    }

<span data-ttu-id="8ee1d-111">Hello **clusterSettings** attribut peut être inclus dans un Bonjour de tooupdate de modèle de gestionnaire de ressources environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-111">hello **clusterSettings** attribute can be included in a Resource Manager template tooupdate hello App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-tooupdate-an-app-service-environment"></a><span data-ttu-id="8ee1d-112">Utilisez l’Explorateur de ressources Azure tooupdate un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="8ee1d-112">Use Azure Resource Explorer tooupdate an App Service Environment</span></span>
<span data-ttu-id="8ee1d-113">Ou bien, vous pouvez mettre à jour hello environnement App Service à l’aide de [Explorateur de ressources Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8ee1d-113">Alternatively, you can update hello App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="8ee1d-114">Dans l’Explorateur de ressources, accédez au nœud toohello hello environnement App Service (**abonnements** > **resourceGroups** > **fournisseurs**  >  **Microsoft.Web** > **hostingEnvironments**).</span><span class="sxs-lookup"><span data-stu-id="8ee1d-114">In Resource Explorer, go toohello node for hello App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="8ee1d-115">Puis cliquez sur hello environnement App Service spécifique que vous souhaitez tooupdate.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-115">Then click hello specific App Service Environment that you want tooupdate.</span></span>
2. <span data-ttu-id="8ee1d-116">Dans le volet droit de hello, cliquez sur **en lecture/écriture** dans tooallow de barre d’outils supérieure hello interactif de modification dans l’Explorateur de ressources.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-116">In hello right pane, click **Read/Write** in hello upper toolbar tooallow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="8ee1d-117">Cliquez sur hello bleu **modifier** modifiable de modèle de gestionnaire de ressources du hello toomake bouton.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-117">Click hello blue **Edit** button toomake hello Resource Manager template editable.</span></span>
4. <span data-ttu-id="8ee1d-118">Défilement vers le bas toohello du volet de droite hello.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-118">Scroll toohello bottom of hello right pane.</span></span> <span data-ttu-id="8ee1d-119">Hello **clusterSettings** attribut est à hello tout en bas, où vous pouvez entrer ou mettre à jour sa valeur.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-119">hello **clusterSettings** attribute is at hello very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="8ee1d-120">Tableau de hello type (ou copier et coller) de valeurs de configuration souhaitée dans hello **clusterSettings** attribut.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-120">Type (or copy and paste) hello array of configuration values you want in hello **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="8ee1d-121">Cliquez sur hello verte **PUT** bouton qui est située en haut de hello de hello volet droit toocommit hello modification toohello environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-121">Click hello green **PUT** button that's located at hello top of hello right pane toocommit hello change toohello App Service Environment.</span></span>

<span data-ttu-id="8ee1d-122">Toutefois, vous envoyez la modification de hello, dure environ 30 minutes pour multiplié par nombre de hello de frontaux Bonjour environnement App Service pour modifier un effet de tootake hello.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-122">However you submit hello change, it takes roughly 30 minutes multiplied by hello number of front ends in hello App Service Environment for hello change tootake effect.</span></span>
<span data-ttu-id="8ee1d-123">Par exemple, si un environnement App Service a quatre frontaux, il prendra environ deux heures pour toofinish de mise à jour de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for hello configuration update toofinish.</span></span> <span data-ttu-id="8ee1d-124">Lors de la modification de la configuration hello est déployée, aucune autre mise à l’échelle des opérations ou des opérations de modification de configuration ne peuvent avoir lieu dans hello environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-124">While hello configuration change is being rolled out, no other scaling operations or configuration change operations can take place in hello App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="8ee1d-125">Désactivation de TLS 1.0</span><span class="sxs-lookup"><span data-stu-id="8ee1d-125">Disable TLS 1.0</span></span>
<span data-ttu-id="8ee1d-126">Une question récurrente de clients, notamment les clients qui traitent avec mise en conformité PCI audits, est comment tooexplicitly désactiver TLS 1.0 pour leurs applications.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how tooexplicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="8ee1d-127">TLS 1.0 peut être désactivé via les éléments suivants de hello **clusterSettings** entrée :</span><span class="sxs-lookup"><span data-stu-id="8ee1d-127">TLS 1.0 can be disabled through hello following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="8ee1d-128">Modifier l’ordre des suites de chiffrement TLS</span><span class="sxs-lookup"><span data-stu-id="8ee1d-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="8ee1d-129">Une autre question à partir de clients est si ils peuvent modifier la liste de hello de chiffrements négocié par leur serveur et que cela est possible en modifiant hello **clusterSettings** comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-129">Another question from customers is if they can modify hello list of ciphers negotiated by their server and this can be achieved by modifying hello **clusterSettings** as shown below.</span></span> <span data-ttu-id="8ee1d-130">liste de Hello des suites de chiffrement disponibles peut être récupérée à partir de [cet article MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="8ee1d-130">hello list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="8ee1d-131">Si des valeurs incorrectes sont définies pour la suite de chiffrement de hello SChannel ne peut pas comprendre, tous les serveurs de tooyour communication TLS peuvent cesser de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-131">If incorrect values are set for hello cipher suite that SChannel cannot understand, all TLS communication tooyour server might stop functioning.</span></span> <span data-ttu-id="8ee1d-132">Dans ce cas, vous devez tooremove hello *FrontEndSSLCipherSuiteOrder* entrée à partir de **clusterSettings** et envoyer hello mis à jour le Gestionnaire de ressources du modèle toorevert toohello différé par défaut chiffrement paramètres de la suite.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-132">In such a case, you will need tooremove hello *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit hello updated Resource Manager template toorevert back toohello default cipher suite settings.</span></span>  <span data-ttu-id="8ee1d-133">Utilisez cette fonctionnalité avec précaution.</span><span class="sxs-lookup"><span data-stu-id="8ee1d-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="8ee1d-134">Prise en main</span><span class="sxs-lookup"><span data-stu-id="8ee1d-134">Get started</span></span>
<span data-ttu-id="8ee1d-135">site de modèle de gestionnaire de ressources du démarrage rapide Azure Hello comprend un modèle avec la définition de base hello pour [création d’un environnement App Service](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span><span class="sxs-lookup"><span data-stu-id="8ee1d-135">hello Azure Quickstart Resource Manager template site includes a template with hello base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
