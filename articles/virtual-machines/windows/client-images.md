---
title: images de client Windows aaaUse dans Azure | Documents Microsoft
description: "Comment toouse abonnement Visual Studio avantages toodeploy Windows 7, Windows 8 ou Windows 10 dans Azure pour les scénarios de développement/test"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 91c3880a-cede-44f1-ae25-f8f9f5b6eaa4
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: 4ac7c3d9872673030f4ea0f0ab38625dd9d9c1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-client-in-azure-for-devtest-scenarios"></a>Utilisation d’un client Windows dans Azure pour les scénarios de développement et/ou test
Vous pouvez utiliser Windows 7, Windows 8 ou Windows 10 dans Azure pour des scénarios de développement / de test à condition de disposer d'un abonnement Visual Studio (anciennement MSDN) approprié. Cet article présente les conditions d’éligibilité hello pour l’exécution de client Windows dans Azure et l’utilisation de hello images de la galerie Azure.

## <a name="subscription-eligibility"></a>Admissibilité à un abonnement
Les abonnés Visual Studio actifs (les personnes qui ont acquis une licence d’abonnement Visual Studio) peuvent utiliser un client Windows à des fins de développement et de tests. Un client Windows peut être utilisé sur votre propre matériel et vos machines virtuelles Azure en cours d’exécution dans n’importe quel type d’abonnement Azure. Client Windows ne peut pas être déployé tooor utilisé dans Azure pour la production normale, ou par des personnes qui ne sont pas des abonnés actifs de Visual Studio.

Pour votre commodité, nous avons apporté certaines images de Windows 10 disponibles à partir de la galerie d’Azure hello dans [offre de développement/test éligible](#eligible-offers). Les abonnés Visual Studio dans n’importe quel type d’offre peuvent également [correctement préparer et créer](prepare-for-upload-vhd-image.md) une image 64 bits de Windows 7, Windows 8 ou Windows 10, puis [télécharger tooAzure](upload-generalized-managed.md). utilisation de Hello reste toodev/test limité par les abonnés actifs de Visual Studio.

## <a name="eligible-offers"></a>Offres admissibles
Hello suivant hello détails de table offre les identificateurs qui sont éligible toodeploy Windows 10 via hello galerie Azure. Hello Windows 10 images sont uniquement visible toohello suivant des offres. Les abonnés Visual Studio qui doive toorun Windows client dans un type autre offre besoin vous trop[correctement préparer et créer](prepare-for-upload-vhd-image.md) une image 64 bits de Windows 7, Windows 8 ou Windows 10 et [puis téléchargez tooAzure](upload-generalized-managed.md).

| Nom de l’offre | Numéro de l’offre | Images de client disponibles |
|:--- |:---:|:---:|
| [Pay-As-You-Go Dev/Test](https://azure.microsoft.com/offers/ms-azr-0023p/) |0023P |Windows 10 |
| [Abonnés Visual Studio Enterprise (MPN)](https://azure.microsoft.com/offers/ms-azr-0029p/) |0029P |Windows 10 |
| [Abonnés Visual Studio Professional](https://azure.microsoft.com/offers/ms-azr-0059p/) |0059P |Windows 10 |
| [Abonnés Visual Studio Test Professional](https://azure.microsoft.com/offers/ms-azr-0060p/) |0060P |Windows 10 |
| [Visual Studio Premium avec MSDN (avantage)](https://azure.microsoft.com/offers/ms-azr-0061p/) |0061P |Windows 10 |
| [Abonnés Visual Studio Enterprise](https://azure.microsoft.com/offers/ms-azr-0063p/) |0063P |Windows 10 |
| [Abonnés Visual Studio Enterprise (BizSpark)](https://azure.microsoft.com/offers/ms-azr-0064p/) |0064P |Windows 10 |
| [Enterprise Dev/Test](https://azure.microsoft.com/ofers/ms-azr-0148p/) |0148P |Windows 10 |

## <a name="check-your-azure-subscription"></a>Vérification de votre abonnement Azure
Si vous ne connaissez pas votre ID d’offre, vous pouvez l’obtenir via hello portail Azure dans un des deux façons suivantes :  

- Sur le panneau de « Abonnements » hello :

  ![Offre des détails de l’ID de hello portail Azure](./media/client-images/offer-id-azure-portal.png) 

- Vous pouvez également cliquer sur **Facturation**, puis sur votre ID d’abonnement. ID d’offre Hello s’affiche dans le panneau de facturation hello.

Vous pouvez également afficher les ID d’offre hello de hello [onglet 'Abonnements'](http://account.windowsazure.com/Subscriptions) du portail de compte Azure hello :

![Détails de l’ID de l’offre à partir du portail de compte Azure hello](./media/client-images/offer-id-azure-account-portal.png) 

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez désormais déployer vos machines virtuelles à l’aide de [PowerShell](quick-create-powershell.md), de [modèles Resource Manager](ps-template.md) ou de [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).

