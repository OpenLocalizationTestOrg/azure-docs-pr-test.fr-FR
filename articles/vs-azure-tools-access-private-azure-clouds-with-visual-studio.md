---
title: "aaaAccessing clouds privés Azure avec Visual Studio | Documents Microsoft"
description: "Découvrez les ressources de cloud privé de tooaccess à l’aide de Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a>Accès à des clouds privés Azure avec Visual Studio
Par défaut, Visual Studio prend en charge les points de terminaison REST du cloud public Azure. Dans cette rubrique, vous apprendrez comment toouse votre private cloud du certificat tooaccess - et interagir avec - hello cloud privé à partir de Visual Studio.

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a>tooaccess un privé Azure cloud dans Visual Studio
1. Bonjour [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885) pour le cloud privé de hello, téléchargez votre fichier de paramètres de publication, ou contactez votre administrateur pour un fichier de paramètres de publication. Sur la version publique de hello d’Azure, hello toodownload lien il s’agit de [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/). (fichier téléchargé de hello doit avoir une extension `.publishsettings`)

1. Ouvrez Visual Studio.

1. Dans **l’Explorateur de serveurs**, avec le bouton hello **Azure** nœud et, dans le menu contextuel de hello, sélectionnez **gérer et filtrer les abonnements**.
   
    ![Commande Gérer les abonnements](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. Bonjour **gérer les abonnements Microsoft Azure** boîte de dialogue, sélectionnez hello **certificats** onglet, puis sélectionnez **importation**.
   
    ![Importation de certificats Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. Bonjour **les abonnements Microsoft Azure Import** boîte de dialogue, sélectionnez **Parcourir**.

    ![Bouton de boîte de dialogue Importer les abonnements Microsoft Azure hello Parcourir](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. Bonjour **ouvrir** boîte de dialogue Parcourir toohello répertoire dans lequel vous hello enregistré fichier publish-settings, sélectionnez hello fichier et sélectionnez **ouvrir**.

    ![Sélectionnez le fichier de paramètres de publication hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. Lorsque retourné toohello **les abonnements Microsoft Azure Import** boîte de dialogue, sélectionnez **importation**.

    ![Fichier d’importation de paramètres de publication hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    certificats de Hello sont importées à partir du fichier de paramètres de publication hello dans Visual Studio, et vous pouvez maintenant interagir avec vos ressources de cloud privé.
   
## <a name="next-steps"></a>Étapes suivantes
- [Publication tooan Azure Cloud Service à partir de Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- [Téléchargement et importation des paramètres de publication et des informations d’abonnement](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)
