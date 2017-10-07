---
title: "dans Azure dans les machines virtuelles de centre de sécurité et Linux aaaAzure | Documents Microsoft"
description: "Apprenez-en davantage sur la sécurité de votre machine virtuelle Linux Azure avec Azure Security Center."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/07/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7aa0de35fb311457e769f152c8575ec43e41c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-virtual-machine-security-by-using-azure-security-center"></a>Surveiller la sécurité des machines virtuelles à l’aide d’Azure Security Center

Azure Security Center peut vous aider à acquérir une meilleure visibilité des pratiques de sécurité de vos ressources Azure. Azure Security Center assure une surveillance intégrée de la sécurité. Il peut détecter des menaces qui sans cela pourraient passer inaperçues. Ce didacticiel décrit Azure Security Center et comment effectuer les opérations suivantes :
 
> [!div class="checklist"]
> * Configurer la collecte de données
> * Définir des stratégies de sécurité
> * Afficher et résoudre des problèmes d’intégrité de configuration
> * Examiner les menaces détectées  

## <a name="security-center-overview"></a>Vue d’ensemble de Security Center

Security Center identifie des problèmes potentiels de configuration des machines virtuelles et des menaces de sécurité ciblées. Il peut s’agir de machines virtuelles dépourvues de groupes de sécurité réseau, de disques non chiffrés et d’attaques RDP (Remote Desktop Protocol) par force brute. informations de Hello sont indiquées sur le tableau de bord du centre de sécurité de hello dans les graphiques faciles à lire.

tooaccess hello du tableau de bord centre de sécurité, Bonjour portail Azure, dans le menu hello, sélectionnez **centre de sécurité**. Sur le tableau de bord hello, vous pouvez voir l’intégrité de la sécurité de votre environnement Azure hello, rechercher le nombre de recommandations en cours et Afficher état actuel de hello d’alertes de menace. Vous pouvez développer chaque graphique de haut niveau de toosee plus en détail.

![Tableau de bord de Security Center](./media/tutorial-azure-security/asc-dash.png)

Centre de sécurité au-delà de recommandations de tooprovide de découverte de données pour les problèmes qu’il détecte. Par exemple, si une machine virtuelle a été déployée sans groupe de sécurité réseau associé, Security Center affiche une recommandation ainsi que des étapes de correction que vous pouvez suivre. Vous obtenez la mise à jour automatisée sans quitter le contexte hello du centre de sécurité.  

![Recommandations](./media/tutorial-azure-security/recommendations.png)

## <a name="set-up-data-collection"></a>Configurer la collecte de données

Vous pouvez obtenir la visibilité dans les configurations de sécurité de machine virtuelle, vous devez tooset la collecte de données de centre de sécurité. Cela implique la collecte de données de l’activation et la création d’un compte de stockage Azure toohold collectée données. 

1. Dans le tableau de bord du centre de sécurité hello, cliquez sur **stratégie de sécurité**, puis sélectionnez votre abonnement. 
2. Pour **Collecte de données**, sélectionnez **Activée**.
3. toocreate un compte de stockage, sélectionnez **choisir un compte de stockage**. Ensuite, sélectionnez **OK**.
4. Sur hello **stratégie de sécurité** panneau, sélectionnez **enregistrer**. 

agent de collecte de données de centre de sécurité Hello est installé sur tous les ordinateurs virtuels et commence la collecte de données. 

## <a name="set-up-a-security-policy"></a>Configurer une stratégie de sécurité

Stratégies de sécurité sont des éléments de hello toodefine utilisés pour lequel le centre de sécurité collecte des données et émet des recommandations. Vous pouvez appliquer des jeux de toodifferent de stratégies de sécurité différent de ressources Azure. Bien que par défaut les ressources Azure soient évaluées pour tous les éléments de la stratégie, vous pouvez désactiver des éléments individuels de la stratégie pour toutes les ressources ou pour un groupe de ressources Azure. Pour obtenir des informations détaillées sur les stratégies de sécurité de Security Center, consultez [Définir des stratégies de sécurité dans Azure Security Center](../../security-center/security-center-policies.md). 

tooset une stratégie de sécurité pour toutes les ressources Azure :

1. Dans le tableau de bord du centre de sécurité hello, sélectionnez **stratégie de sécurité**, puis sélectionnez votre abonnement.
2. Sélectionnez **Stratégie de prévention**.
3. Activer ou désactiver les éléments de stratégie que vous souhaitez tooapply tooall des ressources Azure.
4. Quand vous avez fini de sélectionner vos paramètres, choisissez **OK**.
5. Sur hello **stratégie de sécurité** panneau, sélectionnez **enregistrer**. 

tooset une stratégie pour un groupe de ressources spécifique :

1. Dans le tableau de bord du centre de sécurité hello, sélectionnez **stratégie de sécurité**, puis sélectionnez un groupe de ressources.
2. Sélectionnez **Stratégie de prévention**.
3. Activer ou désactiver les éléments de stratégie que vous souhaitez le groupe de ressources tooapply toohello.
4. Sous **HÉRITAGE**, sélectionnez **Unique**.
5. Quand vous avez fini de sélectionner vos paramètres, choisissez **OK**.
6. Sur hello **stratégie de sécurité** panneau, sélectionnez **enregistrer**.  

Dans cette page, vous pouvez également désactiver la collecte des données pour un groupe de ressources spécifique.

Bonjour l’exemple suivant, une stratégie unique a été créée pour un groupe de ressources nommé *myResoureGroup*. Dans cette stratégie, les recommandations en matière de chiffrement de disque et de pare-feu d’applications web sont désactivées.

![Stratégie unique](./media/tutorial-azure-security/unique-policy.png)

## <a name="view-vm-configuration-health"></a>Afficher l’état de configuration des machines virtuelles

Une fois que vous avez activé la collecte de données et définir une stratégie de sécurité, le centre de sécurité commence tooprovide les alertes et les recommandations. Comme les ordinateurs virtuels sont déployés, l’agent de collecte de données hello est installé. Centre de sécurité est ensuite rempli avec les données de hello nouvelles machines virtuelles. Pour des informations détaillées sur l’intégrité de la configuration des machines virtuelles, consultez [Protéger vos machines virtuelles dans Security Center](../../security-center/security-center-virtual-machine-recommendations.md). 

Comme les données sont collectées, l’intégrité des ressources hello pour chaque machine virtuelle et les ressources Azure connexes est agrégée. informations de Hello sont affichées dans un graphique de facile à lire. 

intégrité des ressources tooview :

1.  Tableau de bord du centre de sécurité hello, sous **contrôle d’intégrité de sécurité**, sélectionnez **de calcul**. 
2.  Sur hello **de calcul** panneau, sélectionnez **virtuels**. Cette vue fournit un résumé de l’état de la configuration hello pour toutes vos machines virtuelles.

![Calculer l’état d’intégrité](./media/tutorial-azure-security/compute-health.png)

toosee toutes les recommandations pour une machine virtuelle, sélectionnez hello machine virtuelle. Recommandations et mise à jour sont traitées plus en détail dans la section suivante de hello de ce didacticiel.

## <a name="remediate-configuration-issues"></a>Corriger les problèmes de configuration

Dès que le centre de sécurité commence toopopulate avec les données de configuration, les recommandations sont effectuées en fonction de stratégie de sécurité hello que permet de paramétrer. Par exemple, si une machine virtuelle a été configurée sans un groupe de sécurité réseau associé, une recommandation se toocreate un. 

toosee une liste de toutes les recommandations : 

1. Dans le tableau de bord du centre de sécurité hello, sélectionnez **recommandations**.
2. Sélectionnez une recommandation spécifique. Une liste de toutes les ressources pour lequel s’applique la recommandation de hello s’affiche.
3. tooapply une recommandation, sélectionnez une ressource spécifique. 
4. Suivez les instructions de hello pour les étapes de mise à jour. 

Dans de nombreux cas, le centre de sécurité fournit des étapes vous pouvez prendre une recommandation tooaddress sans quitter le centre de sécurité. Bonjour l’exemple suivant, le centre de sécurité détecte un groupe de sécurité réseau qui a une règle de trafic entrant non restreinte. Sur la page de recommandation hello, vous pouvez sélectionner hello **modifier les règles de trafic entrant** bouton. Hello l’interface utilisateur qui est nécessaire toomodify hello règle s’affiche. 

![Recommandations](./media/tutorial-azure-security/remediation.png)

Les recommandations sont marquées comme étant résolues à mesure qu’elles sont appliquées. 

## <a name="view-detected-threats"></a>Consulter les menaces détectées

En outre, tooresource des recommandations de configuration, le centre de sécurité affiche les alertes de détection de menace. fonctionnalité d’alertes de sécurité Hello regroupe les données collectées à partir de chaque machine virtuelle, des journaux de mise en réseau Azure et partenaire connecté solutions toodetect les menaces de sécurité par rapport aux ressources Azure. Pour obtenir des informations détaillées sur les fonctionnalités de détection des menaces de Security Center, consultez [Fonctionnalités de détection d’Azure Security Center](../../security-center/security-center-detection-capabilities.md).

fonctionnalité d’alertes de sécurité Hello requiert le centre de sécurité hello toobe couche augmentée de la tarification *libre* trop*Standard*. 30 jours **version d’évaluation gratuite** est disponible lorsque vous déplacez toothis plus le niveau de tarification. 

niveau de tarification hello toochange :  

1. Dans le tableau de bord du centre de sécurité hello, cliquez sur **stratégie de sécurité**, puis sélectionnez votre abonnement.
2. Sélectionnez **Niveau tarifaire**.
3. Sélectionnez nouveau niveau de hello, puis **sélectionnez**.
4. Sur hello **stratégie de sécurité** panneau, sélectionnez **enregistrer**. 

Une fois que vous avez modifié le niveau de tarification de hello, graphique alertes de sécurité hello commence toopopulate car des menaces de sécurité sont détectés.

![Alertes de sécurité](./media/tutorial-azure-security/security-alerts.png)

Sélectionnez une alerte tooview des informations. Par exemple, vous pouvez voir une description de la menace de hello, temps de détection de hello, toutes les tentatives de menace et hello recommandée de mise à jour. Bonjour l’exemple suivant, une attaque en force brute RDP a été détectée avec 294 tentatives RDP. Une solution recommandée est fournie.

![Attaque RDP](./media/tutorial-azure-security/rdp-attack.png)

## <a name="next-steps"></a>Étapes suivantes
Ce didacticiel vous a montré comment configurer Azure Security Center, puis examiner les machines virtuelles dans Azure Security Center. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Configurer la collecte de données
> * Définir des stratégies de sécurité
> * Afficher et résoudre des problèmes d’intégrité de configuration
> * Examiner les menaces détectées

Avance toohello suivant didacticiel toolearn plus d’informations sur la création d’un élément de configuration/CD de pipeline avec Jenkins, GitHub et Docker.

> [!div class="nextstepaction"]
> [Créer une infrastructure d’intégration continue/de livraison continue avec Jenkins, GitHub et Docker](tutorial-jenkins-github-docker-cicd.md)

