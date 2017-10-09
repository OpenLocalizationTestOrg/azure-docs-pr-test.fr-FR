---
title: aaaAzure points de terminaison de Service
description: "Décrit les paramètres de point de terminaison de Service Azure hello Bonjour boîte à outils Azure pour Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9c6125ec-7278-461e-b69c-ed56e844f742
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 357aa56409a894719077f2c8f302575c8ebb6883
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-endpoints"></a>Points de terminaison de service Azure
Points de terminaison de service Azure déterminent que si votre application est déployée tooand géré par la plateforme Azure globale de hello, Azure géré par 21Vianet en Chine ou privée plateforme Azure. Hello **points de terminaison de Service** boîte de dialogue vous permet de toospecify dont vous souhaitez toouse des points de terminaison de service. tooopen hello **points de terminaison de Service** boîte de dialogue, dans Eclipse, cliquez sur **fenêtre**, cliquez sur **préférences**, développez **Azure**, puis cliquez sur **Points de terminaison de service**. Hello du paramètre **ensemble actif** champ détermine le service Azure qui seront utilisés pour hello points de terminaison Azure projets dans votre espace de travail actuel.

Hello Voici hello **points de terminaison de Service** boîte de dialogue.

![][ic719493]

## <a name="tooset-hello-service-endpoints"></a>points de terminaison de service tooset hello
Bonjour **points de terminaison de Service** boîte de dialogue, effectuez l’une de hello suivant des actions :

* Si vous souhaitez toouse hello plateforme Azure globale, à partir de hello **ensemble actif** liste déroulante, sélectionnez **windowsazure.com** et cliquez sur **OK**.

* Si vous souhaitez toouse Azure géré par 21Vianet en Chine, à partir de hello **ensemble actif** liste déroulante, sélectionnez **windowsazure.cn (China)** et cliquez sur **OK**.

* Si vous souhaitez toouse une plateforme Azure privée :

  1. Cliquez sur **Modifier**.

  2. Une boîte de dialogue s’ouvre, vous informant que hello **points de terminaison de Service** boîte de dialogue va être fermée et hello préférence jeux de fichier s’ouvre. Cliquez sur **OK**.

  3. Dans le fichier preferencesets.xml de hello, créez un `preferenceset` élément. Pour ce nouvel élément, créer `name`, `blob`, `management`, `portalURL` et `publishsettings` des attributs et ajouter des valeurs qui correspondent tooyour de plateforme Azure privée. Vous pouvez utiliser les valeurs hello fournis hello existantes `preferenceset` éléments en tant que modèles. **Remarque**: hello valeur utilisée pour hello `blob` attribut doit contenir le texte hello « blob » dans l’URL de hello.

  4. Enregistrez et fermez preferencesets.xml.

  5. Rouvrez hello **points de terminaison de Service** boîte de dialogue.

  6. À partir de hello **ensemble actif** liste déroulante, sélectionnez hello actif défini que vous créé, cliquez sur **OK**.

  7. Une fois que vous avez créé votre plateforme Azure privée `preferenceset` élément, vous pouvez modifier tooit de valeurs affectées hello en cliquant sur hello **modifier** bouton Bonjour **point de terminaison de Services** boîte de dialogue. Vous pouvez également créer plusieurs éléments de plateforme Azure privée `preferenceset` si vous le souhaitez.

## <a name="see-also"></a>Voir aussi
[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]

[Lors de l’installation hello boîte à outils Azure pour Eclipse][Installing hello Azure Toolkit for Eclipse] 

[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719493]: ./media/azure-toolkit-for-eclipse-azure-service-endpoints/ic719493.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268600.aspx -->
