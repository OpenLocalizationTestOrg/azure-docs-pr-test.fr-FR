---
title: "Créer un conteneur de service cloud avec PowerShell | Microsoft Docs"
description: "Cet article explique comment créer un conteneur de service cloud avec PowerShell. Le conteneur héberge les rôles Web et de travail."
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
ms.openlocfilehash: 2023fa7b318f9f76ce1e1ea0a46110297be9a001
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-an-azure-powershell-command-to-create-an-empty-cloud-service-container"></a><span data-ttu-id="5893e-104">Utiliser une commande Azure PowerShell pour créer un conteneur de service cloud vide</span><span class="sxs-lookup"><span data-stu-id="5893e-104">Use an Azure PowerShell command to create an empty cloud service container</span></span>
<span data-ttu-id="5893e-105">Cet article explique comment créer rapidement un conteneur Cloud Services à l’aide d’applets de commande Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5893e-105">This article explains how to quickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="5893e-106">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="5893e-106">Please follow the steps below:</span></span>

1. <span data-ttu-id="5893e-107">Installez l’applet de commande Microsoft Azure PowerShell à partir de la page [Téléchargements d’Azure PowerShell](http://aka.ms/webpi-azps) .</span><span class="sxs-lookup"><span data-stu-id="5893e-107">Install the Microsoft Azure PowerShell cmdlet from the [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="5893e-108">Ouvrez l’invite de commandes PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5893e-108">Open the PowerShell command prompt.</span></span>
3. <span data-ttu-id="5893e-109">Utilisez l’applet de commande [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="5893e-109">Use the [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) to sign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5893e-110">Pour obtenir des instructions complémentaires sur l’installation de l’applet de commande Azure PowerShell et sur la connexion à votre abonnement Azure, consultez l’article [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5893e-110">For further instruction on installing the Azure PowerShell cmdlet and connecting to your Azure subscription, refer to [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="5893e-111">Créez un conteneur de service cloud Azure vide à l’aide de l’applet de commande **New-AzureService** .</span><span class="sxs-lookup"><span data-stu-id="5893e-111">Use the **New-AzureService** cmdlet to create an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="5893e-112">Suivez cet exemple pour appeler l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="5893e-112">Follow this example to invoke the cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="5893e-113">Pour plus d’informations sur la création du service cloud Azure, exécutez :</span><span class="sxs-lookup"><span data-stu-id="5893e-113">For more information about creating the Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="5893e-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5893e-114">Next steps</span></span>
* <span data-ttu-id="5893e-115">Pour gérer le déploiement du service cloud, reportez-vous aux rubriques relatives aux commandes [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx) et [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx).</span><span class="sxs-lookup"><span data-stu-id="5893e-115">To manage the cloud service deployment, refer to the [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="5893e-116">Pour plus d’informations, vous pouvez également consulter l’article [Configuration des services cloud](cloud-services-how-to-configure.md) .</span><span class="sxs-lookup"><span data-stu-id="5893e-116">You may also refer to [How to configure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="5893e-117">Pour publier votre projet de service cloud dans Azure, consultez l’exemple de code **PublishCloudService.ps1** dans l’article [Livraison continue du service cloud dans Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="5893e-117">To publish your cloud service project to Azure, refer to the  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
