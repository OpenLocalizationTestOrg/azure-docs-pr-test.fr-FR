---
title: aaaCreate un conteneur de service cloud avec PowerShell | Documents Microsoft
description: "Cet article explique comment toocreate un cloud service conteneur avec PowerShell. conteneur de Hello héberge les rôles web et worker."
services: cloud-services
documentationcenter: .net
author: cawaMS
manager: timlt
editor: 
ms.assetid: c8f32469-610e-4f37-a3aa-4fac5c714e13
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 4c47b10b5ba1f9cc39594a45cd869bf04fcaadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a><span data-ttu-id="0637c-104">Utilisez un toocreate de commande Azure PowerShell un conteneur de service cloud vide</span><span class="sxs-lookup"><span data-stu-id="0637c-104">Use an Azure PowerShell command toocreate an empty cloud service container</span></span>
<span data-ttu-id="0637c-105">Cet article explique comment tooquickly créer un conteneur de Services de cloud computing à l’aide des applets de commande PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="0637c-105">This article explains how tooquickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="0637c-106">Suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0637c-106">Please follow hello steps below:</span></span>

1. <span data-ttu-id="0637c-107">Installer l’applet de commande PowerShell de Microsoft Azure hello de hello [Azure PowerShell télécharge](http://aka.ms/webpi-azps) page.</span><span class="sxs-lookup"><span data-stu-id="0637c-107">Install hello Microsoft Azure PowerShell cmdlet from hello [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="0637c-108">Ouvrez l’invite de commandes PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="0637c-108">Open hello PowerShell command prompt.</span></span>
3. <span data-ttu-id="0637c-109">Hello d’utilisation [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign dans.</span><span class="sxs-lookup"><span data-stu-id="0637c-109">Use hello [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0637c-110">Pour obtenir des instructions supplémentaires sur l’installation d’applet de commande PowerShell Azure hello et la connexion tooyour abonnement Azure, consultez trop[comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0637c-110">For further instruction on installing hello Azure PowerShell cmdlet and connecting tooyour Azure subscription, refer too[How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="0637c-111">Hello d’utilisation **New-AzureService** toocreate de l’applet de commande un conteneur de service cloud Azure vide.</span><span class="sxs-lookup"><span data-stu-id="0637c-111">Use hello **New-AzureService** cmdlet toocreate an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="0637c-112">Suivez cette applet de commande hello de tooinvoke exemple :</span><span class="sxs-lookup"><span data-stu-id="0637c-112">Follow this example tooinvoke hello cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="0637c-113">Pour plus d’informations sur la création de service de cloud Azure hello, exécutez :</span><span class="sxs-lookup"><span data-stu-id="0637c-113">For more information about creating hello Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="0637c-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0637c-114">Next steps</span></span>
* <span data-ttu-id="0637c-115">toomanage hello déploiement du service cloud, consultez le toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), et [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commandes.</span><span class="sxs-lookup"><span data-stu-id="0637c-115">toomanage hello cloud service deployment, refer toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="0637c-116">Vous pouvez également faire référence trop[tooconfigure de services cloud](cloud-services-how-to-configure.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="0637c-116">You may also refer too[How tooconfigure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="0637c-117">toopublish votre service cloud tooAzure de projet, consultez le toohello **PublishCloudService.ps1** exemple de code à partir de [livraison continue pour le service cloud dans Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="0637c-117">toopublish your cloud service project tooAzure, refer toohello  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
