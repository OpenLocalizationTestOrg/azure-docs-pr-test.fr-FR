---
title: "aaaInstall Endpoint Protection dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandation du centre de sécurité Azure ** installer Endpoint Protection **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a>Installer Endpoint Protection dans Azure Security Center
Azure Security Center recommande d’installer Endpoint Protection sur vos machines virtuelles Azure si cette dernière n’est pas déjà activée. Cette recommandation s’applique tooWindows machines virtuelles.

> [!NOTE]
> Cet exemple de déploiement utilise Microsoft Antimalware. Consultez [Intégration des partenaires dans Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) pour obtenir la liste des partenaires intégrés dans Security Center.  
>
>

## <a name="implement-hello-recommendation"></a>Implémenter la recommandation de hello

> [!NOTE]
> Ce document présente le service de hello à l’aide d’un exemple de déploiement.  Ce document n'est pas un guide pas à pas.
>
>

1. Bonjour **recommandations** panneau, sélectionnez **installer Endpoint Protection**.
   ![Sélectionner Installer Endpoint Protection][1]
2. Hello **installer Endpoint Protection** panneau s’ouvre en affichant une liste d’ordinateurs virtuels sans protection de point de terminaison. Sélectionnez hello de liste hello machines virtuelles que vous souhaitez une protection de point de terminaison tooinstall sur et cliquez sur **installer sur des machines virtuelles**.
   ![Sélectionnez les machines virtuelles tooinstall Endpoint Protection sur][2]
3. Hello **sélectionner une Protection de point de terminaison** panneau s’ouvre tooallow vous tooselect hello endpoint protection solution souhaitée toouse. Dans cet exemple, nous allons sélectionner **Microsoft Antimalware**.
   ![Sélectionner Endpoint Protection][3]
4. Des informations supplémentaires sur la solution de protection de point de terminaison hello s’affiche. Sélectionnez **Créer**.
   ![Créer une solution anti-programme malveillant][4]
5. Entrez les paramètres de configuration hello requis sur hello **Ajout d’une Extension** panneau, puis sélectionnez **OK**. toolearn savoir plus sur les paramètres de configuration de hello, consultez [par défaut et la Configuration du logiciel anti-programme malveillant personnalisée](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).

[Microsoft Antimalware](../security/azure-security-antimalware.md) est maintenant actif sur hello sélectionné des machines virtuelles.

## <a name="see-also"></a>Voir aussi
Cet article vous a montré comment tooimplement hello recommandation du centre de sécurité « Installer Endpoint Protection ». toolearn savoir plus sur l’activation de Microsoft Antimalware dans Azure, consultez hello suivant du document :

* [Microsoft Antimalware pour Services de cloud computing et Machines virtuelles](../security/azure-security-antimalware.md) --Découvrez comment toodeploy Microsoft Antimalware.

toolearn en savoir plus sur le centre de sécurité, consultez hello suivant des documents :

* [Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité.
* [Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez comment les recommandations peuvent vous aider à protéger vos ressources Azure.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) --Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) --Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : recherchez des billets de blog sur la sécurité et la conformité Azure.

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
