---
title: "connecteurs de Proxy d’application Azure AD portails aaaClassic | Documents Microsoft"
description: "Aborde comment toocreate et gérer des groupes de connecteurs de Proxy d’Application Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b283796a-9679-4c79-b703-802bb850f65d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 43559b0f4ffc3c7dbbf00901e89ac276d01796e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>Publier des applications sur des réseaux et emplacements distincts à l’aide de groupes de connecteurs
> [!div class="op_single_selector"]
> * [Portail Azure](active-directory-application-proxy-connectors-azure-portal.md)
> * [Portail Azure Classic](active-directory-application-proxy-connectors.md)
>
>

Les groupes de connecteurs sont utiles dans divers scénarios, notamment les suivants :

* Sites contenant plusieurs centres de données interconnectés. Dans ce cas, vous souhaitez tookeep autant le trafic au sein du centre de données hello que possible, car les liens entre centres de données sont coûteux et lente. Vous pouvez déployer des connecteurs dans chaque centre de données tooserve seules hello les applications qui résident dans le centre de données hello. Cette approche réduit les liens entre centres de données et fournit une expérience entièrement transparente tooyour utilisateurs.
* La gestion des applications installées sur des réseaux isolés qui ne font pas partie du réseau d’entreprise de hello principal. Vous pouvez utiliser des connecteurs de tooinstall dédié de groupes de connecteur sur des réseaux isolés tooalso isoler toohello réseau d’applications.
* Pour les applications installées sur IaaS pour l’accès au cloud, les groupes de connecteurs fournissent d’une applications de hello hello accès tooall service toosecure courantes. Groupes de connecteurs ne créer des dépendances supplémentaires sur votre réseau d’entreprise ou fragmenter l’expérience d’application hello. Les connecteurs peuvent être installés sur chaque centre de données du cloud et servir uniquement les applications qui se trouvent sur ce réseau. Vous pouvez installer plusieurs connecteurs tooachieve haut niveau de disponibilité.
* Prise en charge des environnements à plusieurs forêts dans lesquelles des connecteurs spécifiques peuvent être déployées par forêt et définir tooserve des applications spécifiques.
* Groupes de connecteur peuvent être utilisés dans les sites de récupération d’urgence tooeither détecter le basculement ou en tant que sauvegarde pour hello principal site.
* Groupes de connecteurs peuvent également être utilisé tooserve plusieurs sociétés à partir d’un seul client.

## <a name="prerequisite-create-your-connectors"></a>Condition préalable : créez vos connecteurs
toogroup vos connecteurs, [installer plusieurs connecteurs](active-directory-application-proxy-enable.md), puis attribuez un nom et de les regrouper. Enfin, vous avez tooassign les applications de toospecific.

## <a name="step-1-create-connector-groups"></a>Étape 1 : créer des groupes de connecteurs
Vous pouvez créer autant de groupes de connecteurs que vous le souhaitez. Création d’un groupe connecteur s’effectue en hello portail Azure classic.

1. Sélectionnez votre annuaire, puis cliquez sur **Configurer**.  
    ![Capture d’écran de la configuration du proxy d’application - cliquez sur Gérer les groupes de connecteurs](./media/active-directory-application-proxy-connectors/app_proxy_connectors_creategroup.png)
2. Proxy d’Application, cliquez sur **gérer les groupes de connecteurs** et créer un groupe de connecteurs en nommant les groupe hello.  
    ![Capture d’écran de groupes de connecteurs du proxy d’application - nommez le nouveau groupe](./media/active-directory-application-proxy-connectors/app_proxy_connectors_namegroup.png)

## <a name="step-2-assign-connectors-tooyour-groups"></a>Étape 2 : Affecter des connecteurs tooyour
Une fois créés, les groupes de connecteurs hello déplacer le groupe approprié du toohello connecteurs hello.

1. Sous **Proxy d’application**, cliquez sur **Gérer les connecteurs**.
2. Sous **groupe**, sélectionnez groupe hello pour chaque connecteur. Il peut prendre connecteurs hello des too10 minutes toobecome active dans le nouveau groupe de hello.  
    ![Capture d’écran de connecteurs du proxy d’application - sélectionnez un groupe dans le menu déroulant](./media/active-directory-application-proxy-connectors/app_proxy_connectors_connectorlist.png)

## <a name="step-3-assign-applications-tooyour-connector-groups"></a>Étape 3 : Affecter des groupes de connecteurs tooyour d’applications
dernière étape de Hello est tooset chaque groupe de connecteurs toohello application qui l’héberge.

1. Bonjour portail Azure classic, dans votre annuaire, sélectionnez hello Application tooassign toohello groupe et cliquez sur **configurer**.
2. Sous **groupe de connecteurs**, sélectionnez hello groupe hello toouse de l’application. Cette modification est appliquée immédiatement.  
    ![Capture d’écran de groupe de connecteurs du proxy d’application - sélectionnez un groupe dans le menu déroulant](./media/active-directory-application-proxy-connectors/app_proxy_connectors_newgroup.png)

## <a name="see-also"></a>Voir aussi
* [Activer le proxy d’application](active-directory-application-proxy-enable.md)
* [Activer l’authentification unique](active-directory-application-proxy-sso-using-kcd.md)
* [Activer l’accès conditionnel](active-directory-application-proxy-conditional-access.md)
* [Résoudre les problèmes rencontrés avec le proxy d’application](active-directory-application-proxy-troubleshoot.md)

Pour les informations les plus récentes hello et mises à jour, consultez hello [blog de Proxy d’Application](http://blogs.technet.com/b/applicationproxyblog/)
