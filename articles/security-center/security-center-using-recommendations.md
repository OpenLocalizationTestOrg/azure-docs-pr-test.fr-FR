---
title: "aaaUse sécurité de Azure Security Center recommandations tooenhance | Documents Microsoft"
description: " Découvrez comment les stratégies de sécurité toouse et les recommandations dans le centre de sécurité Azure toohelp atténuer une attaque de sécurité. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: terrylan
ms.openlocfilehash: bd314350a5abfceea3e171f2e1b55afe4549c1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-security-center-recommendations-tooenhance-security"></a>Sécurité de tooenhance recommandations utilisation Azure Security Center
Vous pouvez réduire les risques de hello d’un événement de sécurité importants en configurant une stratégie de sécurité, puis en implémentant les recommandations hello fournies par Azure Security Center. Cet article vous explique comment les stratégies de sécurité toouse et les recommandations dans le centre de sécurité toohelp atténuer une attaque de sécurité.

> [!NOTE]
> Cet article s’appuie sur les rôles hello et les concepts présentés dans le centre de sécurité de hello [guide de planification et d’opérations](security-center-planning-and-operations-guide.md). Il est un guide de planification hello conseillé tooreview avant de continuer.
>
>

## <a name="managing-security-recommendations"></a>Gestion des Recommandations de sécurité
Une stratégie de sécurité définit l’ensemble de hello de contrôles qui sont recommandés pour les ressources hello spécifié abonnement ou groupe de ressources. Dans le centre de sécurité, vous définissez des stratégies selon les exigences de sécurité de la société tooyour. toolearn, voir [définir des stratégies de sécurité dans le centre de sécurité](security-center-policies.md).

Stratégies de sécurité pour les groupes de ressources sont hérités du niveau d’abonnement hello.

![Héritage d'une stratégie de sécurité][1]

Si vous avez besoin de stratégies personnalisées dans les groupes de ressources spécifiques, vous pouvez désactiver l’héritage dans le groupe de ressources hello. toodisable, définir l’héritage tooUnique dans Panneau de stratégie de sécurité hello et personnaliser les contrôles de hello centre de sécurité affiche les recommandations pour.

Par exemple, si vous avez des charges de travail qui ne nécessitent pas de stratégie de hello SQL de base de données Transparent Data Encryption (TDE), désactiver la stratégie hello au niveau d’abonnement hello et activez-la uniquement dans les groupes de ressources hello où TDE de SQL est requis.

> [!NOTE]
> S’il existe un conflit entre la stratégie de niveau d’abonnement et de la stratégie de niveau de groupe de ressources, la stratégie au niveau du groupe de ressources hello est prioritaire.
>
>

Centre de sécurité analyse l’état de la sécurité de vos ressources Azure hello. Lorsque le centre de sécurité identifie les éventuelles failles de sécurité, il crée des recommandations basées sur les contrôles hello définies dans la stratégie de sécurité hello. recommandations de Hello vous guident tout au long des processus de hello de la configuration de contrôles de sécurité hello nécessité.

Les recommandations de stratégie actuelles de Security Center se concentrent sur les mises à jour du système, la configuration du système d’exploitation, les groupes de sécurité réseau sur les sous-réseaux et les machines virtuelles, l’audit de base de données SQL, SQL Database TDE, et les pare-feu d’applications web. Pour hello plus récentes des recommandations du centre de sécurité, consultez [gestion des recommandations de sécurité dans le centre de sécurité](security-center-recommendations.md).

## <a name="scenario"></a>Scénario
Ce scénario vous montre comment toouse centre de sécurité toohelp réduire les risques de hello d’un incident de sécurité importants par les recommandations du centre de sécurité et d’exécution des actions. Hello scénario utilise hello, la société fictive Contoso, et les rôles présentés dans hello centre de sécurité [guide de planification et d’opérations](security-center-planning-and-operations-guide.md#security-roles-and-access-controls). les rôles de Hello représentent les personnes et les équipes qui peuvent utiliser des tâches centre de sécurité tooperform différents liés à la sécurité. rôles de Hello sont :

![Rôles du scénario][2]

Contoso migrée récemment certaines de leur tooAzure de ressources locales. Contoso souhaite tooimplement et mettre à jour les protections qui réduisent leur attaque de sécurité vulnérabilité tooa de leurs ressources de cloud de hello.

## <a name="recommended-solution"></a>Solution recommandée
Une solution est toouse centre de sécurité tooprevent et détecter des vulnérabilités de sécurité. Contoso a tooSecurity centre via leur abonnement Azure. Hello [niveau gratuit](security-center-pricing.md) du centre de sécurité est automatiquement activé sur tous les abonnements Azure et collecte des données est activée sur tous les ordinateurs virtuels dans leur abonnement.

David, membre de l'équipe de sécurité informatique de Contoso, configure une **stratégie de sécurité** à l’aide de Security Center. Centre de sécurité analyse l’état de sécurité hello de ressources Azure de Contoso. Lorsque le centre de sécurité identifie les éventuelles failles de sécurité, il crée **recommandations** basée sur les contrôles hello définies dans la stratégie de sécurité hello.

Jeff, qui possède une charge de travail dans le cloud, est responsable de la maintenance des protections conformément à la stratégie de sécurité de Contoso. Jeff peut surveiller les recommandations hello créées par des protections tooapply centre de sécurité. recommandations de Hello guident Jeff hello de la configuration de contrôles de sécurité hello nécessité.

En ordre pour Jeff tooimplement et mettre à jour les protections et éliminer les failles de sécurité, he doit :

- Surveiller les recommandations de sécurité fournies par Security Center
- Évaluer les recommandations de sécurité et décider s’il doit les appliquer ou les ignorer
- Appliquer les recommandations de sécurité

Nous allons suivre toosee des étapes de Jeff comment il utilise le centre de sécurité recommandations tooguide lui tout au long des processus de hello de la configuration de contrôles des failles de sécurité tooeliminate.

## <a name="how-tooimplement-this-solution"></a>Comment tooimplement cette solution
Jeff se connecte trop[portail Azure](https://azure.microsoft.com/features/azure-portal/) et ouvre hello console du centre de sécurité. Dans le cadre de son quotidienne suivi des activités, il vérifie toosee s’il existe des recommandations de sécurité en effectuant hello comme suit :

1. Jeff sélectionne hello **recommandations** vignette tooopen hello **recommandations** panneau.
   ![Sélectionnez hello recommandations vignette][3]
2. Jeff passe en revue la liste des recommandations hello. Il constate que le centre de sécurité a fourni la liste hello des recommandations par ordre de priorité, à partir de la priorité de toolowest de priorité la plus élevée. Il décide tooaddress une recommandation de haute priorité sur la liste de hello. Il sélectionne **installer Endpoint Protection** sur hello **recommandations** panneau.
3. Hello **installer Endpoint Protection** panneau s’ouvre en affichant une liste d’ordinateurs virtuels sans logiciel anti-programme malveillant activée. Jeff passe en revue la liste hello d’ordinateurs virtuels, sélectionne toutes les machines virtuelles et sélectionne ensuite **installer sur des machines 3 virtuelles**.
   ![Installer Endpoint Protection][4]
4. Hello **sélectionner une Protection de point de terminaison** panneau s’ouvre Jeff propose deux solutions anti-programme malveillant. Jeff sélectionne hello **Microsoft Antimalware** solution.
5. Des informations supplémentaires sur la solution anti-programme malveillant de hello s’affiche. Jeff sélectionne **Créer**.
   ![Microsoft Antimalware][5]
6. Jeff saisit hello nécessaire les paramètres de configuration de hello **installer** panneau et sélectionne **OK**.

[Microsoft Antimalware](../security/azure-security-antimalware.md) est maintenant actif sur hello sélectionné des machines virtuelles.

Jeff continue toomove hello haute priorité et les recommandations de priorité moyenne, par le biais de la prise de décisions sur la mise en œuvre. Jeff référence hello [gestion des recommandations de sécurité](security-center-recommendations.md) recommandations de hello toounderstand et ce que chacune d’elles fait si il applique l’article.

Jeff découvre que [MSRC Microsoft Security Response Center ()](../security/azure-security-response-center.md) réalise une surveillance de hello réseau Azure et l’infrastructure sélectionnez sécurité et reçoit des plaintes intelligence et abus de menace de tiers. Si Jeff fournit des détails de contact de sécurité pour l’abonnement Azure de Contoso, les contacts de Microsoft Contoso si hello MSRC découvre les données client que Contoso a accédé par un tiers illégal ou non autorisé. Nous allons suivre Jeff telle qu’il s’applique hello **fournissent des détails de contact de sécurité** recommandation (une recommandation de gravité moyenne dans la liste de hello des recommandations ci-dessus).

1. Jeff sélectionne **fournissent des détails de contact de sécurité** sur hello **recommandations** panneau, ce qui ouvre hello **fournissent des détails de contact de sécurité** panneau.
2. Jeff sélectionne les informations de contact tooprovide abonnement Azure hello sur. Un second panneau **Fournissez les détails du contact de sécurité** s’ouvre.
   ![Informations de contact de sécurité][6]
3. Sur hello deuxième **fournissent des détails de contact de sécurité** insère de panneau, Jeff :

  - adresses de messagerie de contact de sécurité Hello séparés par des virgules (il n’est pas un toohello limiter le nombre d’adresses de messagerie qu’il peut entrer)
  - Un numéro de téléphone du contact de sécurité

4. Jeff active également l’option de hello **m’envoyer des e-mails sur les alertes** tooreceive des e-mails sur les alertes de gravité élevée.
5. Jeff sélectionne **OK** sécurité de hello tooapply contacter les abonnement de tooContoso plus d’informations.

Enfin, Jeff passe en revue la recommandation de priorité basse hello **les vulnérabilités du système d’exploitation corriger** et détermine que cette recommandation n’est pas applicable. Il souhaite que recommandation de hello toodismiss. Jeff sélectionne points hello trois toohello droit, puis sélectionne **Dismiss**.
   ![Ignorer une recommandation][7]

## <a name="conclusion"></a>Conclusion
Surveiller les recommandations dans Security Center peut vous aider à éliminer les failles de sécurité avant qu'une attaque ne se produise. Vous pouvez empêcher un incident de sécurité en implémentant et en gérant des protections à l'aide des stratégies de sécurité de Security Center.

<!--Image references-->
[1]: ./media/security-center-using-recommendations/security-center-policy-inheritance.png
[2]: ./media/security-center-using-recommendations/scenario-roles.png
[3]: ./media/security-center-using-recommendations/select-recommendations-tile.png
[4]: ./media/security-center-using-recommendations/install-endpoint-protection.png
[5]:./media/security-center-using-recommendations/microsoft-antimalware.png
[6]: ./media/security-center-using-recommendations/provide-security-contact-details.png
[7]: ./media/security-center-using-recommendations/dismiss-recommendation.png
