---
title: "aaaConnect tooan local système SAP dans Azure Logic Apps | Documents Microsoft"
description: "Se connecter de système SAP tooan local à partir de votre flux de travail application logique via la passerelle de données locale hello"
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a>Se connecter de système SAP tooan local à partir de la logique d’applications avec le connecteur SAP hello 

passerelle de données locale Hello vous permet de toomanage données et accéder en toute sécurité les ressources locales. Cette rubrique montre comment vous pouvez connecter le système SAP local logique applications tooan. Dans cet exemple, votre application logique demande un IDOC via HTTP et envoie la réponse hello.    

> [!NOTE]
> Limitations actuelles : 
> - Votre application logique expire si toutes les étapes nécessaires pour la réponse de hello ne se terminent dans hello [limite de délai d’attente de demandes](./logic-apps-limits-and-config.md). Dans ce scénario, les demandes peuvent être bloquées. 
> - Sélecteur de fichier Hello n’affiche pas tous les champs disponibles hello. Dans ce scénario, vous pouvez ajouter manuellement des chemins d’accès.

## <a name="prerequisites"></a>Composants requis

- Installer et configurer hello dernières [passerelle de données locale](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 ou une version ultérieure. [Comment tooconnect toohello local passerelle de données dans une application logique](http://aka.ms/logicapps-gateway) listes hello étapes. passerelle de Hello doit être installé sur un ordinateur local avant de pouvoir continuer.

- Téléchargement et installation hello dernière SAP bibliothèque cliente sur hello même de l’ordinateur où vous avez installé la passerelle de données hello. Utiliser les hello SAP versions suivantes : 
    - Serveur SAP
        - N’importe quel serveur SAP que hello prise en charge le connecteur .NET (NCo) 3.0
 
    - Client SAP
        - Connecteur SAP .NET (NCo) 3.0

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a>Ajouter des déclencheurs et les actions pour la connexion de système de tooyour SAP

le connecteur SAP Hello possède des actions, mais pas les déclencheurs. Par conséquent, nous avons toouse un autre déclencheur au début de hello du flux de travail hello. 

1. Ajouter le déclencheur de demande/réponse hello et sélectionnez **nouvelle étape**.

2. Sélectionnez **ajouter une action**, puis sélectionnez le connecteur SAP hello en tapant `SAP` dans le champ de recherche hello :    

     ![Sélectionnez le serveur d’applications SAP ou le serveur de messagerie SAP.](media/logic-apps-using-sap-connector/sap-action.png)

3. Sélectionnez [**Serveur d’applications SAP**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) ou [**Serveur de messagerie SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), selon votre installation SAP. Si vous n’avez pas une connexion existante, vous êtes invité à toocreate une.

   1. Sélectionnez **se connecter via la passerelle de données locale**et entrez les détails de hello pour votre système SAP :   

       ![Ajouter tooSAP de chaîne de connexion](media/logic-apps-using-sap-connector/picture2.png)  

   2. Sous **passerelle**, sélectionnez une passerelle existante, ou tooinstall une passerelle, sélectionnez **installer une passerelle**.

        ![Installer une nouvelle passerelle](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. Après avoir entré tous les détails de hello, sélectionnez **créer**. 
   Logique d’applications configure et teste la connexion hello, s’assurer que les connexions hello fonctionnement correctement.

4. Entrez un nom pour votre connexion SAP.

5. différentes options de SAP Hello sont désormais disponibles. toofind catégorie IDOC, sélectionnez à partir de la liste de hello. Ou tapez manuellement dans le chemin d’accès hello et réponse hello sélectionnez HTTP dans hello **corps** champ :

     ![Action SAP](media/logic-apps-using-sap-connector/picture3.png)

6. Ajouter une action hello pour la création d’un **réponse HTTP**. message de réponse Hello doit provenir de la sortie SAP hello.

7. Enregistrez votre application logique. Testez-le en envoyant un IDOC via l’URL du déclencheur hello HTTP. Après hello QU'IDOC est envoyé, attendez réponse hello à partir de l’application logique de hello :   

     > [!TIP]
     > Découvrez comment faire trop[surveiller vos applications logiques](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Maintenant que le connecteur SAP hello est ajouté l’application logique de tooyour, commencer à Explorer les autres fonctionnalités :

- BAPI
- RFC

## <a name="get-help"></a>Obtenir de l’aide

tooask questions, répondre aux questions et savoir quels autres Azure Logic Apps font les utilisateurs, visitez hello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp améliorer Azure Logic Apps et connecteurs, voter pour ou envoyer vos idées à hello [site de commentaires utilisateur Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Étapes suivantes

- Découvrez comment toovalidate, transformation et autres fonctions de BizTalk de type Bonjour [Pack d’intégration Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md). 
- [Se connecter aux données local tooon](../logic-apps/logic-apps-gateway-connection.md) à partir d’applications de logique
