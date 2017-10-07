---
title: "aaaEncode ou décoder les fichiers plats dans les applications Azure logique | Documents Microsoft"
description: "Comment toouse hello encodeur de fichier de fichier ou un décodeur Bonjour Pack d’intégration Enterprise dans vos applications logiques"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 82152dab-c7ad-43df-b721-596559703be8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; mandia
ms.openlocfilehash: 2c295586625fd84366ec7cbafdcebf0489ba234d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-enterprise-integration-with-flat-files"></a>Vue d’ensemble de l’intégration d’entreprise avec des fichiers plats

Vous souhaiterez tooencode XML contenu avant de l’envoyer partenaire tooa dans un scénario d’entreprise-entreprise (B2B). Dans une application logique, vous pouvez utiliser les fichiers plats hello encodage connecteur toodo cela. Hello application logique que vous créez peut obtenir sa XML contenu à partir de diverses sources, y compris à partir d’un déclencheur de la demande HTTP, à partir d’une autre application ou même à partir d’un des hello plusieurs [connecteurs](../connectors/apis-list.md). Pour plus d’informations sur les applications de la logique, consultez hello [documentation des applications logique](logic-apps-what-are-logic-apps.md "en savoir plus sur les applications de la logique").  

## <a name="create-hello-flat-file-encoding-connector"></a>Créer le connecteur de codage de fichier plat hello
Suivez ces étapes tooadd un connecteur tooyour logique application l’encodage de fichier plat.

1. Créer une application de la logique et [lier le compte d’intégration tooyour](logic-apps-enterprise-integration-accounts.md "savoir toolink une application de la logique de l’intégration compte tooa"). Ce compte contient un schéma hello vous utiliserez tooencode hello données XML.  
2. Ajouter un **demande - HTTP lors de la demande est reçue** application logique de tooyour déclencheur.  
   ![Capture d’écran de déclencheur tooselect](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
3. Ajoutez les fichiers plats hello encodage action, comme suit :
   
    a. Sélectionnez hello **plus** signe.
   
    b. Sélectionnez hello **ajouter une action** lien (s’affiche lorsque vous avez sélectionné le signe plus hello).
   
    c. Dans la zone de recherche de hello, entrez *plat* toofilter tous hello toohello actions une que vous souhaitez toouse.
   
    d. Sélectionnez hello **le codage de fichier plat** option de liste de hello.   
   ![Capture d’écran de l’option Encodage du fichier plat](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
4. Sur hello **le codage de fichier plat** boîte de dialogue, sélectionnez hello **contenu** zone de texte.  
   ![Capture d’écran de la zone de texte Contenu](media/logic-apps-enterprise-integration-flatfile/flatfile-3.png)  
5. Sélectionnez body est dupliquée hello hello contenu que vous souhaitez tooencode. balise body de Hello remplit les champs contenu hello.     
   ![Capture d’écran de la balise body](media/logic-apps-enterprise-integration-flatfile/flatfile-4.png)  
6. Sélectionnez hello **nom de schéma** zone de liste, puis choisissez le schéma hello toouse tooencode hello d’entrée de contenu.    
   ![Capture d’écran de la zone de liste Nom du schéma](media/logic-apps-enterprise-integration-flatfile/flatfile-5.png)  
7. Enregistrez votre travail.   
   ![Capture d’écran de l’icône Enregistrer](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)  

À ce stade, vous avez terminé de configurer votre connecteur d’encodage de fichier plat. Dans une application réelle, vous pouvez vouloir toostore les données de hello encodé dans une application métier-, telles que Salesforce. Ou vous pouvez envoyer ce tooa données encodées partenaire commercial. Vous pouvez facilement ajouter une sortie de hello toosend action Hello encodage action tooSalesforce ou tooyour de partenaire commercial, à l’aide de l’une des hello tous les autres connecteurs fournies.

Vous pouvez maintenant tester votre connecteur en effectuant un point de terminaison demande toohello HTTP, y compris le hello XML contenu dans le corps hello de demande de hello.  

## <a name="create-hello-flat-file-decoding-connector"></a>Créer le fichier plat de hello le décodage du connecteur

> [!NOTE]
> toocomplete ces étapes, vous devez toohave un fichier de schéma déjà téléchargé dans votre compte d’intégration.

1. Ajouter un **demande - HTTP lors de la demande est reçue** application logique de tooyour déclencheur.  
   ![Capture d’écran de déclencheur tooselect](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)    
2. Ajoutez les fichiers plats hello le décodage d’action, comme suit :
   
    a. Sélectionnez hello **plus** signe.
   
    b. Sélectionnez hello **ajouter une action** lien (s’affiche lorsque vous avez sélectionné le signe plus hello).
   
    c. Dans la zone de recherche de hello, entrez *plat* toofilter tous hello toohello actions une que vous souhaitez toouse.
   
    d. Sélectionnez hello **le décodage de fichier plat** option de liste de hello.   
   ![Capture d’écran de l’option Décodage du fichier plat](media/logic-apps-enterprise-integration-flatfile/flatfile-2.png)   
3. Sélectionnez hello **contenu** contrôle. Cela génère une liste de contenu hello à partir des étapes antérieures que vous pouvez utiliser comme toodecode de contenu hello. Notez que hello *corps* hello demande HTTP entrante est disponible toobe utilisé comme hello toodecode contenu. Vous pouvez également entrer toodecode de contenu hello directement dans hello **contenu** contrôle.     
4. Sélectionnez hello *corps* balise. Avis hello body est dupliquée est désormais Bonjour **contenu** contrôle.
5. Sélectionnez Nom hello du schéma hello que vous souhaitez le contenu toouse toodecode hello. Hello capture d’écran suivante montre que *OrderFile* est le nom de schéma sélectionné hello. Ce nom de schéma a été chargé dans le compte d’intégration hello précédemment.
   
   ![Capture d’écran de la boîte de dialogue Décodage du fichier plat](media/logic-apps-enterprise-integration-flatfile/flatfile-decode-1.png)    
6. Enregistrez votre travail.  
   ![Capture d’écran de l’icône Enregistrer](media/logic-apps-enterprise-integration-flatfile/flatfile-6.png)    

À ce stade, vous avez terminé de configurer votre connecteur de décodage de fichier plat. Dans une application réelle, vous pouvez vouloir toostore les données de hello décodée dans une application métier de telles que Salesforce. Vous pouvez facilement ajouter une sortie de hello toosend action Hello décodage tooSalesforce d’action.

Vous pouvez maintenant tester votre connecteur en effectuant un point de terminaison demande toohello HTTP et y compris le contenu XML de hello vous toodecode dans le corps hello de demande de hello.  

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur hello Pack d’intégration Enterprise](logic-apps-enterprise-integration-overview.md "en savoir plus sur le Pack d’intégration Enterprise").  

