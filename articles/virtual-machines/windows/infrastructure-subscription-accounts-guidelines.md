---
title: aaaSubscription et les comptes pour les machines virtuelles Windows dans Azure | Documents Microsoft
description: "Découvrez hello clé conception et implémentation des recommandations pour les abonnements et les comptes dans Azure."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 761fa847-78b0-4078-a33a-d95d198d1029
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f9dc712af559b04490be1dc721a9b9f7fe9ed88f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a>Instructions pour les abonnements et les comptes Azure pour machines virtuelles Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Cet article se concentre sur comment tooapproach abonnement et gestion des comptes en tant que votre environnement et de la base d’utilisateurs augmente.

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a>Instructions d’implémentation pour les abonnements et les comptes
Décisions :

* Le jeu de comptes et les abonnements devez-vous toohost votre charge de travail informatique ou d’infrastructure ?
* Comment toobreak vers le bas hello hiérarchie toofit votre organisation ?

Tâches :

* Définir la hiérarchie logique que vous aimeriez toomanage à partir d’un niveau d’abonnement.
* toomatch cette hiérarchie logique, les comptes hello requis et des abonnements sous chaque compte.
* Créer un jeu hello des abonnements et des comptes à l’aide de votre convention d’affectation de noms.

## <a name="subscriptions-and-accounts"></a>Abonnements et comptes
toowork avec Azure, vous devez un ou plusieurs abonnements Azure. Des ressources telles que des machines virtuelles ou des réseaux virtuels existent dans le contexte de ces abonnements.

* Les clients d’entreprise ont généralement une inscription d’entreprise, hello des ressources de plus haut dans la hiérarchie de hello et tooone associée ou autres comptes.
* Pour les particuliers et les clients sans une inscription de l’entreprise, la ressource de plus de hello est compte de hello.
* Les abonnements sont associés tooaccounts, et il peut y avoir un ou plusieurs abonnements par compte. Azure enregistre les informations au niveau d’abonnement hello de facturation.

En raison de la limite de toohello de niveaux de hiérarchie deux sur la relation d’abonnement de compte/hello, il est important tooalign hello conventions d’affectation des comptes et des abonnements toohello besoins de facturation. Par exemple, si une entreprise internationale utilise Azure, ils peuvent choisir le compte de toohave un par région et ont des abonnements gérés au niveau de la région de hello :

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

Par exemple, vous pouvez utiliser hello suivant structure :

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

Si une région décide toohave plus de groupe tooa associé à un seul abonnement, convention d’affectation de noms de hello doit incorporer un tooencode moyen hello des données supplémentaires sur le compte de hello ou nom de l’abonnement hello. Cette organisation permet masser facturation données toogenerate hello nouveaux niveaux de hiérarchie au cours de la facturation de rapports :

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

organisation de Hello pourrait ressembler à hello l’exemple suivant :

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

Nous fournissons une facturation détaillée au moyen d’un fichier téléchargeable, pour un compte unique ou pour tous les comptes liés à un accord d’entreprise.

## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

