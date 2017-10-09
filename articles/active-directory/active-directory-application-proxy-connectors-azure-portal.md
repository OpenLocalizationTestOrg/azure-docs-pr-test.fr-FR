---
title: "applications aaaPublishing sur des réseaux distincts et les emplacements à l’aide de groupes de connecteurs de Proxy d’application Azure AD | Documents Microsoft"
description: "Aborde comment toocreate et gérer des groupes de connecteurs de Proxy d’Application Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: 8c9a84b365eab28eaaeb343d4d1e2e6990537fec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>Publier des applications sur des réseaux et emplacements distincts à l’aide de groupes de connecteurs
> [!div class="op_single_selector"]
> * [Portail Azure](active-directory-application-proxy-connectors-azure-portal.md)
> * [portail Azure Classic](active-directory-application-proxy-connectors.md)
>

Les clients utilisent le proxy d’application Azure AD pour obtenir toujours plus de scénarios et d’applications. C’est pourquoi nous avons rendu le proxy d’application encore plus flexible en activant davantage de topologies. Vous pouvez créer des groupes de connecteurs de Proxy d’Application afin que vous pouvez affecter des connecteurs spécifiques tooserve des applications spécifiques. Cette fonctionnalité vous offre plus toooptimize de contrôle et les méthodes votre déploiement de Proxy d’Application. 

Groupe de connecteur tooa est affecté à chaque connecteur de Proxy d’Application. Tous les hello connecteurs appartenant toohello même groupe de connecteurs agissent comme une unité distincte pour la haute disponibilité et l’équilibrage de charge. Tous les connecteurs appartient le groupe de connecteurs tooa. Si vous ne créez pas de groupes, tous vos connecteurs se trouvent dans un groupe par défaut. Votre administrateur peut créer des groupes et assigner toothem connecteurs Bonjour portail Azure. 

Toutes les applications sont affectées de groupe de connecteurs tooa. Si vous ne créez des groupes, toutes vos applications sont affectées par groupe de tooa par défaut. Mais si vous organisez vos connecteurs en groupes, vous pouvez définir chaque toowork application avec un groupe de connecteurs spécifique. Dans ce cas, les connecteurs hello uniquement dans ce groupe servent application hello lors de la demande. Cette fonctionnalité s’avère utile si vos applications sont hébergées à des emplacements différents. Vous pouvez créer des groupes basés sur l’emplacement, afin que les applications sont toujours prises en charge par les connecteurs sont physiquement fermer toothem.

>[!TIP] 
>Si vous avez un grand déploiement de Proxy d’Application, n’affectez pas de n’importe quel groupe de connecteurs applications toohello par défaut. De cette façon, nouveaux connecteurs ne recevez pas tout le trafic dynamique jusqu'à ce que vous les affectez le groupe de connecteur active tooan. Cette configuration vous permet également connecteurs tooput en mode inactif en les déplaçant le groupe par défaut de toohello précédent, afin que vous pouvez effectuer la maintenance sans impact sur vos utilisateurs.

## <a name="prerequisites"></a>Composants requis
toogroup vos connecteurs, vous avez toomake que vous [plusieurs connecteurs installés](active-directory-application-proxy-enable.md). Lorsque vous installez un nouveau connecteur, il est automatiquement ajouté hello **par défaut** groupe de connecteurs.

## <a name="create-connector-groups"></a>Créer des groupes de connecteurs
Utilisez ces toocreate étapes autant de groupes de connecteurs que vous le souhaitez. 

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
1. Sélectionnez **Azure Active Directory** > **Applications d’entreprise** > **Proxy d’application**.
2. Sélectionnez **Nouveau groupe de connecteurs**. panneau du nouveau groupe de connecteurs Hello s’affiche.

   ![Sélectionner un nouveau groupe de connecteurs](./media/active-directory-application-proxy-connectors-azure-portal/new-group.png)

3. Donnez un nom à votre nouveau groupe de connecteur, puis utilisez hello dropdown menu tooselect connecteurs appartenant à ce groupe.
4. Sélectionnez **Enregistrer**.

## <a name="assign-applications-tooyour-connector-groups"></a>Affecter des groupes de connecteurs tooyour d’applications
Procédez comme suit pour chaque application que vous avez publiée avec le proxy d’application. Vous pouvez affecter un groupe de connecteurs tooa application lorsque vous la publiez tout d’abord, ou vous pouvez utiliser ces affectations de hello toochange suit quand vous le souhaitez.   

1. Tableau de bord de gestion hello pour votre annuaire, sélectionnez **des applications d’entreprise** > **toutes les applications** > hello application dans laquelle le groupe de connecteurs tooassign tooa >  **Le Proxy d’application**.
2. Hello d’utilisation **groupe de connecteurs** liste déroulante menu tooselect hello groupe hello toouse de l’application.
3. Sélectionnez **enregistrer** modification de hello tooapply.

## <a name="use-cases-for-connector-groups"></a>Cas d’utilisation des groupes de connecteurs 

Les groupes de connecteurs sont utiles dans divers scénarios, notamment les suivants :

### <a name="sites-with-multiple-interconnected-datacenters"></a>Sites contenant plusieurs centres de données interconnectés

De nombreuses organisations possèdent plusieurs centres de données interconnectés. Dans ce cas, vous souhaitez tookeep autant le trafic au sein du centre de données hello que possible, car les liens entre centres de données sont coûteux et lente. Vous pouvez déployer des connecteurs dans chaque centre de données tooserve seules hello les applications qui résident dans le centre de données hello. Cette approche réduit les liens entre centres de données et fournit une expérience entièrement transparente tooyour utilisateurs.

### <a name="applications-installed-on-isolated-networks"></a>Applications installées sur des réseaux isolés

Applications peuvent être hébergées dans des réseaux qui ne font pas partie du réseau d’entreprise de hello principal. Vous pouvez utiliser des connecteurs de tooinstall dédié de groupes de connecteur sur des réseaux isolés tooalso isoler toohello réseau d’applications. Cela se produit généralement lorsqu’un fournisseur tiers gère une application spécifique pour votre organisation. 

Groupes de connecteurs permettent de vous tooinstall dédié aux réseaux de publier des applications spécifiques uniquement, ce qui facilite les connecteurs et plus sécurisée des fournisseurs tiers toothird toooutsource la gestion des applications.

### <a name="applications-installed-on-iaas"></a>Applications installées sur IaaS 

Pour les applications installées sur IaaS pour l’accès au cloud, les groupes de connecteurs fournissent d’une applications de hello hello accès tooall service toosecure courantes. Groupes de connecteurs ne créer des dépendances supplémentaires sur votre réseau d’entreprise ou fragmenter l’expérience d’application hello. Les connecteurs peuvent être installés sur chaque centre de données du cloud et servir uniquement les applications qui se trouvent sur ce réseau. Vous pouvez installer plusieurs connecteurs tooachieve haut niveau de disponibilité.

Prenez comme exemple une organisation qui dispose de plusieurs ordinateurs virtuels connectés tootheir propre réseau virtuel IaaS hébergé. tooallow employés toouse ces applications, ces réseaux privés est connectés toohello réseau d’entreprise à l’aide de VPN de site à site. Les employés qui se trouvent sur site bénéficient ainsi d’une bonne expérience. Mais, peut-être pas idéal pour les employés distants, car elle nécessite tooroute accès à l’infrastructure locale supplémentaire, comme vous pouvez voir dans le diagramme hello ci-dessous :

![Réseau IaaS Azure AD](./media/application-proxy-publish-apps-separate-networks/application-proxy-iaas-network.png)
  
Avec les groupes de connecteurs de Proxy d’Application Azure AD, permettent à un common service toosecure hello accès tooall applications sans créer de dépendance supplémentaire sur votre réseau d’entreprise :

![Fournisseurs de cloud multiples IaaS Azure AD](./media/application-proxy-publish-apps-separate-networks/application-proxy-multiple-cloud-vendors.png)

### <a name="multi-forest--different-connector-groups-for-each-forest"></a>Forêts multiples : groupes de connecteurs différents pour chaque forêt

La plupart des clients qui ont déployé le proxy d’application utilisent ses fonctionnalités d’authentification unique (SSO) par le biais de la délégation Kerberos contrainte (KCD). tooachieve cela, machines besoin toobe tooa joint à un domaine du connecteur hello qui peut déléguer des utilisateurs de hello vers l’application hello. KCD prend en charge les fonctionnalités inter-forêts. Mais pour les entreprises qui disposent d’environnements distincts à plusieurs forêts sans approbation entre eux, il est impossible d’utiliser un connecteur unique pour toutes les forêts. 

Dans ce cas, des connecteurs spécifiques peuvent être déployées par forêt, et ensemble tooserve applications qui ont été publiée tooserve hello uniquement les utilisateurs de cette forêt spécifique. Chaque groupe de connecteurs représente une forêt différente. Alors que le client de hello et la plupart de l’expérience de hello est unifié pour toutes les forêts, les utilisateurs peuvent avoir tootheir applications de forêt à l’aide de groupes Azure AD.
 
### <a name="disaster-recovery-sites"></a>Sites de récupération d’urgence

Il existe deux approches différentes que vous pouvez utiliser avec un site de récupération d’urgence, en fonction de l’implémentation de vos sites :

* Si votre site de récupération d’urgence est créé en mode actif / actif dans lequel il est exactement comme site principal de hello et hello même mise en réseau et les paramètres Active Directory, vous pouvez créer des connecteurs de hello sur le site de récupération d’urgence de hello Bonjour même groupe de connecteurs en tant que site principal de hello. Ainsi, les basculements toodetect Azure AD pour vous.
* Si votre site de récupération d’urgence est distinct de site principal de hello, vous pouvez créer un groupe de connecteur différent dans le site de récupération d’urgence de hello et 1) sont soit des applications de sauvegarde ou (2) manuellement détournent groupe de connecteurs hello existant application toohello récupération d’urgence en fonction des besoins.
 
### <a name="serve-multiple-companies-from-a-single-tenant"></a>Traiter plusieurs entreprises à partir d’un seul client

Il existe différentes façons services pour plusieurs sociétés associés à tooimplement un modèle dans lequel un fournisseur de services unique déploie et gère de Azure AD. Groupes de connecteurs aident hello admin scinder les connecteurs hello et des applications dans différents groupes. Toohave n’est unidirectionnelle, ce qui n’est appropriée pour les petites entreprises, un seul locataire Azure AD pendant hello différentes sociétés ont leur propre nom de domaine et les réseaux. Cela vaut également pour les scénarios et les situations M&A où une division informatique unique sert plusieurs entreprises pour des raisons réglementaires ou professionnelles. 

## <a name="sample-configurations"></a>Exemples de configurations

Que vous pouvez implémenter, exemples hello suivant des groupes de connecteurs.
 
### <a name="default-configuration--no-use-for-connector-groups"></a>Configuration par défaut : inutile pour les groupes de connecteurs

Si vous n’utilisez pas les groupes de connecteurs, votre configuration ressemblerait à ceci :

![AzureAD Aucun groupe de connecteurs](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-1.png)
 
Cette configuration est suffisante pour les tests et les petits déploiements. Elle est également adaptée si votre organisation dispose d’une topologie de réseau à plat.
 
### <a name="default-configuration-and-an-isolated-network"></a>Configuration par défaut et réseau isolé

Cette configuration est une évolution du hello par défaut, dans lequel il existe une application spécifique qui s’exécute dans un réseau isolé, telles que les réseaux virtuels IaaS : 

![AzureAD Aucun groupe de connecteurs](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-2.png)
 
### <a name="recommended-configuration--several-specific-groups-and-a-default-group-for-idle"></a>Configuration recommandée : plusieurs groupes spécifiques et un groupe par défaut inactif

Hello configuration recommandée pour les organisations important et complexes est groupe de connecteurs toohave hello par défaut en tant que groupe qui ne servent pas toutes les applications et est utilisé pour les connecteurs inactifs ou nouvellement installés. Toutes les applications sont traitées à l’aide de groupes de connecteurs personnalisés. Cela permet à toute la complexité hello de scénarios hello décrits ci-dessus.

Dans l’exemple hello ci-dessous, la société de hello a deux centres de données, A et B, avec deux connecteurs qui font Office de chaque site. Des applications différentes s’exécutent sur chaque site. 

![AzureAD Aucun groupe de connecteurs](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-3.png)
 
## <a name="next-steps"></a>Étapes suivantes

* [Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md)
* [Activer l’authentification unique](application-proxy-sso-overview.md)


