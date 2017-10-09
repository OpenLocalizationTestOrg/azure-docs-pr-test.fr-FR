---
title: "aaaSecuring accès tooAzure RemoteApp et au-delà | Documents Microsoft"
description: "Découvrez comment sécuriser l’accès tooAzure RemoteApp à l’aide de l’accès conditionnel dans Azure Active Directory"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: a19b0b09-ab26-4beb-80bb-33a46da39887
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 98dfe69e2f5fa5014b6eb3157e01f131c287134d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-remoteapp-and-beyond"></a>Sécurisation des accès tooAzure RemoteApp et au-delà
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Dans cet article nous donne une vue d’ensemble de la façon dont un administrateur peut définir un canal de sécuriser l’accès à partir des utilisateurs finaux hello, via Azure RemoteApp et se terminant par une ressource sécurisée, par exemple une base de données SQL ou une autre application back-end. Hello vise toomake assurer que seuls les utilisateurs autorisés hello de réunion souhaité conditions peuvent accéder à des applications à distance, et qui hello terminale sécurisé uniquement accessibles à partir de l’environnement de Azure RemoteApp hello contrôlé et non à partir d’autres emplacements.

Il existe 3 domaines principaux hello admin doit toolook à :

![Considérations relatives à l’accès conditionnel à Azure RemoteApp](./media/remoteapp-secureaccess/ra-conditionalenvironment.png)

Lisez la suite pour plus d’informations et des réponses aux questions de toothese.

## <a name="who-can-access-hello-collection"></a>Qui peut accéder à la collection de hello ?
administrateur de Hello choisit les utilisateurs hello qui peuvent accéder à des applications à distance dans la collection de hello. Vous pouvez utiliser des comptes professionnels ou scolaires Azure Active Directory (Azure AD) (précédemment appelés « comptes professionnels ») ou des comptes Microsoft (par exemple @outlook.com). La plupart des scénarios d’entreprise utilisent des comptes Azure AD ; ils vous permettent d’utiliser les fonctionnalités d’accès conditionnel décrites plus loin et sont également hello uniquement dans les cas pour les collections de joints au domaine. rest Hello d’article de hello suppose que vous utilisez des comptes Azure AD avec Azure RemoteApp.

**Ce que nous avons accompli :**

À l’aide d’Azure AD comptes toocontrol accès tooAzure que RemoteApp nous donne deux choses :

1. Nous savons toujours hello applications nous avez publié et accéder à n’importe quel back end ces applications se connectent à accès.
2. Nous contrôle hello sous-jacent Azure AD afin que nous pouvons créer et supprimer des comptes utilisateur, définir des stratégies de mot de passe, utilisent l’authentification multifacteur, etc.. 

## <a name="how-is-hello-collection-accessed-from-where"></a>L’accès à la collection de hello ? À partir d’où ?
Généralement, les administrateurs souhaitent toodefine stratégies pour l’accès à un environnement côté Internet public, tels que Azure RemoteApp. Par exemple, qu’ils souhaitent tooensure que les utilisateurs l’accès à environnement hello d’en dehors du réseau d’entreprise de hello accéder toouse l’authentification multifacteur (MFA) toogain ; ou peut-être qu’ils doivent être bloqués complètement.

Azure RemoteApp les administrateurs peuvent utiliser les fonctionnalités de hello disponibles via les stratégies d’accès conditionnel Azure AD Premium tooset pour leur environnement Azure RemoteApp. Ils peuvent également utiliser la génération de rapports et d’alertes toomonitor fonctionnalités comment les environnement hello sont accessible.

### <a name="how-tooset-up-conditional-access-for-azure-remoteapp"></a>Comment tooset d’accès conditionnel pour Azure RemoteApp
Nous sommes toowalk continu via un exemple de scénario : hello Azure RemoteApp non-membre environnement de toohello tooblock accès lorsque les utilisateurs sont en dehors du réseau d’entreprise de hello.

> [!NOTE]
> Nous supposons que vous avez mis à niveau Azure AD toohello niveau Premium et que vous avez créé au moins une collection Azure RemoteApp.
> 
> 

1. Dans le portail Azure, cliquez sur hello **Active Directory** onglet. Puis cliquez sur le répertoire hello tooconfigure.
   
   N’oubliez pas : Accès conditionnel est une propriété de votre annuaire et non de Azure RemoteApp, donc la configuration est effectuée au niveau du répertoire hello. Cela signifie également que vous devez toobe hello directory administrateur toomake ces modifications.
2. Cliquez sur **Applications**, puis cliquez sur **Microsoft Azure RemoteApp** tooset accès conditionnel. Notez que vous pouvez configurer un accès conditionnel pour chaque application « logiciel en tant que service » séparément dans votre répertoire.
   ![Configuration de l’accès conditionnel pour Azure RemoteApp](./media/remoteapp-secureaccess/ra-conditionalaccessscreen.png)
3. Sur hello **configurer** onglet, définissez **activer les règles d’accès** tooON.
   ![Activer des règles d’accès pour Azure RemoteApp](./media/remoteapp-secureaccess/ra-enableaccessrules.png)
4. Vous pouvez maintenant configurer des règles et choisissez qui tooapply à :
   
   1. Choisissez **bloquer l’accès à l’extérieur de travail** toocompletely empêcher les utilisateurs d’accéder à Azure RemoteApp en dehors de l’environnement de réseau hello vous spécifiez.
   2. Cliquez sur option hello ci-dessous toodefine hello plages d’adresses qui constituent votre « réseau approuvé. » Tous les éléments figurant en dehors de celles-ci seront rejetées.
5. Tester votre configuration en lançant le client d’Azure RemoteApp hello à partir d’une adresse IP en dehors de la plage de hello spécifiée. Une fois que vous vous êtes connecté avec vos informations d’identification Azure AD, un message semblable à ce qui suit doit s’afficher :

![Accès refusé tooAzure RemoteApp](./media/remoteapp-secureaccess/ra-accessdenied.png)

### <a name="future-conditional-access-features"></a>Futures fonctionnalités d’accès conditionnel
équipe Azure Active Directory de Hello fonctionne sur les nouvelles fonctionnalités de l’accès conditionnel. Les administrateurs seront en mesure de toocreate de nouveaux types de règles au-delà des règles selon l’emplacement réseau. Une version préliminaire publique de nouvelles fonctionnalités de hello doit être disponible bientôt.

### <a name="how-toomonitor-access-tooazure-remoteapp"></a>Comment accéder à toomonitor tooAzure RemoteApp
Un toouse fonctionnalité intéressante en même temps que l’accès conditionnel est une fonctionnalité de création de rapports de Azure Active Directory Premium hello. Vous pouvez utiliser toomonitor de rapports qui accède à votre environnement et détecter toute activité suspecte.

Par exemple, vous pouvez voir les noms de hello d’utilisateurs hello ayant accédé à Azure RemoteApp, combien de fois qu’elle et à quel moment.

1. Dans le Portail Azure, cliquez sur **Active Directory**, puis sur votre annuaire.
2. Accédez toohello **rapports** onglet.
3. Dans la liste hello des rapports, sélectionnez **l’utilisation des applications** sous **intégré applications**.
   
   Des statistiques agrégées pour Azure RemoteApp s’affichent. 
   ![Statistiques agrégées sur l’accès à Azure RemoteApp](./media/remoteapp-secureaccess/ra-accessstats.png)
4. Cliquez sur hello application tooreveal plus d’informations sur les utilisateurs qui accèdent à Azure RemoteApp.
   ![Statistiques des accès utilisateur pour Azure RemoteApp](./media/remoteapp-secureaccess/ra-userstats.png)

### <a name="summary"></a>Résumé
Avec Azure Active Directory Premium, vous pouvez définir des règles tooAzure RemoteApp accès (et d’autres logiciels comme une application de service disponible via Azure AD). Les règles sont actuellement limitée toonetwork les stratégies selon l’emplacement, mais seront Bonjour futures étendus tooother les aspects de la gestion de l’entreprise.

Azure AD Premium offre également la création de rapports et fonctionnalités hello contrôle hello admin d’étendre davantage de contrôle a sur leur environnement Azure RemoteApp.

## <a name="how-do-i-make-sure-my-secure-resource-is-accessible-only-from-my-azure-remoteapp-environment"></a>Comment m’assurer que ma ressource sécurisée est accessible uniquement à partir de mon environnement Azure RemoteApp ?
Dans les sections précédentes de cet article nous se concentre sur la sécurisation d’un environnement de Azure RemoteApp toohello accès. Nous avons fait qui en choisissant les utilisateurs de hello qui sont autorisés à accéder et de configurer le contrôle d’accès règles toofurther comment ils peuvent utiliser le service de hello.

Un scénario courant pour les déploiements Azure RemoteApp est que les applications distantes hello doivent toocommunicate avec une ressource de serveur principal, par exemple une base de données SQL. Cette ressource est hébergée localement (par exemple, dans un réseau d’entreprise) ou dans le cloud hello (par exemple, dans Azure IaaS). Les administrateurs souhaitent souvent toomake vraiment que hello principale ressource uniquement accessible par les applications déployées via Azure RemoteApp et pas par exemple par une application en cours d’exécution directement sur l’ordinateur de l’utilisateur et d’y accéder via Internet public. Azure RemoteApp est souvent considéré comme hello centralisée et l’environnement sécurisé et donc hello seul chemin par le biais duquel les utilisateurs doivent interagir avec hello ressource principale.

solution de Hello est tooplace à la fois hello Azure RemoteApp environnement et la ressource sécurisée hello hello même Azure réseau virtuel (VNET). Si la ressource de hello est dans un autre site, vous pouvez établir une connexion VPN de site à site, par exemple toocreate un centre de données Azure hello spanning réseau virtuel et l’environnement hello client local.

Azure RemoteApp prend en charge deux types de déploiement de collection dans lesquels vous pouvez fournir votre propre réseau virtuel :

* Non à un domaine : hello applications auront « ligne de vue « Hello autres ressources Bonjour réseau virtuel. Par exemple, cela peut être utilisé tooconnect applications tooa base de données SQL qui utilise l’authentification SQL (applications s’authentifient utilisateur hello directement par rapport à la base de données hello)
* Joint à un domaine : hello machines virtuelles utilisées par Azure RemoteApp sont tooa joints à un contrôleur de domaine hello réseau virtuel. Cela est utile lorsque les applications de hello doivent tooauthenticate par rapport à un contrôleur de domaine Windows dans la ressource de commande tooget accès tooa back-end.
  ![Collection jointe à un domaine dans Azure RemoteApp](./media/remoteapp-secureaccess/ra-domainjoined.png)

### <a name="how-toocreate-a-secure-connection-between-azure-and-my-on-premises-environment"></a>Comment toocreate une connexion sécurisée entre Azure et de mon environnement local
Plusieurs options de configuration permettent de connecter vos environnements Azure et local. Une bonne vue d’ensemble des options de hello est disponible ici.

Avec Azure RemoteApp vous devez, tooconfigure votre réseau virtuel tout d’abord et ensuite l’utiliser pendant le processus de création hello de votre collection. 

## <a name="hello-complete-solution"></a>solution complète de Hello
diagramme de Hello ci-dessous montre solution complète de hello où nous avons créé un canal d’un accès sécurisé à partir de l’utilisateur final de hello, via Azure RemoteApp (ARA), dans la ressource de serveur principal hello.
![Sécuriser Azure RemoteApp](./media/remoteapp-secureaccess/ra-secureoverview.png) dans étape 1 nous hello utilisateurs sélectionnés et créé des règles d’accès qui déterminent comment ARA est accessible. Dans l’exemple hello ci-dessous nous permettent uniquement l’accès aux utilisateurs qui travaillent à partir du réseau d’entreprise de hello. Utilisateurs non conformes ne seront pas du tout environnement de ARA tooaccess en mesure de hello.
Dans la phase 2, nous avons exposée ressource de serveur principal hello uniquement via la configuration de réseau virtuel/VPN hello qui nous contrôler. Azure RemoteApp a été placée dans hello même réseau virtuel. résultat final de Hello est que les ressources hello uniquement accessibles via l’environnement de ARA hello.

