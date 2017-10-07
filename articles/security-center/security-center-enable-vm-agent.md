---
title: aaaEnable Agent de machine virtuelle dans Azure Security Center | Documents Microsoft
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** activer VM Agent **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a>Activer l’agent de machine virtuelle dans le Centre de sécurité Azure
Hello Agent de machine virtuelle doit être installé sur les machines virtuelles (VM) dans l’ordre trop[activer la collecte des données](security-center-enable-data-collection.md).  Permet de centre de sécurité Azure toosee qui nécessitent des machines virtuelles hello Agent de machine virtuelle et recommande que vous activez hello Agent de machine virtuelle sur ces machines virtuelles.

Hello Agent de machine virtuelle est installé par défaut pour les ordinateurs virtuels qui sont déployés à partir de hello Azure Marketplace. article de Hello [Agent de machine virtuelle et Extensions-partie 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) fournit des informations sur la façon dont tooinstall hello Agent de machine virtuelle.

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement. Il ne s’agit pas d’un guide pas à pas.
>
>

## <a name="implement-hello-recommendation"></a>Implémenter la recommandation de hello
1. Bonjour **Panneau de recommandations**, sélectionnez **activer l’Agent de machine virtuelle**.
   ![Activer l’agent de machine virtuelle][1]
2. Cela ouvre le panneau de hello **VM Agent manquant ou ne répond pas**. Ce panneau répertorie les machines virtuelles hello nécessitant hello Agent de machine virtuelle. Suivez les instructions de hello sur l’agent de machine virtuelle hello panneau tooinstall hello.
   ![L’agent de machine virtuelle est manquant][2]

## <a name="see-also"></a>Voir aussi
toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md)--Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md): découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md)--Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md)--Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md)--rechercher Forum aux questions sur l’utilisation du service de hello.
* [Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/)--obtenir les dernières informations de sécurité Azure hello et informations.

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
