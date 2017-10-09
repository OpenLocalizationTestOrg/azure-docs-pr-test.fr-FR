---
title: "systèmes à partir d’Azure Logic Apps du fichier local tooon aaaConnect | Documents Microsoft"
description: "Connecter des systèmes de fichiers local tooon à partir de votre flux de travail application logique via la passerelle de données locale hello et le connecteur du système de fichiers"
keywords: "systèmes de fichiers"
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a>Connecter des systèmes de fichiers local tooon à partir de la logique des applications avec le connecteur de système de fichiers hello

Connectivité de cloud hybride est applications toologic central, c’est le cas toomanage données et en toute sécurité accès aux ressources locales, vos applications logiques peuvent utiliser passerelle de données locale hello. Dans cet article, nous montrons comment tooconnect tooan local système de fichiers avec un scénario de base : copier un fichier de tooDropbox téléchargé tooa partage de fichiers, puis envoyer un courrier électronique.

## <a name="prerequisites"></a>Composants requis

- Installer et configurer hello dernières [passerelle de données locale](https://www.microsoft.com/download/details.aspx?id=53127).
- Installer la passerelle de données de local dernière hello, version 1.15.6150.1 ou version ultérieure. [Se connecter à la passerelle de données locale toohello](http://aka.ms/logicapps-gateway) listes hello étapes. passerelle de Hello doit être installé sur un ordinateur local avant de pouvoir continuer avec hello étapes restantes de hello.

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a>Ajouter le déclencheur et les actions pour la connexion de système de fichiers tooyour

1. Créez une application logique et ajoutez ce déclencheur Dropbox : **Lorsqu’un fichier est créé**. 
2. Sous le déclencheur de hello, choisissez **étape suivante** > **ajouter une action**. 
3. Dans la zone de recherche de hello, entrez `file system` afin de pouvoir consulter les actions toutes prises en charge pour le connecteur du système de fichiers hello.

   ![Rechercher le connecteur de fichiers](media/logic-apps-using-file-connector/search-file-connector.png)

2. Choisissez hello **créer un fichier** action et créer un système de fichiers de connexion tooyour.

   Si vous n’avez pas une connexion existante, vous êtes invité à toocreate une.

   1. Choisissez **Se connecter via la passerelle de données locale**. D’autres propriétés s’affichent.
   2. Sélectionnez le dossier racine de votre système de fichiers.
      
       > [!NOTE]
       > Hello dossier racine est hello parent principal, qui est utilisé pour les chemins d’accès relatifs pour toutes les actions liées aux fichiers. Vous pouvez spécifier un dossier local sur l’ordinateur hello où passerelle de données locale hello est installée ou dossier de hello peut être un partage réseau qui hello ordinateur peut accéder.

   3. Entrez hello username et password pour la passerelle de hello.
   4. Sélectionnez hello passerelle que vous avez installé précédemment.

       ![Configurer la connexion](media/logic-apps-using-file-connector/create-file.png)

3. Après avoir fourni tous les détails de hello, choisissez **créer**. 

   Logique d’applications configure et teste votre connexion, en veillant à ce que les connexions hello fonctionnement correctement. 
   Si la connexion de hello est correctement configuré, vous voyez des options pour l’action hello que vous avez sélectionné précédemment. 
   connecteur de système de fichiers Hello est maintenant prêt à être utilisé.

4. Spécifier que vous souhaitez toocopy les fichiers du dossier racine de toohello Dropbox pour le partage de fichiers local.

   ![Créer une action de fichier](media/logic-apps-using-file-connector/create-file-filled.png)

5. Une fois le fichier logique application copies hello, ajoutez une action d’Outlook qui envoie un message électronique afin que les utilisateurs concernés sachent sur le nouveau fichier de hello. Entrez les destinataires hello, titre et le corps des messages électroniques de hello. 

   Dans le sélecteur de contenu dynamique hello, vous pouvez choisir les sorties de données à partir du connecteur de fichier hello afin de pouvoir ajouter par courrier électronique des toohello plus de détails.

   ![Envoyer l’action de messagerie](media/logic-apps-using-file-connector/send-email.png)

6. Enregistrez votre application logique. Testez votre application en chargeant un fichier tooDropbox. fichier de Hello doit obtenir le partage de fichiers copiés toohello local, et vous devez recevoir un message électronique à propos de l’opération de hello.

   > [!TIP] 
   > Découvrez comment trop[surveiller vos applications logiques](../logic-apps/logic-apps-monitor-your-logic-apps.md).

Félicitations, vous avez maintenant une application logique qui peut se connecter de système de fichiers local tooyour. Essayez d’Explorer les autres fonctionnalités hello offres du connecteur, par exemple :

- Créer un fichier
- Répertorier les fichiers dans un dossier
- Ajouter un fichier
- Supprimer un fichier
- Obtenir le contenu d’un fichier
- Obtenir le contenu d’un fichier à l’aide du chemin
- Obtenir les métadonnées d’un fichier
- Obtenir les métadonnées d’un fichier à l’aide du chemin
- Répertorier les fichiers dans le dossier racine
- Mettre à jour un fichier

## <a name="view-hello-swagger"></a>Swagger hello de vue
Consultez hello [swagger détails](/connectors/fileconnector/). 

## <a name="get-help"></a>Obtenir de l’aide

tooask questions, répondre aux questions et savoir quels autres Azure Logic Apps font les utilisateurs, visitez hello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp améliorer Azure Logic Apps et connecteurs, voter pour ou envoyer vos idées à hello [site de commentaires utilisateur Azure Logic Apps](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Étapes suivantes

- [Se connecter aux données local tooon](../logic-apps/logic-apps-gateway-connection.md) à partir d’applications de logique
- En savoir plus sur [l’intégration d’entreprise](../logic-apps/logic-apps-enterprise-integration-overview.md)
