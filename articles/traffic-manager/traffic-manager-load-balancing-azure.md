---
title: "l’équilibrage de charge aaaUsing services dans Azure | Documents Microsoft"
description: "Ce didacticiel vous montre comment un scénario à l’aide de toocreate hello portefeuille d’équilibrage de charge Azure : Traffic Manager, la passerelle d’Application et équilibrage de charge."
services: traffic-manager
documentationcenter: 
author: liumichelle
manager: vitinnan
editor: 
ms.assetid: f89be3be-a16f-4d47-bcae-db2ab72ade17
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/27/2016
ms.author: limichel
ms.openlocfilehash: d217047102d8c4828250dc0733e8ec9ee1e84b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-load-balancing-services-in-azure"></a>Utilisation des services d’équilibrage de charge dans Azure

## <a name="introduction"></a>Introduction

Microsoft Azure propose plusieurs services destinés à gérer la distribution et l’équilibrage de la charge du trafic réseau. Vous pouvez utiliser ces services individuellement ou combiner leurs méthodes, selon vos besoins, la solution optimale de toobuild hello.

Dans ce didacticiel, nous avons tout d’abord définir un cas d’utilisation client et voir comment elle peut être rendue plus robustes et performantes à l’aide de hello suivant portefeuille d’équilibrage de charge Azure : Traffic Manager, la passerelle d’Application et équilibrage de charge. Ensuite, nous fournir des instructions détaillées pour la création d’un déploiement qui est géographiquement redondant, distribue le trafic tooVMs et vous permet de gérer différents types de demandes.

À un niveau conceptuel, chacun de ces services joue un rôle distinct dans la hiérarchie de l’équilibrage de charge hello.

* **Traffic Manager** assure un équilibrage de charge DNS global. Il examine les requêtes DNS entrantes et répond avec un point de terminaison sain, conformément aux hello routage client hello de stratégie a sélectionné. Les différentes méthodes de routage disponibles sont les suivantes :
  * Performances routage toosend hello demandeur toohello le plus proche point de terminaison en termes de latence.
  * Priorité de routage toodirect tout le trafic tooan point de terminaison, avec d’autres points de terminaison en tant que sauvegarde.
  * Pondérée alternée routage, qui répartit le trafic en fonction de pondération hello affecté tooeach le point de terminaison.

  Hello se connecte directement toothat le point de terminaison. Azure Traffic Manager détecte lorsqu’un point de terminaison n’est pas intègre et puis redirections hello instance intègre tooanother de clients. Consultez trop[documentation d’Azure Traffic Manager](traffic-manager-overview.md) toolearn plus d’informations sur les service hello.
* **Application Gateway** intègre ADC (Application Delivery Controller) sous la forme d’un service, qui offre diverses fonctionnalités d’équilibrage de charge de couche 7 pour votre application. Il permet de productivité de batterie de serveurs web toooptimize clients en déchargeant la passerelle d’application sollicitant beaucoup le processeur SSL arrêt toohello. Autres fonctionnalités de routage de couche 7 incluent distribution alternée de trafic entrant d’affinité de session basée sur un cookie, le routage basé sur le chemin d’accès URL et hello capacité toohost plusieurs sites Web derrière une passerelle d’application unique. Cette dernière peut être configurée en tant que passerelle accessible sur Internet, passerelle interne uniquement ou une combinaison des deux. La passerelle Application Gateway est une solution Azure entièrement gérée, très évolutive et hautement disponible. Elle fournit un ensemble complet de fonctionnalités de diagnostics et de journalisation, pour une meilleure gérabilité.
* **L’équilibrage de charge** fait partie intégrante de pile de Azure SDN hello, fournir hautes performances et à faible latence couche 4 l’équilibrage de charge des services pour les protocoles de tous les protocoles UDP et TCP. Il gère les connexions entrantes et sortantes. Vous pouvez configurer des points de terminaison publics et internes équilibrée et définir des règles toomap entrant des destinations de pool de connexions tooback-end à l’aide de TCP et HTTP-détection d’intégrité options toomanage disponibilité du service.

## <a name="scenario"></a>Scénario

Dans ce scénario, nous utilisons un site web simple qui affiche deux types de contenu : des images et des pages web affichées dynamiquement. site Web de Hello doit être géographiquement redondant, et il doit utiliser ses utilisateurs hello le plus proche (latence la plus faible) toothem d’emplacement. Hello développeur a décidé que les URL qui correspondent aux hello modèle/images / * sont pris en charge à partir d’un pool dédié de machines virtuelles qui sont différentes de rest hello de batterie de serveurs web hello.

En outre, le pool d’ordinateurs virtuels par défaut hello fournit du contenu dynamique hello doit tootalk tooa principal base de données qui est hébergé sur un cluster de haute disponibilité. déploiement complet de Hello est défini par le biais du Gestionnaire de ressources Azure.

À l’aide de Traffic Manager, la passerelle d’Application et équilibrage de charge permet cette tooachieve du site Web de ces objectifs de conception :

* **Redondance géographique de plusieurs**: si une région tombe en panne, les itinéraires de Traffic Manager de trafic en toute transparence toohello de région le plus proche sans intervention de propriétaire de l’application hello.
* **Réduit la latence**: étant donné que Traffic Manager dirige automatiquement hello toohello le plus proche de la région client, une latence plus faible des expériences client de hello lors de la demande de contenu de page Web hello.
* **Évolutivité indépendante**: étant donné que la charge de travail hello web application est séparée par type de contenu, propriétaire de l’application hello peut évoluer hello demande les charges de travail indépendantes des autres. Passerelle d’application garantit que le trafic de hello est routé toohello les pools de droite selon hello spécifié règles et la santé de l’application hello hello.
* **L’équilibrage de charge interne**: équilibrage de charge, car est devant le cluster de haute disponibilité hello, uniquement hello active et intègre point de terminaison pour une base de données est exposée toohello application. En outre, un administrateur de base de données peut optimiser la charge de travail hello en répartissant les réplicas actifs et passifs sur cluster hello indépendante de l’application frontale hello. Équilibrage de charge remet le cluster de connexions toohello haute disponibilité et garantit que seules les bases de données intègres reçoivent les demandes de connexion.

Hello diagramme suivant illustre architecture hello de ce scénario :

![Diagramme de l’architecture d’équilibrage de charge](./media/traffic-manager-load-balancing-azure/scenario-diagram.png)

> [!NOTE]
> Cet exemple n'est qu’une des nombreuses configurations possibles de services d’équilibrage de charge hello Azure offre. Traffic Manager, la passerelle d’Application et équilibrage de charge peuvent être mélangés et mis en correspondance toobest selon vos besoins de l’équilibrage de charge. Par exemple, s’il n’est pas nécessaire de faire appel au déchargement SSL ou au traitement de la couche 7, Load Balancer peut être utilisé à la place d’Application Gateway.

## <a name="setting-up-hello-load-balancing-stack"></a>Configuration de la pile de l’équilibrage de charge hello

### <a name="step-1-create-a-traffic-manager-profile"></a>Étape 1 : créer un profil Traffic Manager

1. Bonjour portail Azure, cliquez sur **nouveau**et puis recherche hello marketplace pour « Profil Traffic Manager ».
2. Sur hello **profil créer Traffic Manager** panneau, entrez hello informations de base suivantes :

  * **Nom** : donnez un nom de préfixe DNS à votre profil Traffic Manager.
  * **Méthode de routage**: sélectionnez hello-le routage du trafic de stratégie de méthode. Pour plus d’informations sur les méthodes de hello, consultez [les méthodes de routage du trafic sur le Gestionnaire de trafic](traffic-manager-routing-methods.md).
  * **Abonnement**: sélectionnez l’abonnement hello qui contient le profil de hello.
  * **Groupe de ressources**: groupe de ressources hello Select qui contient le profil de hello. Il peut s’agir d’un groupe de ressources nouveau ou existant.
  * **Emplacement du groupe de ressources**: service de Traffic Manager est global et non liées tooa emplacement. Toutefois, vous devez spécifier une région pour le groupe de hello où résident les métadonnées hello associée au profil de Traffic Manager hello. Cet emplacement n’a aucun impact sur la disponibilité du runtime hello du profil de hello.

3. Cliquez sur **créer** toogenerate hello profil Traffic Manager.

  ![Panneau Créer un profil Traffic Manager](./media/traffic-manager-load-balancing-azure/s1-create-tm-blade.png)

### <a name="step-2-create-hello-application-gateways"></a>Étape 2 : Créer hello passerelles d’application

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur **nouveau** > **réseau** > **passerelle d’Application**.
2. Entrez hello suit les informations de base sur la passerelle d’application hello :

  * **Nom**: nom hello de passerelle d’application hello.
  * **Taille de la référence (SKU)**: hello la taille de la passerelle d’application hello, disponible en tant que petite, moyenne ou grande.
  * **Le nombre d’instances**: nombre de hello d’instances, une valeur comprise entre 2 et 10.
  * **Groupe de ressources**: groupe de ressources hello qui détient la passerelle d’application hello. Il peut s’agir d’un groupe existant, ou d’un nouveau groupe.
  * **Emplacement**: région hello pour la passerelle d’application hello, qui est hello même emplacement que le groupe de ressources hello. l’emplacement Hello est important, car le réseau virtuel de hello et l’adresse IP publique doivent être Bonjour même emplacement que la passerelle de hello.
3. Cliquez sur **OK**.
4. Définir le réseau virtuel de hello, sous-réseau, IP frontale et configurations d’écouteur pour la passerelle d’application hello. Dans ce scénario, les adresses IP frontales hello sont **Public**, qui lui permet de toobe ajoutée ultérieurement comme un toohello de point de terminaison du profil Traffic Manager.
5. Configurer le port d’écoute hello avec l’une des options suivantes de hello :
    * Si vous utilisez HTTP, il n’exécute aucune opération tooconfigure. Cliquez sur **OK**.
    * Une configuration supplémentaire est requise pour l’utilisation du protocole HTTPS. Consultez trop[créer une passerelle d’application](../application-gateway/application-gateway-create-gateway-portal.md), en commençant à l’étape 9. Lorsque vous avez terminé la configuration de hello, cliquez sur **OK**.

#### <a name="configure-url-routing-for-application-gateways"></a>Configurer le routage d’URL pour les passerelles Application Gateway

Lorsque vous choisissez un pool principal, une passerelle d’application qui est configurée avec une règle basée sur le chemin d’accès prend un modèle de chemin d’accès de l’URL de demande hello de distribution Round-robin tooround Ajout. Dans ce scénario, nous ajoutons une règle basée sur le chemin d’accès de toodirect n’importe quelle URL avec « /images/\*« pool de serveurs toohello image. Pour plus d’informations sur la configuration des URL de routage en fonction du chemin d’accès pour une passerelle d’application, consultez trop[créer une règle basée sur le chemin d’accès pour une passerelle d’application](../application-gateway/application-gateway-create-url-route-portal.md).

![Diagramme de couche web Application Gateway](./media/traffic-manager-load-balancing-azure/web-tier-diagram.png)

1. À partir de votre groupe de ressources, passez l’instance toohello de passerelle d’application hello que vous avez créé dans la précédente section de hello.
2. Sous **paramètres**, sélectionnez **pools principaux**, puis sélectionnez **ajouter** tooadd hello machines virtuelles que vous souhaitez tooassociate avec les pools de hello couche web principal.
3. Sur hello **ajouter le pool principal** panneau, entrez le nom hello du pool principal de hello et toutes les adresses IP de hello d’ordinateurs hello qui résident dans le pool de hello. Dans ce scénario, nous connectons deux pools de serveurs principaux de machines virtuelles.

  ![Panneau Ajouter un pool principal d’Application Gateway](./media/traffic-manager-load-balancing-azure/s2-appgw-add-bepool.png)

4. Sous **paramètres** de passerelle d’application hello, sélectionnez **règles**, puis cliquez sur hello **chemin d’accès en fonction** bouton tooadd une règle.

  ![Bouton Basé sur le chemin de la zone Règles de la passerelle Application Gateway](./media/traffic-manager-load-balancing-azure/s2-appgw-add-pathrule.png)

5. Sur hello **ajouter une règle basée sur le chemin d’accès** panneau, configurer la règle de hello en fournissant hello informations suivantes.

   Paramètres de base :

   + **Nom**: nom convivial de hello de règle hello qui est accessible dans le portail de hello.
   + **Écouteur**: écouteur hello qui est utilisé pour la règle de hello.
   + **Par défaut du pool principal**: hello toobe principal pool utilisé hello règle par défaut.
   + **Paramètres HTTP par défaut**: hello HTTP toobe de paramètres utilisé hello règle par défaut.

   Règles basées sur le chemin :

   + **Nom**: nom convivial de hello d’une règle basée sur le chemin d’accès hello.
   + **Chemins d’accès**: règle de chemin d’accès hello qui est utilisé pour transférer le trafic.
   + **Pool principal**: hello toobe principal pool utilisé avec cette règle.
   + **Paramètre HTTP**: hello HTTP toobe de paramètres utilisé avec cette règle.

   > [!IMPORTANT]
   > Chemins : pour être valides, les chemins doivent commencer par « / ». Hello générique «\*» est autorisée uniquement à la fin de hello. Exemples valides : /xyz, /xyz\* ou /xyz/\*.

   ![Panneau Ajouter une règle basée sur le chemin d’Application Gateway](./media/traffic-manager-load-balancing-azure/s2-appgw-pathrule-blade.png)

### <a name="step-3-add-application-gateways-toohello-traffic-manager-endpoints"></a>Étape 3 : Ajouter des points de terminaison Traffic Manager application passerelles toohello

Dans ce scénario, Traffic Manager est passerelles tooapplication connecté (tel que configuré dans les étapes précédentes de hello) qui résident dans des régions différentes. Maintenant que les passerelles d’application hello sont configurés, étape suivante de hello est tooconnect les tooyour profil Traffic Manager.

1. Ouvrez le profil Traffic Manager. toodo, donc dans votre groupe de ressources ou la recherche de nom hello du profil Traffic Manager de hello de **toutes les ressources**.
2. Dans le volet gauche de hello, sélectionnez **points de terminaison**, puis cliquez sur **ajouter** tooadd un point de terminaison.

  ![Bouton Ajouter de la zone Points de terminaison Traffic Manager](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint.png)

3. Sur hello **ajouter le point de terminaison** panneau, créer un point de terminaison en entrant hello informations suivantes :

  * **Type**: sélectionnez le type hello du point de terminaison tooload-solde. Dans ce scénario, sélectionnez **point de terminaison Azure** étant donné que nous nous connectons il toohello application passerelle instances qui ont été configurés précédemment.
  * **Nom**: entrez le nom hello du point de terminaison hello.
  * **Type de ressource cible**: sélectionnez **adresse IP publique** puis, sous **ressource cible**, sélectionnez l’adresse IP publique de la passerelle d’application hello qui a été configuré précédemment hello.

   ![Panneau Ajouter un point de terminaison de Traffic Manager](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint-blade.png)

4. Maintenant vous pouvez tester votre configuration en y accédant par hello DNS de votre profil Traffic Manager (dans cet exemple : TrafficManagerScenario.trafficmanager.net). Vous pouvez renvoyer les demandes, afficher ou arrêter des ordinateurs virtuels et les serveurs web qui ont été créés dans des régions différentes et modifier tootest de paramètres de profil de Traffic Manager hello votre programme d’installation.

### <a name="step-4-create-a-load-balancer"></a>Étape 4 : Créer un équilibrage de charge

Dans ce scénario, équilibrage de charge distribue les connexions à partir de bases de données toohello hello pour web niveau au sein d’un cluster de haute disponibilité.

Si votre cluster de haute disponibilité de base de données à l’aide de SQL Server AlwaysOn, consultez trop[configurer un ou plusieurs toujours sur disponibilité écouteurs de groupe](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) pour obtenir des instructions pas à pas.

Pour plus d’informations sur la configuration d’un équilibreur de charge interne, consultez [créer un équilibreur de charge interne Bonjour Azure portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md).

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur **nouveau** > **réseau** > **équilibrage de charge**.
2. Sur hello **équilibrage de charge créer** panneau, choisissez un nom pour votre équilibreur de charge.
3. Ensemble hello **Type** trop**interne**, puis choisissez le réseau virtuel approprié de hello et un sous-réseau pour tooreside d’équilibrage de charge hello dans.
4. Sous **Attribution d’adresses IP**, sélectionnez **Dynamique** ou **Statique**.
5. Sous **groupe de ressources**, choisissez le groupe de ressources hello pour l’équilibrage de charge hello.
6. Sous **emplacement**, choisissez hello de région appropriée pour l’équilibrage de charge hello.
7. Cliquez sur **créer** équilibrage de charge toogenerate hello.

#### <a name="connect-a-back-end-database-tier-toohello-load-balancer"></a>Se connecter à un équilibrage de charge de toohello de niveau base de données principale

1. À partir de votre groupe de ressources, trouver l’équilibrage de charge hello qui a été créé dans les étapes précédentes hello.
2. Sous **paramètres**, cliquez sur **pools principaux**, puis cliquez sur **ajouter** tooadd un pool principal.

  ![Panneau Ajouter un pool principal de Load Balancer](./media/traffic-manager-load-balancing-azure/s4-ilb-add-bepool.png)

3. Sur hello **ajouter le pool principal** panneau, entrez le nom hello du pool principal de hello.
4. Ajouter des ordinateurs individuels ou un pool de disponibilité ensemble toohello back-end.

#### <a name="configure-a-probe"></a>Configurer une sonde

1. Dans votre équilibreur de charge, sous **paramètres**, sélectionnez **sondes**, puis cliquez sur **ajouter** tooadd une sonde.

 ![Panneau Ajouter une sonde de Load Balancer](./media/traffic-manager-load-balancing-azure/s4-ilb-add-probe.png)

2. Sur hello **ajouter sonde** panneau, entrez le nom hello pour la sonde de hello.
3. Sélectionnez hello **protocole** pour la sonde de hello. Pour une base de données, vous choisirez sans doute une sonde TCP plutôt qu’une sonde HTTP. toolearn en savoir plus sur les sondes d’équilibrage de charge, consultez trop[sondes d’équilibrage de charge comprendre](../load-balancer/load-balancer-custom-probe-overview.md).
4. Entrez hello **Port** de votre toobe de base de données utilisée pour accéder à la sonde de hello.
5. Sous **intervalle**, spécifiez la fréquence à laquelle tooprobe hello application.
6. Sous **seuil défaillance**, spécifiez le nombre hello d’échecs de sonde en continu qui doit se produire pour hello principal VM toobe est considéré comme non intègre.
7. Cliquez sur **OK** sonde de hello toocreate.

#### <a name="configure-hello-load-balancing-rules"></a>Configurer des règles d’équilibrage de charge hello

1. Sous **paramètres** de votre équilibreur de charge, sélectionnez **règles d’équilibrage de charge**, puis cliquez sur **ajouter** toocreate une règle.
2. Sur hello **règle d’équilibrage ajouter** panneau, entrez hello **nom** pour la règle d’équilibrage de charge hello.
3. Choisissez hello **adresse IP frontale** de hello charge équilibrage, **protocole**, et **Port**.
4. Sous **port principal**, spécifiez hello port toobe est utilisé dans le pool principal hello.
5. Sélectionnez hello **pool principal** et hello **sonde** qui ont été créés dans hello précédentes étapes tooapply hello règle.
6. Sous **persistance de Session**, choisissez comment vous souhaitez que hello sessions toopersist.
7. Sous **délais d’inactivité**, spécifiez hello nombre de minutes avant un délai d’inactivité.
8. Sous **IP flottante**, sélectionnez **Désactivé** ou **Activé**.
9. Cliquez sur **OK** règle de hello toocreate.

### <a name="step-5-connect-web-tier-vms-toohello-load-balancer"></a>Étape 5 : Se connecter à équilibrage de charge toohello couche web machines virtuelles

Maintenant, nous configurons hello adresse et l’équilibrage de charge frontal port IP dans les applications hello qui sont exécutent sur vos machines virtuelles de couche web pour toutes les connexions de base de données. Cette configuration est spécifique toohello les applications qui s’exécutent sur ces ordinateurs virtuels. adresse IP de destination de hello tooconfigure et le port, consultez la documentation d’application toohello. adresse IP toofind hello hello front-end, Bonjour portail Azure, passez pool d’adresses IP frontal toohello hello **paramètres d’équilibrage de charge** panneau.

![Volet de navigation Pool d’IP du serveur principal de Load Balancer](./media/traffic-manager-load-balancing-azure/s5-ilb-frontend-ippool.png)

## <a name="next-steps"></a>Étapes suivantes

* [Vue d’ensemble de Traffic Manager](traffic-manager-overview.md)
* [Vue d’ensemble d’Application Gateway](../application-gateway/application-gateway-introduction.md)
* [Vue d’ensemble d’Azure Load Balancer](../load-balancer/load-balancer-overview.md)
