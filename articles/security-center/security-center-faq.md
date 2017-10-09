---
title: "Forum aux questions (FAQ sur) le centre de sécurité d’aaaAzure | Documents Microsoft"
description: "Ce forum aux questions concerne le Centre de sécurité Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: be2ab6d5-72a8-411f-878e-98dac21bc5cb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: cd0c0f8bdf15cdaf5889f2da5ac3cadf6017a9e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-frequently-asked-questions-faq"></a>FAQ du Centre de sécurité Azure
Ce forum aux questions répond aux questions sur Azure Security Center, un service qui vous permet d’empêcher, détecter et répondre toothreats avec une meilleure visibilité et un contrôle accru de la sécurité hello de vos ressources de Microsoft Azure.

> [!NOTE]
> À compter de début juin 2017, centre de sécurité utiliser hello Microsoft Monitoring Agent toocollect et stocker des données. toolearn, voir [Azure Security Center Platform Migration](security-center-platform-migration.md). informations Hello dans cet article représentent les fonctionnalités du centre de sécurité après la transition toohello Microsoft Monitoring Agent.
>
>

## <a name="general-questions"></a>Questions générales
### <a name="what-is-azure-security-center"></a>Qu’est-ce que le Centre de sécurité Azure ?
Centre de sécurité Azure vous permet d’empêcher, détecter et répondre toothreats avec une meilleure visibilité et un contrôle accru de la sécurité hello de vos ressources Azure. Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité.

### <a name="how-do-i-get-azure-security-center"></a>Comment obtenir le Centre de sécurité Azure ?
Centre de sécurité Azure est activée avec votre abonnement Microsoft Azure et accessible à partir de hello [portail Azure](https://azure.microsoft.com/features/azure-portal/). ([Connectez-vous au portail de toohello](https://portal.azure.com), sélectionnez **Parcourir**, faites défiler la fenêtre trop**centre de sécurité**).  

## <a name="billing"></a>Facturation
### <a name="how-does-billing-work-for-azure-security-center"></a>Comment fonctionne la facturation pour le Centre de sécurité Azure ?
Security Center est proposé en deux niveaux :

Hello **niveau gratuit** offre une visibilité dans l’état de sécurité hello de vos ressources Azure, la stratégie de sécurité de base, les recommandations de sécurité et l’intégration avec les produits et services des partenaires.

Hello **niveau Standard** ajoute les menaces avancées des fonctions de détection, y compris la menace d’intelligence, analyse comportementale, la détection d’anomalies, les incidents de sécurité et rapports d’attribution de la menace. niveau Standard de Hello est gratuit pour hello 60 premiers jours. Si vous choisissez de service de hello toocontinue toouse au-delà de 60 jours, nous allons commencer automatiquement toocharge pour le service de hello.  tooupgrade, sélectionnez niveau tarifaire Bonjour [stratégie de sécurité](security-center-policies.md#set-security-policies). toolearn, voir [tarification du centre de sécurité](security-center-pricing.md).

## <a name="permissions"></a>Autorisations
Centre de sécurité Azure utilise [contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-configure.md), qui fournit des [rôles intégrés](../active-directory/role-based-access-built-in-roles.md) qui peuvent être attribuées toousers, des groupes et des services dans Azure.

Centre de sécurité évalue la configuration de hello de vos problèmes de sécurité tooidentify de ressources et les vulnérabilités. Dans le centre de sécurité, vous voyez uniquement les informations liées tooa ressource lorsque vous sont assignés rôle hello de propriétaire, collaborateur ou lecteur pour le groupe d’abonnement ou une ressource hello appartenant à une ressource.

Consultez [autorisations dans le centre de sécurité Azure](security-center-permissions.md) toolearn plus d’informations sur les rôles et les actions autorisées dans le centre de sécurité.

## <a name="data-collection"></a>Collecte des données
Centre de sécurité collecte les données de vos machines virtuelles de tooassess leur état de sécurité, fournir des recommandations de sécurité et vous alerter toothreats. Lorsque vous accédez au Centre de sécurité pour la première fois, la collecte de données est activée sur toutes les machines virtuelles de votre abonnement. Vous pouvez également activer la collecte des données de hello stratégie du centre de sécurité.

### <a name="how-do-i-disable-data-collection"></a>Comment désactiver la collecte des données ?
Si vous utilisez hello Azure Security Center gratuit, vous pouvez désactiver la collecte des données à partir d’ordinateurs virtuels à tout moment. Collecte de données est requise pour les abonnements sur le niveau Standard de hello. Vous pouvez désactiver la collecte des données d’un abonnement dans hello stratégie de sécurité. ([Connecter toohello portail Azure](https://portal.azure.com), sélectionnez **Parcourir**, sélectionnez **centre de sécurité**, puis sélectionnez **stratégie**.)  Lorsque vous sélectionnez un abonnement, un nouveau panneau s’ouvre et fournit hello d’option tooturn hors **collecte des données**.

### <a name="how-do-i-enable-data-collection"></a>Comment activer la collecte des données ?
Vous pouvez activer la collecte de données pour votre abonnement Azure Bonjour stratégie de sécurité. collecte des données tooenable. [Connectez-vous à toohello portail Azure](https://portal.azure.com), sélectionnez **Parcourir**, sélectionnez **centre de sécurité**, puis sélectionnez **stratégie**. Définissez **collecte des données** trop**sur**.

### <a name="what-happens-when-data-collection-is-enabled"></a>Que se passe-t-il quand la collecte des données est activée ?
Lors de la collecte des données est activée, hello Microsoft Monitoring Agent est automatiquement configuré sur toutes les existantes et tout pris en charge nouveaux ordinateurs virtuels qui sont déployés dans l’abonnement de hello.

### <a name="does-hello-monitoring-agent-impact-hello-performance-of-my-servers"></a>Est hello performances hello l’Agent d’analyse de mes serveurs ?
agent de Hello consomme une quantité nominale de ressources système et doit avoir un impact limité sur les performances de hello. Pour plus d’informations sur l’impact sur les performances et de l’agent de hello et d’extension, consultez hello [guide de planification et d’opérations](security-center-planning-and-operations-guide.md#data-collection-and-storage).

### <a name="where-is-my-data-stored"></a>Où sont stockées mes données ?
Les données collectées à partir de cet agent sont stockées dans un espace de travail Log Analytics existant associé à votre abonnement Azure ou dans un nouvel espace de travail. Pour plus d’informations, consultez [Sécurité des données](security-center-data-security.md).

## <a name="using-azure-security-center"></a>Utilisation du Centre de sécurité Azure
### <a name="what-is-a-security-policy"></a>Qu’est-ce qu’une stratégie de sécurité ?
Une stratégie de sécurité définit l’ensemble de hello de contrôles qui sont recommandés pour les ressources hello spécifié abonnement. Dans le centre de sécurité Azure, vous définissez des stratégies pour vos abonnements Azure, en fonction de la société tooyour exigences de sécurité et de type hello d’applications ou de la sensibilité des données hello dans chaque abonnement.

stratégies de sécurité Hello activés dans les recommandations de sécurité de lecteur Azure Security Center et de surveillance. toolearn en savoir plus sur les stratégies de sécurité, consultez [contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md).

### <a name="who-can-modify-a-security-policy"></a>Qui peut modifier une stratégie de sécurité ?
toomodify une stratégie de sécurité, vous devez être un administrateur de sécurité ou un propriétaire ou un collaborateur de cet abonnement.

toolearn tooconfigure une stratégie de sécurité, voir [définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md).

### <a name="what-is-a-security-recommendation"></a>Qu’est-ce qu’une recommandation de sécurité ?
Centre de sécurité Azure analyse l’état de la sécurité de vos ressources Azure hello. Quand des failles de sécurité potentielles sont identifiées, des recommandations sont créées. guide de recommandations Hello vous guide dans les processus hello de configuration hello nécessaire de contrôle. Voici quelques exemples :

* Configuration du logiciel anti-programme malveillant toohelp identifier et supprimer les logiciels malveillants
* Configuration [groupes de sécurité réseau](../virtual-network/virtual-networks-nsg.md) et les machines de toovirtual toocontrol le trafic de règles
* Configuration d’un toohelp de pare-feu d’applications web vous défendre contre des attaques ciblant vos applications web
* Déploiement de mises à jour système manquantes
* Adressage des configurations de système d’exploitation qui ne correspondent pas hello recommandé de lignes de base

Seules les recommandations qui sont activées dans les stratégies de sécurité sont affichées ici.

### <a name="how-can-i-see-hello-current-security-state-of-my-azure-resources"></a>Comment puis-je voir hello sécurité état actuel de mes ressources Azure ?
Hello **vue d’ensemble du centre de sécurité** panneau affiche hello posture de sécurité globale de votre environnement ventilé par calcul, mise en réseau, stockage et de données et Applications. Chaque type de ressource possède un indicateur montrant la présence éventuelle de failles de sécurité. En cliquant sur chaque vignette affiche une liste des problèmes de sécurité identifiés par le centre de sécurité, ainsi que d’un inventaire des ressources hello dans votre abonnement.

### <a name="what-triggers-a-security-alert"></a>Qu’est-ce qui déclenche une alerte de sécurité ?
Centre de sécurité Azure automatiquement collecte, analyse et fusionne les données du journal à partir de vos ressources Azure, hello réseau et les solutions de partenaire comme contre les logiciels malveillants et les pare-feu. Quand des menaces sont détectées, une alerte de sécurité est créée. Voici quelques exemples de détections :

* Des machines virtuelles compromises qui communiquent avec des adresses IP connues comme étant malveillantes
* Des programmes malveillants avancés qui sont détectés à l’aide du rapport d’erreurs Windows
* Des attaques par force brute contre des machines virtuelles
* Des alertes de sécurité émises par des solutions de sécurité partenaires intégrées, telles que des logiciels anti-programme malveillant ou des pare-feu d’applications web

### <a name="whats-hello-difference-between-threats-detected-and-alerted-on-by-microsoft-security-response-center-versus-azure-security-center"></a>Qu’est la différence de hello de menaces détectées et recevoir une alerte par Microsoft Security Response Center et le centre de sécurité Azure ?
Hello MSRC Microsoft Security Response Center () effectue une analyse de sécurité select de hello réseau Azure et l’infrastructure et reçoit des plaintes intelligence et abus de menace de tiers. Lorsque le MSRC est informé que les données client a été accédées par un tiers illégal ou non autorisé ou utilisation de ce client hello de Azure n’est pas conforme avec les termes du contrat de hello usage Acceptable, un gestionnaire des incidents de sécurité avertit le client de hello. Notification se produit généralement en envoyant un toohello la sécurité par courrier électronique contacts spécifiés dans le centre de sécurité Azure ou hello propriétaire de l’abonnement Azure si un contact de sécurité n’est pas spécifié.

Centre de sécurité est un service Azure qui surveille l’environnement Azure du client de hello et s’applique analytique tooautomatically détecter un large éventail d’activités potentiellement malveillantes. Ces détections sont signalées en tant qu’alertes de sécurité dans le tableau de bord de centre de sécurité hello.

### <a name="which-azure-resources-are-monitored-by-azure-security-center"></a>Quelles ressources Azure sont surveillées par Azure Security Center ?
Centre de sécurité Azure surveille hello suivant des ressources Azure :

* Machines virtuelles (VM) (y compris [Cloud Services](../cloud-services/cloud-services-choose-me.md))
* Réseaux virtuels Azure
* Service SQL Azure
* un compte Azure Storage.
* Azure Web Apps (dans [App Service Environment](../app-service/app-service-app-service-environments-readme.md))
* Solutions de partenaires intégrées à votre abonnement Azure, par exemple pare-feu d’applications web sur les machines virtuelles et sur [App Service Environment](../app-service/app-service-app-service-environments-readme.md)

## <a name="virtual-machines"></a>Machines virtuelles
### <a name="what-types-of-virtual-machines-are-supported"></a>Quels sont les types de machines virtuelles pris en charge ?
Analyse et les recommandations sont disponibles pour les machines virtuelles (VM) créés à l’aide de deux hello [classique et les modèles de déploiement Resource Manager](../azure-classic-rm.md).

Consultez [Plateformes prises en charge dans Azure Security Center](security-center-os-coverage.md) pour obtenir la liste des plateformes prises en charge.

### <a name="why-doesnt-azure-security-center-recognize-hello-antimalware-solution-running-on-my-azure-vm"></a>Pourquoi Azure Security Center ne reconnaît pas les solutions anti-programme malveillant de hello en cours d’exécution sur ma machine virtuelle Azure ?
Azure Security Center bénéficie d’une visibilité sur les logiciels anti-programme malveillant installés par le biais des extensions Azure. Par exemple, le centre de sécurité n’est pas contre les logiciels malveillants en mesure de toodetect qui a été préalablement installés sur une image que vous avez fourni ou si vous avez installé le logiciel anti-programme malveillant sur vos ordinateurs virtuels à l’aide de vos propres processus (par exemple, les systèmes de gestion de configuration).

### <a name="why-do-i-get-hello-message-missing-scan-data-for-my-vm"></a>Je reçois message de type hello « Manquant des données d’analyse » pour ma machine virtuelle ?
Ce message s’affiche lorsqu’il n’existe aucune donnée d’analyse pour une machine virtuelle. Il peut prendre un certain temps (moins d’une heure) pour l’analyse de données toopopulate après que la collecte des données est activée dans le centre de sécurité Azure. Après le remplissage initial de hello de données d’analyse, vous pouvez recevoir ce message, car aucune donnée analyse tout ou il n’existe aucune donnée d’analyse récente. Le remplissage des analyses n’est pas effectué pour une machine virtuelle à l’état Arrêté. Ce message peut également s’afficher si les données d’analyse n’a pas rempli récemment (conformément à la stratégie de rétention hello pour l’agent Windows hello, qui a une valeur par défaut de 30 jours).

### <a name="why-do-i-get-hello-message-vm-agent-is-missing"></a>Je reçois message de type hello « Agent de machine virtuelle est manquant ? »
Hello Agent de machine virtuelle doit être installé sur les machines virtuelles tooenable la collecte de données. Hello Agent de machine virtuelle est installé par défaut pour les ordinateurs virtuels qui sont déployés à partir de hello Azure Marketplace. Pour plus d’informations sur la façon dont tooinstall hello Agent de machine virtuelle sur les autres machines virtuelles, voir blog de hello [Agent de machine virtuelle et Extensions](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/).
