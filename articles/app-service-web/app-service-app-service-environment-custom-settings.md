---
title: "Paramètres personnalisés pour les environnements App Service"
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
ms.openlocfilehash: 687475fae0c90713c15e8abbb92b71059eae81c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="custom-configuration-settings-for-app-service-environments"></a><span data-ttu-id="ab965-103">Paramètres de configuration personnalisés pour les environnements App Service</span><span class="sxs-lookup"><span data-stu-id="ab965-103">Custom configuration settings for App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="ab965-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ab965-104">Overview</span></span>
<span data-ttu-id="ab965-105">Les environnements App Service étant isolés pour chaque client, certains paramètres de configuration peuvent être appliqués exclusivement à des environnements App Service.</span><span class="sxs-lookup"><span data-stu-id="ab965-105">Because App Service Environments are isolated to a single customer, there are certain configuration settings that can be applied exclusively to App Service Environments.</span></span> <span data-ttu-id="ab965-106">Cet article décrit les différentes personnalisations pour les environnements App Service disponibles.</span><span class="sxs-lookup"><span data-stu-id="ab965-106">This article documents the various specific customizations that are available for App Service Environments.</span></span>

<span data-ttu-id="ab965-107">Si vous ne possédez pas d’environnement App Service, voir [Comment créer un environnement App Service](app-service-web-how-to-create-an-app-service-environment.md).</span><span class="sxs-lookup"><span data-stu-id="ab965-107">If you do not have an App Service Environment, see [How to Create an App Service Environment](app-service-web-how-to-create-an-app-service-environment.md).</span></span>

<span data-ttu-id="ab965-108">Vous pouvez stocker les personnalisations de l’environnement App Service (App Service Environment) à l’aide d’un tableau dans le nouvel attribut **clusterSettings** .</span><span class="sxs-lookup"><span data-stu-id="ab965-108">You can store App Service Environment customizations by using an array in the new **clusterSettings** attribute.</span></span> <span data-ttu-id="ab965-109">Cet attribut se trouve dans le dictionnaire des « Propriétés » de l’entité Azure Resource Manager *hostingEnvironments* .</span><span class="sxs-lookup"><span data-stu-id="ab965-109">This attribute is found in the "Properties" dictionary of the *hostingEnvironments* Azure Resource Manager entity.</span></span>

<span data-ttu-id="ab965-110">L’extrait de code abrégé de modèle Resource Manager suivant indique l’attribut **clusterSettings** :</span><span class="sxs-lookup"><span data-stu-id="ab965-110">The following abbreviated Resource Manager template snippet shows the **clusterSettings** attribute:</span></span>

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

<span data-ttu-id="ab965-111">L’attribut **clusterSettings** peut être inclus dans un modèle Resource Manager pour mettre à jour l’environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="ab965-111">The **clusterSettings** attribute can be included in a Resource Manager template to update the App Service Environment.</span></span>

## <a name="use-azure-resource-explorer-to-update-an-app-service-environment"></a><span data-ttu-id="ab965-112">Utilisation de l’Explorateur de ressources Azure pour mettre à jour un environnement App Service</span><span class="sxs-lookup"><span data-stu-id="ab965-112">Use Azure Resource Explorer to update an App Service Environment</span></span>
<span data-ttu-id="ab965-113">Vous pouvez également mettre à jour l’environnement App Service à l’aide de [l’Explorateur de ressources Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ab965-113">Alternatively, you can update the App Service Environment by using [Azure Resource Explorer](https://resources.azure.com).</span></span>  

1. <span data-ttu-id="ab965-114">Dans l’Explorateur de ressources, accédez au nœud de l’environnement App Service (**abonnements** > **resourceGroups** > **fournisseurs** > **Microsoft.Web** > **hostingEnvironments**).</span><span class="sxs-lookup"><span data-stu-id="ab965-114">In Resource Explorer, go to the node for the App Service Environment (**subscriptions** > **resourceGroups** > **providers** > **Microsoft.Web** > **hostingEnvironments**).</span></span> <span data-ttu-id="ab965-115">Cliquez ensuite sur l’environnement App Service spécifique que vous souhaitez mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="ab965-115">Then click the specific App Service Environment that you want to update.</span></span>
2. <span data-ttu-id="ab965-116">Dans le volet de droite, cliquez sur **Lecture/écriture** dans la barre d’outils du haut pour autoriser la modification interactive dans l’Explorateur de ressources.</span><span class="sxs-lookup"><span data-stu-id="ab965-116">In the right pane, click **Read/Write** in the upper toolbar to allow interactive editing in Resource Explorer.</span></span>  
3. <span data-ttu-id="ab965-117">Cliquez sur le bouton bleu **Modifier** pour permettre la modification du modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ab965-117">Click the blue **Edit** button to make the Resource Manager template editable.</span></span>
4. <span data-ttu-id="ab965-118">Faites défiler jusqu'au bas du panneau de droite.</span><span class="sxs-lookup"><span data-stu-id="ab965-118">Scroll to the bottom of the right pane.</span></span> <span data-ttu-id="ab965-119">L’attribut **clusterSettings** , dont vous pouvez entrer ou mettre à jour la valeur, se trouve tout en bas.</span><span class="sxs-lookup"><span data-stu-id="ab965-119">The **clusterSettings** attribute is at the very bottom, where you can enter or update its value.</span></span>
5. <span data-ttu-id="ab965-120">Entrez (ou copiez et collez) le tableau de valeurs de configuration souhaité dans l’attribut **clusterSettings** .</span><span class="sxs-lookup"><span data-stu-id="ab965-120">Type (or copy and paste) the array of configuration values you want in the **clusterSettings** attribute.</span></span>  
6. <span data-ttu-id="ab965-121">Cliquez sur le bouton vert **PUT** situé en haut du panneau de droite pour valider la modification apportée à l’environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="ab965-121">Click the green **PUT** button that's located at the top of the right pane to commit the change to the App Service Environment.</span></span>

<span data-ttu-id="ab965-122">Quelle que soit la manière dont vous soumettez les modifications, environ 30 minutes (multipliées par le nombre de serveurs frontaux présents dans l’environnement App Service) pour qu’elles prennent effet.</span><span class="sxs-lookup"><span data-stu-id="ab965-122">However you submit the change, it takes roughly 30 minutes multiplied by the number of front ends in the App Service Environment for the change to take effect.</span></span>
<span data-ttu-id="ab965-123">Par exemple, si un environnement App Service a quatre serveurs frontaux, la mise à jour de la configuration prendra environ deux heures.</span><span class="sxs-lookup"><span data-stu-id="ab965-123">For example, if an App Service Environment has four front ends, it will take roughly two hours for the configuration update to finish.</span></span> <span data-ttu-id="ab965-124">Tant que la modification de la configuration n’est pas déployée, aucune autre opération de mise à l’échelle ou de modification de configuration n’est possible dans l’environnement App Service.</span><span class="sxs-lookup"><span data-stu-id="ab965-124">While the configuration change is being rolled out, no other scaling operations or configuration change operations can take place in the App Service Environment.</span></span>

## <a name="disable-tls-10"></a><span data-ttu-id="ab965-125">Désactivation de TLS 1.0</span><span class="sxs-lookup"><span data-stu-id="ab965-125">Disable TLS 1.0</span></span>
<span data-ttu-id="ab965-126">Il est fréquent que des clients, en particulier ceux faisant l’objet d’audits de conformité PCI, demandent à ce qu’il soit possible de désactiver explicitement TLS 1.0 pour leurs applications.</span><span class="sxs-lookup"><span data-stu-id="ab965-126">A recurring question from customers, especially customers who are dealing with PCI compliance audits, is how to explicitly disable TLS 1.0 for their apps.</span></span>

<span data-ttu-id="ab965-127">TLS 1.0 peut être désactivé par le biais de l’entrée **clusterSettings** suivante :</span><span class="sxs-lookup"><span data-stu-id="ab965-127">TLS 1.0 can be disabled through the following **clusterSettings** entry:</span></span>

        "clusterSettings": [
            {
                "name": "DisableTls1.0",
                "value": "1"
            }
        ],

## <a name="change-tls-cipher-suite-order"></a><span data-ttu-id="ab965-128">Modifier l’ordre des suites de chiffrement TLS</span><span class="sxs-lookup"><span data-stu-id="ab965-128">Change TLS cipher suite order</span></span>
<span data-ttu-id="ab965-129">Les clients demandent également s’ils peuvent modifier la liste des chiffrements négociés par leur serveur. Ils peuvent le faire en modifiant l’attribut **clusterSettings** comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ab965-129">Another question from customers is if they can modify the list of ciphers negotiated by their server and this can be achieved by modifying the **clusterSettings** as shown below.</span></span> <span data-ttu-id="ab965-130">Vous trouverez la liste des suites de chiffrement disponibles dans [cet article MSDN](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span><span class="sxs-lookup"><span data-stu-id="ab965-130">The list of cipher suites available can be retrieved from [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa374757\(v=vs.85\).aspx).</span></span>

        "clusterSettings": [
            {
                "name": "FrontEndSSLCipherSuiteOrder",
                "value": "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384_P256,TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256,TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256"
            }
        ],

> [!WARNING]
> <span data-ttu-id="ab965-131">Si des valeurs incorrectes sont définies pour la suite de chiffrement et incompréhensibles pour SChannel, l’ensemble de la communication TLS avec votre serveur peut cesser de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="ab965-131">If incorrect values are set for the cipher suite that SChannel cannot understand, all TLS communication to your server might stop functioning.</span></span> <span data-ttu-id="ab965-132">Dans ce cas, vous devrez supprimer l’entrée *FrontEndSSLCipherSuiteOrder* des **clusterSettings** et envoyer le modèle Resource Manager mis à jour pour rétablir les paramètres de suite de chiffrement par défaut.</span><span class="sxs-lookup"><span data-stu-id="ab965-132">In such a case, you will need to remove the *FrontEndSSLCipherSuiteOrder* entry from **clusterSettings** and submit the updated Resource Manager template to revert back to the default cipher suite settings.</span></span>  <span data-ttu-id="ab965-133">Utilisez cette fonctionnalité avec précaution.</span><span class="sxs-lookup"><span data-stu-id="ab965-133">Please use this functionality with caution.</span></span>
> 
> 

## <a name="get-started"></a><span data-ttu-id="ab965-134">Prise en main</span><span class="sxs-lookup"><span data-stu-id="ab965-134">Get started</span></span>
<span data-ttu-id="ab965-135">Le site de modèles Azure Quickstart Resource Manager comprend un modèle dont la définition de base permet de [créer un environnement App Service](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span><span class="sxs-lookup"><span data-stu-id="ab965-135">The Azure Quickstart Resource Manager template site includes a template with the base definition for [creating an App Service Environment](https://azure.microsoft.com/documentation/templates/201-web-app-ase-create/).</span></span>

<!-- LINKS -->

<!-- IMAGES -->
