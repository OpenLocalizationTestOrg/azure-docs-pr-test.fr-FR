---
title: "sources de données aaaAccess localement pour Azure Logic Apps | Documents Microsoft"
description: "Configurer la passerelle de données locale hello pour pouvoir accéder à des sources de données sur site à partir d’applications de logique"
keywords: "accéder aux données, localement, transfert de données, chiffrement, sources de données"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a>Accès aux sources de données sur site à partir de la logique d’applications avec la passerelle de données locale hello

tooaccess des sources de données sur site à partir de vos applications logiques, configurez une passerelle de données local qui logique applications peuvent utiliser avec les connecteurs pris en charge. Hello passerelle fait Office de pont qui fournit le transfert de données rapide et le chiffrement entre les sources de données sur site et vos applications logiques. passerelle de Hello transmet des données à partir de sources locales sur des canaux chiffrés via hello Azure Service Bus. Tout le trafic provient sécurisé trafic sortant à partir de l’agent de passerelle hello. En savoir plus sur [le fonctionnement de la passerelle de données hello](logic-apps-gateway-install.md#gateway-cloud-service). 

passerelle de Hello prend en charge les sources de données de connexions toothese sur site :

*   BizTalk Server 2016
*   DB2  
*   Système de fichiers
*   Informix
*   MQ
*   MySQL
*   Oracle Database
*   PostgreSQL
*   Serveur d’applications SAP 
*   Serveur de messagerie SAP
*   SharePoint
*   SQL Server
*   Teradata

Ces étapes indiquent comment tooset des hello local toowork de passerelle de données avec vos applications logiques. Pour plus d’informations sur les connecteurs pris en charge, voir [Connecteurs pour Azure Logic Apps](../connectors/apis-list.md). 

Pour plus d’informations sur la façon dont toouse hello passerelle avec d’autres services, consultez les articles suivants :

*   [Passerelle de données locale Microsoft Power BI](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Passerelle de données locale Azure Analysis Services](../analysis-services/analysis-services-gateway.md)
*   [Passerelle de données locale Microsoft Flow](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Passerelle de données locale Microsoft PowerApps](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a>Configuration requise

* Vous devez d’abord [installé la passerelle de données hello sur un ordinateur local](logic-apps-gateway-install.md).

* Lorsque vous vous connectez dans toohello portail Azure, vous avez toouse hello même travail ou d’établissement scolaire compte qui a été utilisé trop[installer la passerelle de données locale hello](logic-apps-gateway-install.md#requirements). Votre compte de connexion doit également avoir un toouse abonnement Azure lorsque vous créez une ressource de la passerelle Bonjour portail Azure pour votre installation de la passerelle.

* L’installation de votre passerelle ne peut pas être revendiquée par une autre ressource de passerelle Azure. Vous pouvez associer votre passerelle installation tooonly une passerelle Azure ressource. Revendication se produit lorsque vous créez une ressource de la passerelle hello afin que l’installation de hello n’est pas disponible pour d’autres ressources.

## <a name="set-up-hello-data-gateway-connection"></a>Configurer la connexion de passerelle de données hello

### <a name="1-install-hello-on-premises-data-gateway"></a>1. Installer la passerelle de données locale hello

Si vous n’avez pas encore, suivez hello [passerelle de données locale étapes tooinstall hello](logic-apps-gateway-install.md). Avant de continuer avec hello autres étapes, assurez-vous que vous avez installé la passerelle de données hello sur un ordinateur local.

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a>2. Créer une ressource Azure pour la passerelle de données locale hello

Après avoir installé la passerelle de hello sur un ordinateur local, vous devez créer votre passerelle de données en tant que ressource dans Azure. Cette étape associe également votre ressource de passerelle à votre abonnement Azure.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com "portail Azure"). Assurez-vous que toouse hello même travail Azure ou l’adresse de messagerie de l’école utilisée passerelle de hello tooinstall.

2. Dans le menu de gauche hello dans Azure, choisissez **nouveau** > **intégration** > **passerelle de données locale** comme indiqué ici :

   ![Cherchez « Passerelle de données locale »](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. Sur hello **créer une passerelle connexion** panneau, fournissez ces toocreate détails votre ressource de passerelle de données :

    * **Nom** : entrez un nom pour votre ressource de passerelle. 

    * **Abonnement**: sélectionnez hello tooassociate abonnement Azure avec votre ressource de la passerelle. 
    Cet abonnement doit être hello même abonnement que votre application logique.
   
      abonnement de Hello par défaut est basée sur hello compte Azure que vous avez utilisé toosign dans.

    * **Groupe de ressources** : créez un groupe de ressources ou sélectionnez un groupe de ressources existant pour le déploiement de votre ressource de passerelle. 
    Les groupes de ressources vous aident à gérer des ressources Azure associées en tant que collection.

    * **Emplacement**: Azure limite ce toohello emplacement même région a été sélectionnée pour le service de cloud de passerelle hello pendant [installation de la passerelle](logic-apps-gateway-install.md). 

      > [!NOTE]
      > Assurez-vous que l’emplacement de ressource hello passerelle correspond à l’emplacement de service cloud hello passerelle. Dans le cas contraire, votre installation de passerelle peuvent ne pas apparaît dans la liste des passerelles hello installé pour vous tooselect à l’étape suivante de hello.
      > 
      > Vous pouvez utiliser des régions différentes pour votre ressource de passerelle et votre application logique.

    * **Nom de l’installation**: Si votre installation de la passerelle n’est pas déjà sélectionnée, sélectionnez passerelle hello que vous avez installé précédemment. 

    tooadd hello passerelle ressource tooyour tableau de bord Azure, choisissez **toodashboard du code confidentiel**. 
    Lorsque vous êtes prêt, choisissez **Créer**.

    Par exemple :

    ![Fournir des détails toocreate votre passerelle de données locale](./media/logic-apps-gateway-connection/createblade.png)

    toofind ou afficher votre passerelle de données à tout moment, depuis hello Azure gauche menu principal, accédez trop **plus Services** > **intégration** > **des données locales Passerelles**.

    ![Accédez trop « Plus services », « Intégration d’entreprise », « Passerelles de données locales »](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a>3. Connecter votre passerelle de données logique application toohello local

Maintenant que vous avez créé votre ressource de passerelle de données et votre abonnement Azure associé à cette ressource, créez une connexion entre votre passerelle de données logique app et hello.

> [!NOTE]
> L’emplacement de votre connexion de passerelle doit exister dans hello même région que votre application logique, mais vous pouvez utiliser une passerelle de données qui existe dans une autre région.

1. Bonjour portail Azure, créez ou ouvrez votre application de logique dans le Concepteur de la logique d’application.

2. Ajoutez un connecteur prenant en charge des connexions locales, tel que SQL Server.

3. Ordre de hello indiqué, sélectionnez **se connecter via la passerelle de données locale**, fournissez un nom de connexion unique hello les informations requises et sélectionnez les ressources de passerelle de données hello que vous souhaitez toouse. Lorsque vous êtes prêt, choisissez **Créer**.

   > [!TIP]
   > Un nom de connexion unique vous aidera à identifier facilement cette connexion ultérieurement, en particulier si vous créez plusieurs connexions. Le cas échéant, également inclure hello de domaine complet pour votre nom d’utilisateur. 

   ![Créer une connexion entre une application logique et une passerelle de données](./media/logic-apps-gateway-connection/blankconnection.png)

Félicitations, votre connexion de passerelle est maintenant prête pour votre toouse d’application logique.

## <a name="edit-your-gateway-connection-settings"></a>Modifier vos paramètres de connexion de passerelle

Après avoir créé une connexion de passerelle pour votre application logique, vous pouvez choisir les paramètres de hello toolater mise à jour pour cette connexion spécifique.

1. connexion à la passerelle toofind hello :

   * Dans le panneau de l’application hello logique, sous **outils de développement**, sélectionnez **API connexions**. 
   
     Hello **API connexions** volet affiche toutes les connexions d’API associées à votre application logique, y compris les connexions de la passerelle.

     ![Accédez à tooyour logique application, sélectionnez « Connexions API »](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * Ou, à partir de hello Azure gauche menu principal, accédez trop **plus Services** > **Web et les Services mobiles** > **API connexions** pour toutes les connexions d’API, y compris les connexions de la passerelle, qui sont associés à votre abonnement Azure. 

   * Ou, sur hello Azure gauche menu principal, accédez trop**toutes les ressources** pour toutes les connexions d’API, y compris les connexions de la passerelle, qui sont associées à votre abonnement Azure.

2. Sélectionnez la connexion à la passerelle hello que vous tooview ou modifier, puis cliquez **connexion modifier l’API**.

   > [!TIP]
   > Si vos mises à jour n’entrent en vigueur, essayez de [arrêter et redémarrer le service Windows de passerelle hello](./logic-apps-gateway-install.md#restart-gateway).

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a>Basculer ou supprimer votre ressource de passerelle de données locale

toocreate une ressource passerelle différents, associer votre passerelle avec une autre ressource, ou supprimez la ressource de la passerelle hello, vous pouvez supprimer des ressources de passerelle hello sans affecter l’installation de la passerelle hello. 

1. À partir de hello Azure gauche menu principal, accédez trop**toutes les ressources**. 
2. Cherchez et sélectionnez votre ressource de passerelle de données.
3. Choisissez **passerelle de données locale**, dans la barre d’outils de la ressource hello, choisissez **supprimer**.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Forum Aux Questions

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a>Étapes suivantes

* [Sécuriser vos applications logiques](./logic-apps-securing-a-logic-app.md)
* [Exemples et scénarios courants pour les applications logiques](./logic-apps-examples-and-scenarios.md)
