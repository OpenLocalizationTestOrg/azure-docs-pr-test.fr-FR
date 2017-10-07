---
title: "vue d’ensemble plan, offre, quotas et des abonnements de pile aaaAzure | Documents Microsoft"
description: "Comme un opérateur cloud, je veux toounderstand Qu'azure pile plans, les offres, les quotas et les abonnements."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 8/22/2017
ms.author: erikje
ms.openlocfilehash: 67f5bcfda221473b1f397668e2a3186b80d6f43c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-offer-quota-and-subscription-overview"></a>Vue d’ensemble des plans, des offres, des quotas et des abonnements

Azure Stack permet de fournir un large éventail de services, comme des machines virtuelles, des bases de données SQL Server, SharePoint, Exchange et même des [articles de la Place de marché Azure](azure-stack-marketplace-azure-items.md). En tant qu’opérateur cloud, vous configurez et fournissez ces services dans Azure Stack avec des plans, des offres et des quotas.

Les offres contiennent un ou plusieurs plans, et chaque plan inclut un ou plusieurs services. En créant des plans et en les regroupant dans différentes offres, on peut contrôler :
- les services et ressources auxquels les utilisateurs ont accès ;
- quantité Hello de ressources que les utilisateurs peuvent consommer.
- les régions ont accès aux ressources de toohello

Pour fournir un service, vous suivrez les grandes étapes suivantes :

1. Ajouter un service que vous souhaitez que les utilisateurs de tooyour de toodeliver.
2. Créez un plan qui contient un ou plusieurs services. Lorsque vous créez un plan, sélectionnez ou créez des quotas qui définissent les limites des ressources hello de chaque service dans le plan de hello.
3. Créez une offre qui contient un ou plusieurs plans (plans de base et plans d’extension facultatifs compris).

Une fois que vous avez créé l’offre de hello, vos utilisateurs peuvent s’abonner services de tooit tooaccess hello et il fournit des ressources. Les utilisateurs peuvent s’abonner tooas offre de nombreuses qu’ils le souhaitent. Hello diagramme suivant montre un exemple simple d’un utilisateur qui s’est abonnée tootwo offres. Chaque offre possède un plan ou les deux, et chaque plan de leur donne accès tooservices.

![](media/azure-stack-key-features/image4.png)

## <a name="plans"></a>Abonnements

Les plans regroupent un ou plusieurs services. Comme un opérateur cloud, vous [créer des plans de](azure-stack-create-plan.md) toooffer tooyour utilisateurs. À son tour, vos utilisateurs s’abonner tooyour offres toouse hello plans et services qu’ils comprennent. Lorsque vous créez des plans, assurez-vous que tooset vos quotas, définir vos plans de base et vous pouvez inclure des plans de module complémentaire facultatif.

### <a name="quotas"></a>Quotas

toohelp vous gérez votre capacité du cloud, vous sélectionnez ou créez un quota pour chaque service dans un plan. Quotas de définissent des limites de ressources supérieur hello qui un abonnement de l’utilisateur peut fournir ou consommer. Par exemple, un quota peut permettre un toocreate utilisateur des machines virtuelles de toofive. Les quotas peuvent limiter différentes ressources, notamment les machines virtuelles, la RAM et l’UC.

Les quotas peuvent être configurés région par région. Par exemple, un plan comprenant des services de calcul de la région A peut avoir un quota de deux machines virtuelles, 4 Go de RAM et 10 cœurs de processeur. Dans le Kit de développement de la pile d’Azure, qu’une seule région de hello (nommé *local*) est disponible.

### <a name="base-plan"></a>Plan de base

Lorsque vous créez une offre, administrateur de service hello peut inclure un plan de base. Ces plans de base sont inclus par défaut lorsqu’un utilisateur s’abonne toothat offre. Lorsqu’un utilisateur s’abonne, ils ont accès tooall hello les fournisseurs de ressources spécifiés dans les plans de base (avec les quotas correspondant hello).

### <a name="add-on-plans"></a>Plans d’extension

Vous pouvez également inclure des plans d’extension facultatifs dans une offre. Plans de module complémentaire ne sont pas inclus par défaut dans l’abonnement de hello. Les plans de modules complémentaires sont des plans supplémentaires (avec des quotas) disponibles dans une offre qu’un abonné peut ajouter des abonnements de tootheir. Par exemple, vous pouvez proposer un plan de base avec des ressources limitées pour une version d’évaluation et un plan de module complémentaire avec toocustomers de ressources plus importantes qui décident de service de hello tooadopt.

## <a name="offers"></a>Offres

Offres sont des groupes d’un ou plusieurs plans que vous créez afin que les utilisateurs peuvent s’abonner toothem. Par exemple, une offre Alpha peut contenir un plan A comportant un ensemble de services de calcul et un plan B comportant un ensemble de services de stockage et réseau. 

Lorsque vous [créer une offre](azure-stack-create-offer.md), vous devez inclure au moins un plan de base, mais vous pouvez également créer des plans de modules complémentaires que les utilisateurs peuvent ajouter tootheir abonnement.


## <a name="subscriptions"></a>Abonnements

L’abonnement est la forme sous laquelle les utilisateurs accèdent aux offres. Si vous êtes un opérateur cloud chez un fournisseur de services, vos utilisateurs (clients) achètent vos services en vous abonnant tooyour offres. Si vous êtes un opérateur cloud dans votre organisation, vos utilisateurs (employés) peuvent s’abonner à des services de toohello que vous proposez sans payer. Chaque combinaison entre un utilisateur et une offre correspond à un abonnement unique. Par conséquent, un utilisateur peut avoir des offres d’abonnements toomultiple, mais chaque abonnement s’applique tooonly une offre. Plans, les offres et les quotas s’appliquent uniquement tooeach unique de l’abonnement : ils ne peuvent pas être partagés entre des abonnements. Chaque ressource créée par un utilisateur est associée à un seul abonnement.


### <a name="default-provider-subscription"></a>Abonnement au fournisseur par défaut

Hello abonnement de fournisseur par défaut est automatiquement créé lorsque vous déployez hello Kit de développement de pile Azure. Cet abonnement peut toomanage utilisée Azure pile, déployez davantage de fournisseurs de ressources et créer des plans et des offres pour les utilisateurs. Pour des raisons de licence et sécurité, ne doit pas être utilisé toorun les charges de travail client et les applications. 

## <a name="next-steps"></a>Étapes suivantes

[Créer un plan](azure-stack-create-plan.md)
