---
title: "certificats aaaUsing avec le Pack d’intégration Enterprise | Documents Microsoft"
description: "En savoir plus l’utilisation des certificats avec hello Pack d’intégration Enterprise toouse | Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: cgronlun
ms.assetid: 4cbffd85-fe8d-4dde-aa5b-24108a7caa7d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 7ba9f597a03a852a9ba05d2af08fe4bc2d98aef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-certificates-and-enterprise-integration-pack"></a>En savoir plus sur les certificats et Enterprise Integration Pack
## <a name="overview"></a>Vue d'ensemble
Intégration d’entreprise utilise les communications de certificats toosecure B2B. Vous pouvez utiliser deux types de certificats dans vos applications Enterprise Integration :

* Des certificats publics, qui doivent être achetés auprès d’une autorité de certification (CA).
* Des certificats privés, que vous pouvez créer vous-même. Ces certificats sont parfois tooas auxquels les certificats auto-signés.

## <a name="what-are-certificates"></a>Que sont les certificats ?
Les certificats sont des documents numériques qui vérifient l’identité hello de participants hello dans les communications électroniques et qui également sécuriser les communications électroniques.

## <a name="why-use-certificates"></a>Pourquoi utiliser des certificats ?
Parfois, les communications B2B doivent rester confidentielles. Intégration d’entreprise utilise des certificats toosecure ces communications de deux manières :

* En chiffrant contenu hello des messages
* En signant numériquement les messages  

## <a name="upload-a-public-certificate"></a>Téléchargement d’un certificat public

toouse un *certificat public* dans vos applications logiques avec les fonctionnalités B2B, vous devez tout d’abord certificat de hello tooupload à votre compte d’intégration.  

Après avoir téléchargé un certificat, il est disponible toohelp vous sécuriser vos messages B2B lorsque vous définissez leurs propriétés Bonjour [accords](logic-apps-enterprise-integration-agreements.md) que vous créez.  

Voici hello des instructions détaillées sur le téléchargement de vos certificats publics dans votre compte d’intégration après vous être connecté toohello portail Azure :

1. Sélectionnez **davantage de services** et entrez **intégration** dans la zone de recherche filtre hello. Sélectionnez **comptes d’intégration** à partir de la liste des résultats hello     
![Sélectionnez Parcourir](media/logic-apps-enterprise-integration-certificates/overview-1.png)  
2. Sélectionnez hello intégration compte toowhich tooadd hello certificat.  
![Sélectionnez hello intégration compte toowhich tooadd hello certificat](media/logic-apps-enterprise-integration-certificates/overview-3.png)  
3. Sélectionnez hello **certificats** vignette.  
![Sélectionnez hello certificats vignette](media/logic-apps-enterprise-integration-certificates/certificate-1.png)
4. Bonjour **certificats** panneau s’ouvre, sélectionnez hello **ajouter** bouton.   
![Sélectionnez le bouton Ajouter de hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
5. Entrez un **nom** pour votre certificat et le type de certificat puis hello en tant que **public** à partir de la liste déroulante de hello.  
6. Icône de dossier hello SELECT sur le côté droit de hello Hello **certificat** zone de texte. Lorsque le sélecteur de fichier hello s’ouvre, recherchez et sélectionnez hello fichier de certificat que vous souhaitez le compte d’intégration tooupload tooyour.
7. Sélectionnez le certificat de hello, puis **OK** dans le sélecteur de fichier hello. Cela valide et télécharge le compte d’intégration tooyour hello certificat.
8. Enfin, de retour sur hello **ajouter un certificat** panneau, sélectionnez hello **OK** bouton.  
![Sélectionnez le bouton OK de hello](media/logic-apps-enterprise-integration-certificates/certificate-3.png)  
9. Sélectionnez hello **certificats** vignette. Vous devez voir hello certificat a été ajouté récemment.  
![Consultez le nouveau certificat de hello](media/logic-apps-enterprise-integration-certificates/certificate-4.png)  

## <a name="upload-a-private-certificate"></a>Téléchargement d’un certificat privé

toouse un *certificat privé* dans vos applications logiques avec les fonctionnalités B2B, vous pouvez télécharger un compte d’intégration tooyour certificat privé à hello en prenant comme suit

1. [Télécharger votre tooKey de clé privée coffre](../key-vault/key-vault-get-started.md "en savoir plus sur le coffre de clés") et fournir un **nom de la clé** 
   
   > [!TIP]
   > Vous devez autoriser les opérations de tooperform Logic Apps sur le coffre de clés. Vous pouvez accorder principal du service accès toohello Logic Apps à l’aide de hello suivant de commande PowerShell :`Set-AzureRmKeyVaultAccessPolicy -VaultName 'TestcertKeyVault' -ServicePrincipalName '7cd684f4-8a78-49b0-91ec-6a35d38739ba' -PermissionsToKeys decrypt, sign, get, list`  
   > 
   > 

Une fois que vous avez effectuées précédemment hello, ajoutez un compte de toointegration de certificat privé.

Suivantes sont hello des instructions détaillées sur le téléchargement de vos certificats privés dans votre compte d’intégration après que vous être connecté toohello portail Azure :  
 
1. Sélectionnez hello intégration compte toowhich vous tooadd hello certificat et sélectionnez hello **certificats** vignette.  
![Sélectionnez hello certificats vignette](media/logic-apps-enterprise-integration-certificates/certificate-1.png)  
2. Bonjour **certificats** panneau s’ouvre, sélectionnez hello **ajouter** bouton.   
![Sélectionnez le bouton Ajouter de hello](media/logic-apps-enterprise-integration-certificates/certificate-2.png)
3. Entrez un **nom** pour votre certificat et le type de certificat hello sélectionnez en tant que **privé** à partir de la liste déroulante de hello.   
4. Sélectionnez l’icône de dossier hello sur le côté droit de hello Hello **certificat** zone de texte. Lorsque le sélecteur de fichier hello s’ouvre, trouver le certificat public correspondant hello compte d’intégration tooupload tooyour.   
   
   > [!Note]
   > Lors de l’ajout d’un certificat privé, il est important de tooadd correspondant publique du certificat tooshow dans [accord AS2](logic-apps-enterprise-integration-as2.md) recevoir et envoyer des paramètres pour signer et chiffrer les messages de type hello.
   > 
   >   

5. Sélectionnez hello **groupe de ressources**, **le coffre de clés**, **nom de la clé** et sélectionnez hello **OK** bouton.  
![Ajouter le certificat](media/logic-apps-enterprise-integration-certificates/privatecertificate-1.png)  
6. Sélectionnez hello **certificats** vignette. Vous devez voir hello certificat a été ajouté récemment.
![Consultez le nouveau certificat de hello](media/logic-apps-enterprise-integration-certificates/privatecertificate-2.png)  



* [Créer un contrat B2B](logic-apps-enterprise-integration-agreements.md)  
* [En savoir plus sur Azure Key Vault](../key-vault/key-vault-get-started.md "En savoir plus sur le coffre de clés")  

