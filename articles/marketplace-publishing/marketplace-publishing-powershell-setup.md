---
title: aaaSet des PowerShell toocreate une machine virtuelle pour hello Marketplace | Documents Microsoft
description: "Instructions pour configurer Azure PowerShell et l’utiliser comme un processus facultatif toodeploy d’images de machine virtuelle toocreate, de flux et vendent sur, hello Azure Marketplace"
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
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a><span data-ttu-id="cabd7-103">Configurer Azure PowerShell toocreate offre hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="cabd7-103">Set up Azure PowerShell toocreate an offer for hello Azure Marketplace</span></span>
<span data-ttu-id="cabd7-104">Pour plus d’informations sur la façon de tooset de PowerShell dans Azure, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cabd7-104">For detailed information on how tooset up PowerShell in Azure, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="cabd7-105">Une approche simple est la méthode certificat toouse hello, qui télécharge et importe un certificat nécessaire pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="cabd7-105">A simple approach is toouse hello certificate method, which downloads and imports a certificate needed for authentication.</span></span> <span data-ttu-id="cabd7-106">tooobtain hello nécessaire de certificat, utilisez hello **Get-AzurePublishSettingsFile** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cabd7-106">tooobtain hello needed certificate, use hello **Get-AzurePublishSettingsFile** cmdlet.</span></span> <span data-ttu-id="cabd7-107">Enregistrer le fichier de hello lorsque vous êtes invité.</span><span class="sxs-lookup"><span data-stu-id="cabd7-107">Save hello file when you're prompted.</span></span> <span data-ttu-id="cabd7-108">certificat de hello tooimport dans une session PowerShell, utilisez hello **Import-AzurePublishSettingsFile** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cabd7-108">tooimport hello certificate into a PowerShell session, use hello **Import-AzurePublishSettingsFile** cmdlet.</span></span>

<span data-ttu-id="cabd7-109">tooconfigure et magasin hello commune Microsoft Azure paramètres d’abonnement pour la session de PowerShell hello, utiliser hello **Set-AzureSubscription** et **Select-AzureSubscription** applets de commande :</span><span class="sxs-lookup"><span data-stu-id="cabd7-109">tooconfigure and store hello common Microsoft Azure subscription settings for hello PowerShell session, use hello **Set-AzureSubscription** and **Select-AzureSubscription** cmdlets:</span></span>

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

<span data-ttu-id="cabd7-110">commande premier Hello associe un compte de stockage par défaut abonnement hello (nécessaire pour certaines opérations de configuration de machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="cabd7-110">hello first command associates a default storage account with hello subscription (needed for some VM provisioning operations).</span></span>  <span data-ttu-id="cabd7-111">Hello effectue ensuite les abonnement hello hello celui en cours (reconnu par les autres applets de commande).</span><span class="sxs-lookup"><span data-stu-id="cabd7-111">hello second makes hello subscription hello current one (recognized by other cmdlets).</span></span>

## <a name="see-also"></a><span data-ttu-id="cabd7-112">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="cabd7-112">See also</span></span>
* [<span data-ttu-id="cabd7-113">Mise en route : comment toopublish une toohello offre Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="cabd7-113">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* [<span data-ttu-id="cabd7-114">Création d’une image de machine virtuelle pour hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="cabd7-114">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)

