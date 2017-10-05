---
title: "Configuration de PowerShell pour créer une machine virtuelle pour Marketplace | Microsoft Docs"
description: "Instructions pour configurer Azure PowerShell et l’utiliser comme processus facultatif pour créer des images de machines virtuelles à déployer et à vendre sur Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: bbcce5093d2bbd5326523063db7d0e565fe4de6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-azure-powershell-to-create-an-offer-for-the-azure-marketplace"></a><span data-ttu-id="cd045-103">Configurer Azure PowerShell pour créer une offre pour Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="cd045-103">Set up Azure PowerShell to create an offer for the Azure Marketplace</span></span>
<span data-ttu-id="cd045-104">Pour plus d’informations sur la configuration de PowerShell dans Azure, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cd045-104">For detailed information on how to set up PowerShell in Azure, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="cd045-105">Une approche simple consiste à utiliser la méthode de certificat, qui télécharge et importe le certificat nécessaire à l’authentification.</span><span class="sxs-lookup"><span data-stu-id="cd045-105">A simple approach is to use the certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="cd045-106">Pour obtenir le certificat requis, utilisez l’applet de commande **Get-AzurePublishSettingsFile** .</span><span class="sxs-lookup"><span data-stu-id="cd045-106">To obtain the needed certificate, use the **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="cd045-107">Enregistrez le fichier lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="cd045-107">Save the file when you're prompted.</span></span> <span data-ttu-id="cd045-108">Pour importer le certificat dans une session PowerShell, utilisez l’applet de commande **Import-AzurePublishSettingsFile** .</span><span class="sxs-lookup"><span data-stu-id="cd045-108">To import the certificate into a PowerShell session, use the **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="cd045-109">Pour configurer et stocker les paramètres d’abonnement Microsoft Azure communs pour la session PowerShell, utilisez les applets de commande **Set-AzureSubscription** et **Select-AzureSubscription** :</span><span class="sxs-lookup"><span data-stu-id="cd045-109">To configure and store the common Microsoft Azure subscription settings for the PowerShell session, use the **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="cd045-110">La première commande associe un compte de stockage par défaut à l’abonnement (nécessaire pour certaines opérations d’approvisionnement de la machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="cd045-110">The first command associates a default storage account with the subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="cd045-111">La seconde définit l’abonnement comme abonnement actif (reconnu par les autres applets de commande).</span><span class="sxs-lookup"><span data-stu-id="cd045-111">The second makes the subscription the current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="cd045-112">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="cd045-112">See also</span></span>
* [<span data-ttu-id="cd045-113">Mise en route : publication d’une offre dans Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="cd045-113">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="cd045-114">Création d’une image de machine virtuelle pour Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="cd045-114">Creating a virtual machine image for the Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

