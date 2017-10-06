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
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a>Utilisez un toocreate de commande Azure PowerShell un conteneur de service cloud vide
Cet article explique comment tooquickly créer un conteneur de Services de cloud computing à l’aide des applets de commande PowerShell de Azure. Suivez les étapes de hello ci-dessous :

1. Installer l’applet de commande PowerShell de Microsoft Azure hello de hello [Azure PowerShell télécharge](http://aka.ms/webpi-azps) page.
2. Ouvrez l’invite de commandes PowerShell hello.
3. Hello d’utilisation [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign dans.

   > [!NOTE]
   > Pour obtenir des instructions supplémentaires sur l’installation d’applet de commande PowerShell Azure hello et la connexion tooyour abonnement Azure, consultez trop[comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).
   >
   >
4. Hello d’utilisation **New-AzureService** toocreate de l’applet de commande un conteneur de service cloud Azure vide.

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. Suivez cette applet de commande hello de tooinvoke exemple :

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

Pour plus d’informations sur la création de service de cloud Azure hello, exécutez :

```
Get-help New-AzureService
```

### <a name="next-steps"></a>Étapes suivantes
* toomanage hello déploiement du service cloud, consultez le toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), et [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commandes. Vous pouvez également faire référence trop[tooconfigure de services cloud](cloud-services-how-to-configure.md) pour plus d’informations.
* toopublish votre service cloud tooAzure de projet, consultez le toohello **PublishCloudService.ps1** exemple de code à partir de [livraison continue pour le service cloud dans Azure](cloud-services-dotnet-continuous-delivery.md).
