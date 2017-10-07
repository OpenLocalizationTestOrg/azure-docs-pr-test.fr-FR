---
title: aaaScale un service cloud Azure dans Windows PowerShell | Documents Microsoft
description: "(classique) Découvrez comment toouse PowerShell tooscale un rôle web ou un rôle de travail ou arrière dans Azure."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a>Comment tooscale un cloud service dans PowerShell

Vous pouvez utiliser Windows PowerShell tooscale un rôle web ou un rôle de travail ou en ajoutant ou supprimant des instances.  

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Avant de pouvoir effectuer des opérations sur votre abonnement via PowerShell, vous devez vous connecter :

```powershell
Add-AzureAccount
```

Si vous avez plusieurs abonnements associés à votre compte, vous devrez peut-être toochange hello abonnement en fonction de l’emplacement de votre service cloud. toocheck hello abonnement actuel exécuter :

```powershell
Get-AzureSubscription -Current
```

Si vous avez besoin d’abonnement toochange hello, exécutez :

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a>Vérifier le nombre d’instances actuelles hello pour votre rôle.

état actuel de hello toocheck de votre rôle, exécutez :

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

Vous devez obtenir des informations sur le rôle hello, y compris son décompte de version et l’instance actuelle du système d’exploitation. Dans ce cas, le rôle de hello a une seule instance.

![Plus d’informations sur le rôle de hello](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a>Rôle de hello faire évoluer en ajoutant plusieurs instances

tooscale à votre rôle, passe hello nombre souhaité d’instances comme hello **nombre** paramètre toohello **Set-AzureRole** applet de commande :

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

blocs d’applet de commande Hello momentanément lors de nouvelles instances de hello sont configurés et démarrés. Pendant ce temps, si vous ouvrez une nouvelle fenêtre PowerShell et appel **Get-AzureRole** comme indiqué précédemment, vous verrez le nombre d’instances hello nouvelle cible. Et si vous Inspectez le statut du rôle hello dans le portail de hello, vous devez voir hello nouvelle instance démarre :

![Instance de machine virtuelle en cours de démarrage dans le portail](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

Une fois les nouvelles instances de hello ont démarré, applet de commande hello retournera correctement :

![Augmentation du nombre d’instances du rôle réussie](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a>Mettre à l’échelle dans le rôle de hello en supprimant des instances

Vous pouvez faire évoluer dans un rôle en supprimant des instances de hello identique. Ensemble hello **nombre** paramètre sur **Set-AzureRole** toohello nombre d’instances souhaitées toohave après la mise à l’échelle de hello dans l’opération est terminée.

## <a name="next-steps"></a>Étapes suivantes

Il n’est pas possible de tooconfigure à l’échelle automatique pour les services de cloud à partir de PowerShell. toodo qui, consultez [comment tooauto l’échelle un service cloud](cloud-services-how-to-scale-portal.md).
