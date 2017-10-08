---
title: "déploiement de FS aaaHigh disponibilité géographique d’entre AD dans Azure avec Azure Traffic Manager | Documents Microsoft"
description: "Dans ce document, vous allez apprendre comment toodeploy AD FS dans Azure pour la haute disponibilité."
keywords: "AD fs avec le Gestionnaire de trafic Azure, AD FS avec Azure Traffic Manager, géographique, centre de données multiples, les centres de données géographiques, plusieurs centres de données géographiques, déploiement AD FS dans azure, déploiement AD FS azure, azure AD FS, azure ad fs, déploiement AD FS, déploiement ad fs, adfs dans azure, déployer AD FS dans azure, déployer AD FS dans azure, azure d’adfs, introduction tooAD FS, Azure, AD FS dans Azure iaas, ADFS, déplace adfs tooazure"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: c5838d749cdc5c8aabbe62b255d568525da747ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Déploiement des services AD FS haute disponibilité par-delà les frontières dans Azure avec Azure Traffic Manager
[Déploiement d’AD FS dans Azure](active-directory-aadconnect-azure-adfs.md) fournit des indications pas à pas toohow vous pouvez déployer une infrastructure AD FS simple pour votre organisation dans Azure. Cet article fournit des étapes hello déploiement toocreate géographique entre des services AD FS dans Azure à l’aide [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md). Azure Traffic Manager permet de créer des géographiquement spread haute disponibilité et l’infrastructure AD FS de hautes performances pour votre organisation en rendant l’utilisation de la plage des méthodes de routage disponible toosuit autre a besoin à partir de l’infrastructure de hello.

Une infrastructure AD FS hautement disponible et par-delà les frontières permet d’obtenir ce qui suit :

* **Élimination de point de défaillance unique :** avec les fonctionnalités de basculement de Azure Traffic Manager, vous pouvez obtenir une infrastructure AD FS hautement disponible même lorsqu’un des centres de données hello dans une partie du globe de hello tombe en panne
* **Amélioration des performances :** que vous pouvez utiliser hello suggéré déploiement dans cet article de tooprovide une infrastructure AD FS hautes performances qui permet aux utilisateurs de s’authentifier plus rapidement. 

## <a name="design-principles"></a>Principes de conception
![Conception générale](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

principes de conception de base Hello sera identique, comme répertorié dans les principes de conception dans l’article hello déploiement AD FS dans Windows Azure. diagramme de Hello ci-dessus illustre une simple extension de la région géographique du tooanother hello déploiement de base. Voici certains tooconsider points lors de l’extension de votre zone géographique toonew de déploiement

* **Réseau virtuel :** vous devez créer un nouveau réseau virtuel dans la zone géographique hello souhaité d’infrastructure de toodeploy supplémentaire AD FS. Dans le diagramme hello ci-dessus vous voyez Geo1 réseau et réseau virtuel de Geo2 hello deux réseaux virtuels dans chaque région géographique.
* **Contrôleurs de domaine et serveurs AD FS dans le nouveau réseau virtuel géographique :** il est recommandé de toodeploy des contrôleurs de domaine dans la région nouveau hello afin que les serveurs hello AD FS dans la nouvelle région de hello n’ont pas toocontact un contrôleur de domaine dans une autre mesure réseau absent toocomplete une authentification et ainsi améliorer ses performances de hello.
* **Comptes de stockage :** les comptes de stockage sont associés à une région. Étant donné que vous déployez des ordinateurs dans une nouvelle région géographique, vous aurez des nouveaux comptes de stockage toocreate toobe utilisée dans la région de hello.  
* **Groupes de sécurité réseau :** comme les comptes de stockage, les groupes de sécurité réseau créés dans une région ne peuvent pas être utilisés dans une autre région géographique. Par conséquent, vous devez toocreate nouveau réseau sécurité groupes similaires toothose dans la zone géographique première hello pour le sous-réseau INT et réseau de périmètre dans une région nouveau hello.
* **Étiquettes de DNS pour les adresses IP publiques :** Azure Traffic Manager peut faire référence tooendpoints uniquement via les étiquettes DNS. Par conséquent, vous êtes toocreate requis des étiquettes DNS pour les adresses IP publiques des hello externe équilibreurs de charge.
* **Azure Traffic Manager :** Microsoft Azure Traffic Manager vous permet de répartition hello toocontrol utilisateur trafic tooyour points de terminaison service en cours d’exécution dans différents centres de données monde hello. Azure Traffic Manager fonctionne au niveau DNS de hello. Il utilise DNS réponses toodirect par l’utilisateur le trafic distribué tooglobally points de terminaison. Les clients, connecteront les points de terminaison toothose directement. Différentes options de routage de performances, Weighted et la priorité, vous pouvez facilement choisir d’option de routage hello adaptée aux besoins de votre organisation. 
* **Connectivité de tooV-net net-V entre deux régions :** vous n’avez pas besoin toohave la connectivité entre les réseaux virtuels hello lui-même. Étant donné que chaque réseau virtuel a accès toodomain contrôleurs et serveur AD FS et WAP en soi, ils peuvent fonctionner sans les connexions entre les réseaux virtuels hello dans des régions différentes. 

## <a name="steps-toointegrate-azure-traffic-manager"></a>Étapes toointegrate Azure Traffic Manager
### <a name="deploy-ad-fs-in-hello-new-geographical-region"></a>Déployer AD FS dans la région nouveau hello
Suivez les étapes de hello et les instructions de [déploiement AD FS dans Windows Azure](active-directory-aadconnect-azure-adfs.md) toodeploy hello même topologie dans la région nouveau hello.

### <a name="dns-labels-for-public-ip-addresses-of-hello-internet-facing-public-load-balancers"></a>Étiquettes DNS pour les adresses IP publiques de hello Internet faisant face à des équilibreurs de charge (public)
Comme indiqué ci-dessus, hello Azure Traffic Manager peut uniquement faire référence étiquettes tooDNS comme points de terminaison et par conséquent, il est important de toocreate les étiquettes DNS pour les adresses IP publiques des hello externe équilibreurs de charge. Capture d’écran ci-dessous montre comment vous pouvez configurer votre nom DNS pour l’adresse IP publique de hello. 

![Nom DNS](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Déploiement d’Azure Traffic Manager
Suivez les étapes de hello ci-dessous toocreate un profil traffic manager. Pour plus d’informations, vous pouvez également faire référence trop[gérer un profil Traffic Manager de Azure](../traffic-manager/traffic-manager-manage-profiles.md).

1. **Créez un profil Traffic Manager :** donnez un nom unique à votre profil Traffic Manager. Ce nom de profil de hello fait partie du nom DNS de hello et agit comme un préfixe pour l’étiquette de nom de domaine Traffic Manager hello. nom de Hello / préfixe est ajouté too.trafficmanager.net toocreate un nom DNS pour votre gestionnaire de trafic. Hello capture d’écran ci-dessous montre le Gestionnaire de trafic hello préfixe DNS configurée comme mysts et l’étiquette DNS résultante sera mysts.trafficmanager.net. 
   
    ![Création de profil Traffic Manager](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **Méthode de routage du trafic :** trois options de routage sont disponibles dans Traffic Manager :
   
   * Priorité 
   * Performances
   * Pondéré
     
     **Performances** hello est recommandé d’infrastructure d’option tooachieve très réactif AD FS. Toutefois, vous pouvez choisir une méthode de routage qui convient mieux à vos besoins de déploiement. fonctionnalité de Hello AD FS n’est pas affectée par l’option de routage hello sélectionnée. Pour plus d’informations, consultez l’article [Méthodes de routage du trafic de Traffic Manager](../traffic-manager/traffic-manager-routing-methods.md) . Bonjour capture d’écran de l’exemple ci-dessus, vous pouvez voir hello **performances** méthode sélectionnée.
3. **Configurer des points de terminaison :** dans la page de hello traffic manager, cliquez sur les points de terminaison et sélectionnez Ajouter. Cela ouvre un ajout point de terminaison page semblable toohello capture d’écran ci-dessous
   
   ![Configuration des points de terminaison](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   Pour hello différentes entrées, suivez les indications hello ci-dessous :
   
   **Type :** sélectionner le point de terminaison Azure comme nous sera pointant vers tooan Azure adresse IP publique.
   
   **Nom :** créer un nom que vous souhaitez tooassociate avec point de terminaison hello. Cela n’est pas de nom DNS de hello et n’a aucune incidence sur les enregistrements DNS.
   
   **Type de ressource cible :** sélectionner Public l’adresse IP en tant que propriété de toothis valeur hello. 
   
   **Ressource cible :** vous obtiendrez une option toochoose des étiquettes DNS différents hello vous disposez dans votre abonnement. Choisissez hello que DNS étiquette de point de terminaison toohello correspondant que vous configurez.
   
   Ajouter un point de terminaison pour chaque zone géographique que vous voulez que hello Azure Traffic Manager tooroute le trafic.
   Pour plus d’informations et des instructions détaillées sur la façon de tooadd / configurer des points de terminaison dans le Gestionnaire de trafic, consultez trop[ajouter, désactiver, activer ou supprimer des points de terminaison](../traffic-manager/traffic-manager-endpoints.md)
4. **Configurer la sonde :** dans la page de hello traffic manager, cliquez sur la Configuration. Dans la page de configuration hello, vous devez toochange hello moniteur paramètres tooprobe au port HTTP 80 et /adfs/probe de chemin d’accès relatif
   
    ![Configurer une analyse](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **Assurez-vous qu’état hello de points de terminaison hello est connecté, une fois la configuration de hello terminée**. Si tous les points de terminaison sont dans l’état 'Dégradé', Azure Traffic Manager effectuera un meilleure tentative tooroute hello le trafic en supposant que les diagnostics hello est incorrect et tous les points de terminaison sont accessibles.
   > 
   > 
5. **Modification des enregistrements DNS pour Azure Traffic Manager :** votre service de fédération doit être un nom de Azure Traffic Manager DNS CNAME toohello. Créez un enregistrement CNAME dans hello enregistrements DNS publics afin que toute personne qui tente de service de fédération hello tooreach réellement atteint hello Azure Traffic Manager.
   
    Par exemple, toopoint hello federation service fs.fabidentity.com toohello Traffic Manager, vous devez tooupdate votre hello toobe enregistrement de ressource DNS suivant :
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-hello-routing-and-ad-fs-sign-in"></a>Test hello routage et l’authentification dans AD FS
### <a name="routing-test"></a>Test de routage
Un test de base pour le routage de hello serait tootry ping hello fédération nom DNS du service à partir d’un ordinateur dans chaque zone géographique. En fonction de la méthode de routage hello choisi, point de terminaison hello qu'il interroge réellement apparaîtront dans l’affichage de ping hello. Par exemple, si vous avez sélectionné les performances hello routage, puis le point de terminaison hello plus proche toohello région du client de hello sera atteinte. Voici instantané hello de deux commandes ping à partir de deux ordinateurs de client autre région, dans la région Asie de l’est et dans l’ouest des États-Unis. 

![Test de routage](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>Test de connexion des services AD FS
tootest de façon plus simple Hello AD FS est à l’aide de page de IdpInitiatedSignon.aspx hello. Dans l’ordre en mesure de toobe : toodo, il est nécessaire de tooenable hello IdpInitiatedSignOn sur les propriétés de hello AD FS. Suivez les étapes de hello ci-dessous tooverify votre installation d’AD FS

1. Exécuter hello ci-dessous l’applet de commande sur le serveur du hello AD FS, à l’aide de PowerShell, tooset il tooenabled. 
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
2. À partir d’une machine externe, accédez à https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx
3. Vous devez voir hello AD FS page comme ci-dessous :
   
    ![Test ADFS : demande d’authentification](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    En cas de connexion réussie, vous obtenez un message de réussite semblable à celui qui suit :
   
    ![Test ADFS : authentification réussie](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>Liens connexes
* [Déploiement des services AD FS dans Azure](active-directory-aadconnect-azure-adfs.md)
* [Qu’est-ce que Traffic Manager ?](../traffic-manager/traffic-manager-overview.md)
* [Méthodes de routage du trafic de Traffic Manager](../traffic-manager/traffic-manager-routing-methods.md)

## <a name="next-steps"></a>Étapes suivantes
* [Gestion d’un profil Azure Traffic Manager](../traffic-manager/traffic-manager-manage-profiles.md)
* [Ajouter, désactiver, activer ou supprimer des points de terminaison](../traffic-manager/traffic-manager-endpoints.md) 

