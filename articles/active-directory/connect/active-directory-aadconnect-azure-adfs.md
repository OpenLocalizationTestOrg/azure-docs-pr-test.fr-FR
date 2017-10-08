---
title: aaaActive Directory Federation Services dans Azure | Documents Microsoft
description: "Dans ce document, vous allez apprendre comment toodeploy AD FS dans Azure pour la haute disponibilité."
keywords: "déployer AD FS dans azure, déployer AD FS azure, azure AD FS, azure ad fs, déployer AD FS, déployer ad fs, adfs dans azure, déployer AD FS dans azure, déployer AD FS dans azure, azure d’adfs, introduction tooAD FS, Azure, AD FS dans Azure, iaas, ADFS, déplacer adfs tooazure"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2c39271f7569b9ce395dce2f53f5ba5a4897b132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Déploiement d’Active Directory Federation Services dans Azure
AD FS simplifie et sécurise la fédération des identités et l’authentification unique (SSO) sur le web. Fédération avec Azure AD ou Office 365 permet aux utilisateurs de tooauthenticate à l’aide locale des informations d’identification et accéder à toutes les ressources dans le cloud. Par conséquent, il est important de toohave une haute disponibilité ADFS infrastructure tooensure accéder tooresources à la fois localement et dans le cloud de hello. Déploiement d’AD FS dans Azure peut aider à atteindre hello haute disponibilité requise avec les efforts minimale.
Le déploiement d’AD FS dans Azure présente toute une série d’avantages, notamment :

* **Haute disponibilité** -puissance hello de groupes à haute disponibilité Azure, vous vérifiez une infrastructure hautement disponible.
* **TooScale facile** – ont besoin de performances plus ? Migrer facilement des machines de puissantes toomore en seulement quelques clics dans Azure
* **La géo-redondance** – avec redondance géographique Azure vous pouvez être sûr que votre infrastructure est hautement disponible monde hello
* **TooManage facile** – avec les options de gestion est hautement simplifiée dans le portail Azure, la gestion de votre infrastructure est très facile et conviviale 

## <a name="design-principles"></a>Principes de conception
![Conception du déploiement](./media/active-directory-aadconnect-azure-adfs/deployment.png)

diagramme de Hello ci-dessus montre hello recommandé toostart topologie de base déploiement de votre infrastructure AD FS dans Azure. principes de Hello hello différents composants de la topologie de hello sont répertoriées ci-dessous :

* **Contrôleur de domaine / serveurs ADFS**: si votre environnement compte moins de 1 000 utilisateurs, vous pouvez installer simplement le rôle AD FS sur vos contrôleurs de domaine. Si vous ne souhaitez pas que tout impact sur les performances sur les contrôleurs de domaine hello ou si vous avez plus de 1 000 utilisateurs, puis déployer AD FS sur des serveurs distincts.
* **Serveur WAP** – il est nécessaire toodeploy les serveurs Proxy d’Application Web, afin que les utilisateurs peuvent accéder hello AD FS quand ils ne sont pas sur le réseau d’entreprise hello également.
* **Réseau de périmètre**: serveurs de Proxy d’Application Web hello seront placées dans hello réseau de périmètre et TCP/443 uniquement l’accès est autorisé entre hello DMZ et sous-réseau interne de hello.
* **Équilibreurs de charge**: tooensure haute disponibilité des serveurs AD FS et Proxy d’Application Web, nous recommandons d’utiliser un équilibreur de charge interne pour les serveurs AD FS et l’équilibrage de charge Azure pour les serveurs Proxy d’Application Web.
* **Haute disponibilité**: déploiement de tooprovide redondance tooyour AD FS, il est recommandé de regrouper deux ou plusieurs machines virtuelles dans un groupe à haute disponibilité pour les charges de travail similaires. Dans une telle configuration, vous avez la garantie qu’au moins une des machines virtuelles sera disponible pendant un événement de maintenance planifié ou non planifié.
* **Comptes de stockage**: il est recommandé de comptes de stockage toohave deux. Ayant un seul compte de stockage peut entraîner des toocreation d’un point de défaillance unique et peut entraîner hello toobecome de déploiement non disponible dans un scénario peu probable où le compte de stockage hello tombe en panne. Le choix de deux comptes de stockage permet d’associer un compte de stockage pour chaque ligne d’erreur.
* **Séparation des réseaux** : les serveurs Web Application Proxy doivent être déployés sur un réseau DMZ distinct. Vous pouvez diviser un réseau virtuel en deux sous-réseaux, puis déployez hello ou les serveurs Proxy d’Application Web dans un sous-réseau isolé. Vous pouvez simplement configurer les paramètres de groupe de sécurité de réseau hello pour chaque sous-réseau et autoriser uniquement les communications entre les sous-réseaux de deux hello requises. Voir les détails ci-dessous en fonction du scénario de déploiement

## <a name="steps-toodeploy-ad-fs-in-azure"></a>Étapes toodeploy AD FS dans Azure
les étapes de Hello indiquées dans cette section plan hello guide toodeploy hello ci-dessous représentés infrastructure AD FS dans Azure.

### <a name="1-deploying-hello-network"></a>1. Déploiement hello réseau
Comme indiqué ci-dessus, vous pouvez soit créer deux sous-réseaux dans un même réseau virtuel, soit créer deux réseaux virtuels totalement différents. Cet article se concentre sur le déploiement d’un seul réseau virtuel subdivisé en deux sous-réseaux. Il s’agit actuellement d’une approche plus simple que deux des réseaux virtuels distincts nécessiterait une passerelle tooVNet de réseau virtuel pour les communications.

**1.1 Création d’un réseau virtuel**

![Création d’un réseau virtuel](./media/active-directory-aadconnect-azure-adfs/deploynetwork1.png)

Bonjour portail Azure, le réseau virtuel et que vous pouvez déployer hello réseau et un sous-réseau virtuels immédiatement avec un simple clic. Sous-réseau INT est également définie et est maintenant prêt à être toobe de machines virtuelles ajoutée.
étape suivante de Hello est tooadd un autre réseau de sous-réseau toohello, autrement dit, les sous-réseaux hello réseau de périmètre. toocreate hello sous-réseau du réseau de périmètre, il vous suffit

* Sélectionnez le réseau de hello qui vient d’être créé
* Dans les propriétés de hello sélectionnez sous-réseau
* Dans hello sous-réseau Panneau de configuration, cliquez sur hello bouton Ajouter
* Indiquez hello sous-réseau nom et l’adresse espace informations toocreate hello sous-réseau

![Sous-réseau](./media/active-directory-aadconnect-azure-adfs/deploynetwork2.png)

![DMZ de sous-réseau](./media/active-directory-aadconnect-azure-adfs/deploynetwork3.png)

**1.2. Création des groupes de sécurité réseau de hello**

Un groupe de sécurité réseau (NSG) contient une liste de règles de liste de contrôle d’accès (ACL) qui autorisent ou refusent le trafic réseau tooyour des instances de machine virtuelle dans un réseau virtuel. Des groupes de sécurité réseau peuvent être associés à des sous-réseaux ou à des instances de machine virtuelle au sein de ce sous-réseau. Lorsqu’un groupe de sécurité réseau est associé à un sous-réseau, listes de contrôle hello appliquent instances de machine virtuelle tooall hello dans ce sous-réseau.
Pour les besoins de hello de ce guide, nous allons créer deux groupes de sécurité réseau : un pour un réseau interne et un réseau de périmètre. Ces groupes seront respectivement nommés NSG_INT et NSG_DMZ.

![Création d’un groupe de sécurité réseau](./media/active-directory-aadconnect-azure-adfs/creatensg1.png)

Après hello que NSG est créé, il y a 0 règles de trafic sortant entrants et 0. Une fois les rôles hello sur les serveurs respectifs hello installé et opérationnel, puis hello règles entrantes et sortantes peuvent être effectuées en fonction toohello souhaité au niveau de sécurité.

![Initialisation d’un groupe de sécurité réseau](./media/active-directory-aadconnect-azure-adfs/nsgint1.png)

Une fois créés, hello NSG associer NSG_INT sous-réseau INT et NSG_DMZ avec un sous-réseau de réseau de périmètre. Exemple de capture d’écran :

![Configuration d’un groupe de sécurité réseau](./media/active-directory-aadconnect-azure-adfs/nsgconfigure1.png)

* Cliquez sur Panneau de configuration de sous-réseaux tooopen hello pour les sous-réseaux
* Sélectionnez tooassociate de sous-réseau hello avec hello NSG 

Après la configuration, un panneau hello pour les sous-réseaux doit se présenter comme ci-dessous :

![Sous-réseaux après un groupe de sécurité réseau](./media/active-directory-aadconnect-azure-adfs/nsgconfigure2.png)

**1.3. Créer la connexion tooon local**

Nous devons un local tooon connexion dans l’ordre toodeploy hello contrôleur de domaine (DC) dans azure. Azure propose divers tooconnect d’options de connectivité votre tooyour d’infrastructure sur site infrastructure Azure.

* Point à site
* Réseau virtuel de site à site
* ExpressRoute

Il est recommandé de toouse ExpressRoute. ExpressRoute vous permet de créer des connexions privées entre les centres de données Azure et une infrastructure locale ou dans un environnement de colocalisation. Les connexions ExpressRoute ne sont pas établies via hello Internet public. Ils offrent plus la fiabilité, débits plus importants, latences moindres et une sécurité accrue par rapport aux connexions classiques sur Internet de hello.
S’il est recommandé de toouse ExpressRoute, vous pouvez choisir n’importe quelle méthode de connexion plus adapté à votre organisation. lire des différentes options de connectivité à l’aide d’ExpressRoute, toolearn plus d’informations sur ExpressRoute et hello [présentation technique d’ExpressRoute](https://aka.ms/Azure/ExpressRoute).

### <a name="2-create-storage-accounts"></a>2. Créer des comptes de stockage
Dans la haute disponibilité de commande toomaintain et éviter la dépendance sur un seul compte de stockage, vous pouvez créer deux comptes de stockage. Diviser les machines hello dans chaque groupe à haute disponibilité en deux groupes et puis affectez chaque groupe à un compte de stockage distinct.

![Créer des comptes de stockage](./media/active-directory-aadconnect-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3. Créer des groupes à haute disponibilité
Pour chaque rôle (contrôleur de domaine/AD FS et WAP), créer des groupes à haute disponibilité qui contient les 2 machines à hello minimale. ce afin de garantir une meilleure disponibilité pour chaque rôle. Alors que les groupes à haute disponibilité de hello création, il est essentiel toodecide suivant de hello :

* **Domaines d’erreur**: machines virtuelles dans hello même erreur de domaine partagent hello même source d’alimentation et commutateur réseau physique. Il est recommandé d’utiliser au moins 2 domaines d’erreur. valeur par défaut de Hello est 3 et vous pouvez la laisser ainsi à des fins de hello de ce déploiement
* **Mettre à jour des domaines**: les Machines appartenant toohello même domaine de mise à jour sont redémarrés ensemble pendant une mise à jour. Vous souhaitez toohave au moins 2 domaines de mise à jour. Hello la valeur par défaut est 5, et vous pouvez la laisser ainsi à des fins de hello de ce déploiement

![Groupes à haute disponibilité](./media/active-directory-aadconnect-azure-adfs/availabilityset1.png)

Créer hello suivant à haute disponibilité

| Groupe à haute disponibilité | Rôle | Domaines d’erreur | Domaines de mise à jour |
|:---:|:---:|:---:|:--- |
| contosodcset |Contrôleur de domaine/AD FS |3 |5 |
| contosowapset |WAP |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4. Déployer les machines virtuelles
étape suivante de Hello est toodeploy virtuels qui hébergera hello différents rôles de votre infrastructure. Nous vous recommandons d’affecter au moins deux machines virtuelles à chaque groupe à haute disponibilité. Créez quatre machines virtuelles pour le déploiement de base hello.

| Ordinateur | Rôle | Sous-réseau | Groupe à haute disponibilité | Compte de stockage | Adresse IP |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |Contrôleur de domaine/AD FS |INT |contosodcset |contososac1 |Statique |
| contosodc2 |Contrôleur de domaine/AD FS |INT |contosodcset |contososac2 |Statique |
| contosowap1 |WAP |DMZ |contosowapset |contososac1 |Statique |
| contosowap2 |WAP |DMZ |contosowapset |contososac2 |Statique |

Comme vous l’avez peut-être remarqué, aucun groupe de sécurité réseau n’a été spécifié, Il s’agit, car azure vous permet d’utiliser un groupe de sécurité réseau au niveau du sous-réseau hello. Ensuite, vous pouvez contrôler le trafic réseau de machine à l’aide de hello que NSG individuel associé soit sous-réseau de hello quoi objet de carte réseau hello. Pour en savoir plus, consultez l’article [Présentation du groupe de sécurité réseau](https://aka.ms/Azure/NSG).
Adresse IP statique est recommandée si vous gérez hello DNS. Vous pouvez utiliser Azure DNS et à la place dans les enregistrements DNS de hello pour votre domaine, consultez toohello de nouveaux ordinateurs par leurs noms de domaine complets Azure.
Après que le déploiement de hello est terminée, votre volet de l’ordinateur virtuel doit ressembler à ci-dessous :

![Machines virtuelles déployées](./media/active-directory-aadconnect-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-hello-domain-controller--ad-fs-servers"></a>5. Contrôleur de domaine configuration hello / serveurs AD FS
 Dans l’ordre tooauthenticate toute requête entrante, AD FS devez contrôleur de domaine toocontact hello. toosave hello voyage coûteux à partir du contrôleur de domaine local tooon Azure pour l’authentification, il est recommandé de toodeploy un réplica hello du contrôleur de domaine dans Azure. Dans l’ordre tooattain haute disponibilité, il est recommandé de toocreate un ensemble de disponibilité au moins 2 contrôleurs de domaine.

| Contrôleur de domaine | Rôle | Compte de stockage |
|:---:|:---:|:---:|
| contosodc1 |Réplica |contososac1 |
| contosodc2 |Réplica |contososac2 |

* Promouvoir les deux serveurs de hello en tant que contrôleurs de domaine réplica avec DNS
* Configurez les serveurs de hello AD FS en installant le rôle hello AD FS à l’aide du Gestionnaire de serveur hello.

### <a name="6-deploying-internal-load-balancer-ilb"></a>6. Déployer l’équilibreur de charge interne (ILB)
**6.1. Créer hello équilibrage de charge interne**

toodeploy un équilibrage de charge interne, sélectionnez les équilibreurs de charge dans hello portail Azure et cliquez sur Ajouter (+).

> [!NOTE]
> Si vous ne voyez pas **équilibreurs de charge** dans le menu, cliquez sur **Parcourir** Bonjour bas à gauche du portail de hello et faites défiler jusqu'à ce que vous voyiez **équilibreurs de charge**.  Puis cliquez sur les tooadd en étoile hello jaune il tooyour menu. Sélectionnez maintenant hello nouvelle configuration équilibrage de charge icône tooopen hello panneau toobegin d’équilibrage de charge hello.
> 
> 

![Rechercher un équilibreur de charge](./media/active-directory-aadconnect-azure-adfs/browseloadbalancer.png)

* **Nom**: donner n’importe quel équilibreur de charge toohello nom approprié
* **Schéma**: étant donné que cet équilibrage de charge sera placé devant les serveurs hello AD FS et est conçu pour les connexions de réseau interne uniquement, sélectionnez « Interne »
* **Réseau virtuel**: choisissez un réseau virtuel hello où vous déployez des services AD FS
* **Sous-réseau**: choisissez le sous-réseau interne de hello ici
* **Affectation d’adresses IP** : Statique

![Équilibreur de charge interne](./media/active-directory-aadconnect-azure-adfs/ilbdeployment1.png)

Après avoir cliqué sur Créer et hello équilibrage de charge interne est déployé, vous devez le voir dans la liste hello des équilibreurs de charge :

![Équilibreurs de charge après équilibreur de charge interne](./media/active-directory-aadconnect-azure-adfs/ilbdeployment2.png)

Étape suivante consiste à tooconfigure pool principal d’hello et sonde de back-end hello.

**6.2. Configuration du pool principal de l’équilibreur de charge interne**

Sélectionnez hello nouvellement créé équilibrage de charge interne dans le panneau de configuration hello équilibreurs de charge. Il ouvre le panneau des paramètres hello. 

1. Sélectionnez les pools principaux à partir du Panneau de paramètres hello
2. Bonjour ajouter le panneau de configuration de pool principal, cliquez sur Ajouter une machine virtuelle
3. Dans le panneau qui s’affiche, vous pouvez choisir votre groupe à haute disponibilité
4. Choisissez le groupe à haute disponibilité hello AD FS

![Configuration du pool principal de l’équilibreur de charge interne](./media/active-directory-aadconnect-azure-adfs/ilbdeployment3.png)

**6.3. Configuration de la sonde**

Dans le panneau des paramètres d’équilibrage de charge interne hello, sélectionnez les sondes.

1. Cliquez sur Ajouter
2. Indiquez les détails de la sonde a. **Nom** : nom de la sonde b. **Protocole** : TCP c. **Port** : 443 (HTTPS) d. **Intervalle**: 5 (valeur par défaut) – il s’agit d’intervalle de salutation auquel équilibrage de charge interne chercheront machines hello dans le pool principal d’hello e. **Limite de seuil de fonctionnement anormal**: 2 (par défaut val ue) – il s’agit de seuil hello d’échecs de sonde consécutifs après lequel équilibrage de charge interne déclare un ordinateur dans hello principal pool non réactif et arrêter envoi du trafic tooit.

![Configuration de la sonde d’équilibreur de charge interne](./media/active-directory-aadconnect-azure-adfs/ilbdeployment4.png)

**6.4. Création des règles d’équilibrage de charge**

Commande tooeffectively solde hello du trafic, hello équilibrage de charge interne doit être configuré avec les règles d’équilibrage de charge. Dans l’ordre toocreate une règle d’équilibrage de charge, 

1. Sélectionnez la règle à partir du Panneau de paramètres hello Hello équilibrage de charge interne d’équilibrage de charge
2. Cliquez sur Ajouter Bonjour panneau règle équilibrage de charge
3. Bonjour ajouter charge équilibrage Panneau de règle une. **Nom**: fournissez un nom pour la règle de hello b. **Protocole** : sélectionnez TCP c. **Port** : 443 d. **Port principal** : 443 e. **Pool principal**: sélectionnez pool hello vous avez créé pour AD FS hello cluster f antérieur. **Sonde**: sonde hello sélectionnez créé précédemment pour les serveurs AD FS

![Configuration des règles d’équilibrage de l’équilibreur de charge interne](./media/active-directory-aadconnect-azure-adfs/ilbdeployment5.png)

**6.5. Mise à jour du serveur DNS avec l’équilibreur de charge interne**

Atteindre le serveur DNS de tooyour et créer un enregistrement CNAME pour hello équilibrage de charge interne. Hello CNAME doit être hello service de fédération avec l’adresse IP de hello pointant adresse IP toohello hello équilibrage de charge interne. Par exemple, si hello adresse DIP d’équilibrage de charge interne est 10.3.0.8 et le service de fédération hello installé est fs.contoso.com, puis créez un enregistrement CNAME pour fs.contoso.com pointant too10.3.0.8.
Cela garantit que toutes les communications concernant fs.contoso.com finissent à hello équilibrage de charge interne et sont correctement acheminé.

### <a name="7-configuring-hello-web-application-proxy-server"></a>7. Configuration de serveur de Proxy d’Application Web hello
**7.1. Configuration des serveurs de hello Proxy d’Application Web serveurs tooreach AD FS**

Dans l’ordre tooensure qui sont des serveurs Proxy d’Application Web tooreach en mesure des serveurs de hello AD FS derrière hello équilibrage de charge interne, créez un enregistrement dans %systemroot%\system32\drivers\etc\hosts hello pour hello équilibrage de charge interne. Notez que hello nom unique (DN) doit être le nom de service de fédération hello, par exemple fs.contoso.com. Et entrée d’adresse IP hello doit être l’adresse IP de d’équilibrage de charge hello (10.3.0.8 comme exemple de hello) de.

**7.2. L’installation du rôle de Proxy d’Application Web hello**

Après que vous être assuré que les serveurs Proxy d’Application Web sont des serveurs de hello AD FS en mesure de tooreach derrière l’équilibrage de charge interne, vous pouvez ensuite installer les serveurs Proxy d’Application Web hello. Les serveurs Proxy d’Application Web ne doit pas agir toohello joint à un domaine. Installer des rôles de Proxy d’Application Web de hello sur deux serveurs de Proxy d’Application Web hello en sélectionnant le rôle d’accès à distance hello. le Gestionnaire de serveur Hello guide installation de WAP toocomplete hello.
Pour plus d’informations sur la façon de lire toodeploy WAP, [installer et configurer le serveur Proxy d’Application Web de hello](https://technet.microsoft.com/library/dn383662.aspx).

### <a name="8--deploying-hello-internet-facing-public-load-balancer"></a>8.  Déploiement hello équilibrage de charge Internet face (Public)
**8.1.  Création d’un équilibreur de charge (public) accessible sur Internet**

Bonjour portail Azure, sélectionnez les équilibreurs de charge et puis cliquez sur Ajouter. Dans le volet d’équilibrage de charge de créer de hello, entrez hello informations suivantes

1. **Nom**: nom de l’équilibrage de charge hello
2. **Schéma**: Public ; cette option indique à Azure que cet équilibreur de charge aura besoin d’une adresse publique.
3. **Adresse IP**: créez une nouvelle adresse IP (dynamique)

![Équilibreur de charge accessible sur Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment1.png)

Après le déploiement, l’équilibrage de charge hello s’affiche dans la liste de programmes d’équilibrage de charge hello.

![Liste des équilibreurs de charge](./media/active-directory-aadconnect-azure-adfs/elbdeployment2.png)

**8.2. Affecter une adresse IP publique de DNS étiquette toohello**

Cliquez sur à l’entrée d’équilibrage de charge hello nouvellement créé dans hello charge équilibrages panneau toobring panneau hello pour la configuration. Suivez au-dessous étapes tooconfigure hello DNS pour l’adresse IP publique hello :

1. Cliquez sur l’adresse IP publique de hello. Panneau hello pour l’adresse IP publique hello et ses paramètres s’ouvre
2. Cliquez sur Configuration
3. Indiquez un nom DNS. Celle-ci figurera alors comme nom DNS public hello auxquelles vous pouvez accéder depuis n’importe où, par exemple contosofs.westus.cloudapp.azure.com. Vous pouvez ajouter une entrée DNS externe pour le service de fédération hello (par exemple, fs.contoso.com) qui résout le nom DNS de toohello Hello externe hello charger équilibrage (contosofs.westus.cloudapp.azure.com).

![Configuration de l’équilibreur de charge accessible sur Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment3.png) 

![Configuration de l’équilibreur de charge accessible sur Internet (DNS)](./media/active-directory-aadconnect-azure-adfs/elbdeployment4.png)

**8.3. Configuration d’un pool principal pour l’équilibreur de charge (public) accessible sur Internet** 

Hello suivent même procédure que dans la création d’équilibreur de charge interne hello, pool principal de tooconfigure hello pour Internet face (Public) équilibreur de charge en tant que la disponibilité de hello défini pour les serveurs de proxy hello. Par exemple, contosowapset.

![Configuration d’un pool principal pour l’équilibreur de charge accessible sur Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment5.png)

**8.4. Configuration de la sonde**

Suivez hello même procédure que dans la configuration de sonde hello de tooconfigure d’équilibrage de charge interne hello pour le pool principal d’hello de serveurs de proxy.

![Configuration de la sonde d’équilibreur de charge accessible sur Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment6.png)

**8.5. Création d’une ou plusieurs règles d’équilibrage de charge**

Suivez hello mêmes étapes que dans l’équilibrage de charge du hello tooconfigure à équilibrage de charge interne de règle pour le port TCP 443.

![Configuration des règles d’équilibrage de l’équilibreur de charge accessible sur Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment7.png)

### <a name="9-securing-hello-network"></a>9. Sécurisation de hello réseau
**9.1. Sécurisation de sous-réseau interne de hello**

En général, vous devez hello suivant les règles tooefficiently sécuriser votre sous-réseau interne (dans l’ordre de hello comme indiqué ci-dessous)

| Règle | Description | Flux |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |Autoriser les communications HTTPS hello à partir du réseau de périmètre |Trafic entrant |
| DenyInternetOutbound |Aucun toointernet d’accès |Règle de trafic sortant |

![Règles d’accès INT (entrant)](./media/active-directory-aadconnect-azure-adfs/nsg_int.png)

[comment]: <> (![règles d’accès INT (entrant)](./media/active-directory-aadconnect-azure-adfs/nsgintinbound.png)) [comment]: <> (![(règles d’accès INT (sortant)](./media/active-directory-aadconnect-azure-adfs/nsgintoutbound.png))

**9.2. Sécurisation de sous-réseau du réseau de périmètre hello**

| Règle | Description | Flux |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |Autoriser HTTPS à partir d’internet toohello réseau de périmètre |Trafic entrant |
| DenyInternetOutbound |N’est pas HTTPS toointernet est bloquée |Règle de trafic sortant |

![Règles d’accès EXT (entrant)](./media/active-directory-aadconnect-azure-adfs/nsg_dmz.png)

[comment]: <> (![règles d’accès EXT (entrant)](./media/active-directory-aadconnect-azure-adfs/nsgdmzinbound.png)) [comment]: <> (![(règles d’accès EXT (sortant)](./media/active-directory-aadconnect-azure-adfs/nsgdmzoutbound.png))

> [!NOTE]
> Si l’authentification du certificat utilisateur client (authentification clientTLS à l’aide de certificats utilisateur X509) est requise, AD FS nécessite l’activation du port TCP 49443 pour l’accès entrant.
> 
> 

### <a name="10-test-hello-ad-fs-sign-in"></a>10. Tester l’authentification dans hello AD FS
Hello simple est tootest QU'ADFS se trouve à l’aide de page de IdpInitiatedSignon.aspx hello. Dans l’ordre en mesure de toobe : toodo, il est nécessaire de tooenable hello IdpInitiatedSignOn sur les propriétés de hello AD FS. Suivez les étapes de hello ci-dessous tooverify votre installation d’AD FS

1. Exécuter hello ci-dessous l’applet de commande sur le serveur du hello AD FS, à l’aide de PowerShell, tooset il tooenabled.
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true 
2. À partir d’une machine externe, accédez à https://adfs.thecloudadvocate.com/adfs/ls/IdpInitiatedSignon.aspx  
3. Vous devez voir hello AD FS page comme ci-dessous :

![Page de connexion de test](./media/active-directory-aadconnect-azure-adfs/test1.png)

Si l’authentification aboutit, vous obtenez le message de confirmation ci-dessous :

![Réussite du test](./media/active-directory-aadconnect-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Modèle de déploiement d’AD FS dans Azure
modèle de Hello déploie une configuration de 6 ordinateur, 2 pour les contrôleurs de domaine, les services AD FS et WAP.

[Modèle de déploiement d’AD FS dans Azure](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

Vous pouvez utiliser un réseau virtuel existant ou créer un nouveau réseau virtuel lors du déploiement de ce modèle. Hello différents paramètres disponibles pour la personnalisation du déploiement de hello sont répertoriées ci-dessous avec la description de hello de l’utilisation du paramètre hello hello processus de déploiement. 

| Paramètre | Description |
|:--- |:--- |
| Lieu |Hello région toodeploy hello ressources en, par exemple, est des États-Unis. |
| StorageAccountType |type Hello Hello compte de stockage créé |
| VirtualNetworkUsage |Indique si un réseau virtuel sera créé ou si un compte existant est utilisé |
| VirtualNetworkName |nom de Hello de hello tooCreate de réseau virtuel, obligatoire sur l’utilisation du réseau virtuel nouveau ou existant |
| VirtualNetworkResourceGroupName |Spécifie le nom hello hello du groupe de ressources où se trouve le réseau virtuel hello. Lorsque vous utilisez un réseau virtuel existant, cela devient un paramètre obligatoire pour le déploiement de hello puisse trouver hello des ID de réseau virtuel hello |
| VirtualNetworkAddressRange |Hello de plage d’adresses de hello nouveau réseau virtuel, obligatoire si vous créez un réseau virtuel |
| InternalSubnetName |nom de Hello de sous-réseau interne de hello, obligatoire sur les deux options d’utilisation de réseau virtuel (nouvelles ou existantes) |
| InternalSubnetAddressRange |plage d’adresses Hello de sous-réseau interne hello, qui contient les hello ADFS et les contrôleurs de domaine serveurs, obligatoires si vous créez un réseau virtuel. |
| DMZSubnetAddressRange |plage d’adresses Hello du sous-réseau de réseau de périmètre hello, qui contient les hello proxy serveurs d’applications Windows, obligatoires si vous créez un réseau virtuel. |
| DMZSubnetName |nom de Hello de sous-réseau interne de hello, obligatoire sur les deux options d’utilisation de réseau virtuel (nouvelles ou existantes). |
| ADDC01NICIPAddress |adresse IP interne de Hello de hello premier contrôleur de domaine, cette adresse IP statique recevront toohello contrôleur de domaine et doit être une adresse ip valide dans un sous-réseau interne de hello |
| ADDC02NICIPAddress |adresse IP interne de Hello de hello second contrôleur de domaine, cette adresse IP statique recevront toohello contrôleur de domaine et doit être une adresse ip valide dans un sous-réseau interne de hello |
| ADFS01NICIPAddress |Hello interne adresse IP du serveur AD FS de la première hello, cette adresse IP statique recevront un serveur AD FS toohello et doit être une adresse ip valide dans un sous-réseau interne de hello |
| ADFS02NICIPAddress |Hello interne adresse IP du serveur AD FS de la deuxième hello, cette adresse IP statique recevront un serveur AD FS toohello et doit être une adresse ip valide dans un sous-réseau interne de hello |
| WAP01NICIPAddress |Hello interne adresse IP du premier serveur WAP de hello, cette adresse IP statique recevront serveur WAP de toohello et doit être une adresse ip valide dans le sous-réseau du réseau de périmètre hello |
| WAP02NICIPAddress |Hello interne adresse IP du serveur de proxy d’application Web de deuxième hello, cette adresse IP statique recevront serveur WAP de toohello et doit être une adresse ip valide dans le sous-réseau du réseau de périmètre hello |
| ADFSLoadBalancerPrivateIPAddress |adresse IP interne de Hello Hello ADFS l’équilibrage de charge, cette adresse IP statique recevront équilibrage de charge toohello et doit être une adresse ip valide dans un sous-réseau interne de hello |
| ADDCVMNamePrefix |Préfixe du nom de machine virtuelle pour les contrôleurs de domaine |
| ADFSVMNamePrefix |Préfixe du nom de machine virtuelle pour les serveurs ADFS |
| WAPVMNamePrefix |Préfixe du nom de machine virtuelle pour les serveurs WAP |
| ADDCVMSize |taille de machine virtuelle Hello hello contrôleurs de domaine |
| ADFSVMSize |taille de machine virtuelle Hello serveurs ADFS de hello |
| WAPVMSize |taille de machine virtuelle Hello de serveurs de proxy hello |
| AdminUserName |nom Hello de hello administrateur local d’ordinateurs virtuels hello |
| AdminPassword |mot de passe Hello pour le compte administrateur local hello d’ordinateurs virtuels hello |

## <a name="additional-resources"></a>Ressources supplémentaires
* [Groupes à haute disponibilité](https://aka.ms/Azure/Availability) 
* [Équilibrage de charge Azure](https://aka.ms/Azure/ILB)
* [Équilibreur de charge interne](https://aka.ms/Azure/ILB/Internal)
* [Équilibreur de charge accessible sur Internet](https://aka.ms/Azure/ILB/Internet)
* [Comptes de stockage](https://aka.ms/Azure/Storage)
* [Réseaux virtuels Azure](https://aka.ms/Azure/VNet)
* [Liens AD FS et Web Application Proxy](http://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>Étapes suivantes
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)
* [Configuration et gestion de vos services AD FS avec Azure AD Connect](active-directory-aadconnectfed-whatis.md)
* [Déploiement des services AD FS haute disponibilité par-delà les frontières dans Azure avec Azure Traffic Manager](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)

