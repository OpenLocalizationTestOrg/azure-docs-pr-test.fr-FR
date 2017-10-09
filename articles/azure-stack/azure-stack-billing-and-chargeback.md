---
title: "aaaCustomer de facturation et de rétrofacturation dans Azure pile | Documents Microsoft"
description: "Découvrez comment tooretrieve l’utilisation des informations sur les ressources Azure pile."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: a9afc7b6-43da-437b-a853-aab73ff14113
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2016
ms.author: alfredop
ms.openlocfilehash: d92caac2874e5364870b29a38515b579ab059991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-and-billing-in-azure-stack"></a>Utilisation et facturation dans Azure Stack

L’utilisation de représente la quantité hello des ressources consommées par un utilisateur. Pile Azure recueille des informations d’utilisation pour chaque utilisateur et les utilise toobill les. Cet article décrit la façon dont les utilisateurs de la pile de Azure sont facturées pour l’utilisation des ressources, et l’accès à des informations de facturation hello pour analytique, rétrofacturation, etc..

Pile Azure contient hello infrastructure toocollect et les données d’utilisation d’agrégation de toutes les ressources. Vous pouvez accéder à ces données et système de facturation tooa l’exporter à l’aide d’un adaptateur de facturation ou exportez-le tooa un outil décisionnel comme Microsoft Power BI. Après l’exportation, ces informations de facturation sont utilisées pour l’analytique ou transférés tooa rétrofacturation système.

![Modèle conceptuel d’un adaptateur de facturation connexion Azure pile tooa application de facturation](media/azure-stack-billing-and-chargeback/image1.png)

## <a name="what-usage-information-can-i-find-and-how"></a>Quelles informations d’utilisation puis-je trouver et comment ?

Les fournisseurs de ressources Azure Stack, comme Calcul, Stockage et Réseau, génèrent des données d’utilisation toutes les heures pour chaque abonnement. les données d’utilisation Hello contient plus d’informations sur la ressource hello utilisé comme nom de la ressource, de la quantité de nom, ID de la jauge, compteur utilisé toolearn etc. sur les ressources de code hello mètres, consultez toohello [API Forum aux questions sur l’utilisation de](azure-stack-usage-related-faq.md) l’article. 

Une fois les données d’utilisation hello ont été collectées, il est [signalé tooAzure](azure-stack-usage-reporting.md) toogenerate une facture, ce qui peut être affichée via hello portail de facturation Azure. Hello portail de facturation Azure les données d’utilisation de hello uniquement pour les ressources facturables hello. En outre ressources facturables toohello, Azure pile capture les données d’utilisation pour un ensemble plus large de ressources, auquel vous pouvez accéder dans votre environnement Azure pile via l’API REST ou PowerShell. Azure pile cloud les administrateurs peuvent récupérer les données d’utilisation hello pour tous les abonnements de l’utilisateur qu’un utilisateur peut obtenir uniquement les détails d’utilisation.

## <a name="retrieve-usage-information"></a>Récupérer les informations sur l’utilisation

données d’utilisation toogenerate hello, vous devez disposer de ressources qui sont en cours d’exécution et activement à l’aide de système de hello. Si vous ne savez pas si vous avez toutes les ressources en cours d’exécution dans Azure Marketplace de pile, déployez un ordinateur virtuel (VM) et de Vérifiez hello VM analyse toomake panneau que qu’il est en cours d’exécution. Utilisez hello PowerShell applets de commande tooview hello l’utilisation des données suivantes :

1. [Installer PowerShell pour Azure Stack.](azure-stack-powershell-install.md)
2. * [Configurer l’utilisateur hello Azure pile](azure-stack-powershell-configure-user.md) ou hello [l’opérateur Azure pile](azure-stack-powershell-configure-admin.md) environnement PowerShell 
3. données d’utilisation tooretrieve hello, utilisez hello [Get-UsageAggregates](/powershell/module/azurerm.usageaggregates/get-usageaggregates) applet de commande PowerShell :
   ```PowerShell
   Get-UsageAggregates -ReportedStartTime "<Start time for usage reporting>" -ReportedEndTime "<end time for usage reporting>" -AggregationGranularity <Hourly or Daily>
   ```

   Si les données d’utilisation ne seront disponibles, elle est retournée dans comme indiqué dans hello suivant capture d’écran : 
   
   ![Agrégats d’utilisation](media/azure-stack-billing-and-chargeback/image2.png)
   
   PowerShell retourne 1 000 lignes d’utilisation par appel. Vous pouvez utiliser hello continuation paramètre tooretrieve plus de 1 000 lignes

## <a name="next-steps"></a>Étapes suivantes

[TooAzure de pile Azure l’utilisation des données de rapport](azure-stack-usage-reporting.md)

[API Utilisation des ressources de fournisseur](azure-stack-provider-resource-api.md)

[API Utilisation des ressources de client](azure-stack-tenant-resource-usage-api.md)

[Questions fréquentes (FAQ) relatives à l’utilisation](azure-stack-usage-related-faq.md)

