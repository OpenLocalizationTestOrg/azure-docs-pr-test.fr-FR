---
title: "Activer l’aaaAzure capturer des concentrateurs d’événements via le portail | Documents Microsoft"
description: "Activer hello capturer des concentrateurs d’événements à l’aide de hello portail Azure."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/28/2017
ms.author: sethm
ms.openlocfilehash: 27c7528552c497a4d98873a22bd56a991c66247c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-event-hubs-capture-using-hello-azure-portal"></a>Activer la Capture de concentrateurs d’événements à l’aide de hello portail Azure

Vous pouvez configurer la Capture au moment de la création du hub d’événements hello à l’aide de hello [portail Azure](https://portal.azure.com). Vous pouvez soit tooan de données capture hello Azure [stockage d’objets Blob](https://azure.microsoft.com/services/storage/blobs/) conteneur ou tooan [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) compte.

## <a name="capture-data-tooan-azure-storage-account"></a>Compte de stockage Azure tooan de données de capture  

Lorsque vous créez un concentrateur d’événements, vous pouvez activer la Capture en cliquant sur hello **sur** bouton Bonjour **concentrateur d’événements créer** panneau portail. Puis vous spécifiez un compte de stockage et un conteneur en cliquant sur **Azure Storage** Bonjour **capturer le fournisseur** boîte. Comme capturer des concentrateurs d’événements d’utilise l’authentification de service avec le stockage, vous n’avez pas besoin de toospecify une chaîne de connexion de stockage. Sélecteur de ressources Hello sélectionne automatiquement les URI de ressource hello pour votre compte de stockage. Si vous utilisez Azure Resource Manager, vous devez fournir explicitement cet URI en tant que chaîne.

fenêtre Hello par défaut est de 5 minutes. valeur minimale de Hello est 1, hello 15 maximale. Hello **taille** fenêtre a une plage de 10 à 500 Mo.

![][1]

## <a name="capture-data-tooan-azure-data-lake-store-account"></a>Données tooan Azure Data Lake Store compte de capture

tooAzure de données toocapture Data Lake Store, vous créez un compte Data Lake Store et un concentrateur d’événements :

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>Créer un compte Azure Data Lake Store et des dossiers

1. Créer un compte Data Lake Store, conformément aux instructions hello [prise en main Azure Data Lake Store à l’aide de hello Azure portal](../data-lake-store/data-lake-store-get-started-portal.md). 
2. Créez un dossier sous ce compte, en suivant les instructions de hello Bonjour [créer des dossiers dans un compte Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md#createfolder) section.
3. Dans le panneau de compte Data Lake Store hello, cliquez sur **Explorateur de données**.
4. Cliquez sur **Access** (Accès).
5. Cliquez sur **Add**.
6. Bonjour **recherche par nom ou par courrier électronique** zone **Microsoft.EventHubs** , puis sélectionnez cette option. 
7. Hello **autorisations** onglet s’affiche. Définir des autorisations de hello comme indiqué dans la figure suivante de hello :

    ![][6]

8. Cliquez sur **OK**.
9. À présent, créez un dossier dans le dossier racine de hello en dossier cible de toohello de navigation en cliquant sur le nom du dossier hello.
10. Cliquez sur **Access** (Accès).
11. Cliquez sur **Add**.
12. Bonjour **recherche par nom ou par courrier électronique** zone **Microsoft.EventHubs** , puis sélectionnez cette option.
13. Hello **autorisations** onglet s’affiche à nouveau. Définir des autorisations de hello comme indiqué dans la figure suivante de hello :

    ![][5]

### <a name="create-an-event-hub"></a>Création d'un concentrateur d'événements

1. Notez ce concentrateur d’événements hello doit être Bonjour même abonnement Azure que hello Azure Data Lake Store que vous venez de créer. Concentrateur d’événements hello créer, en cliquant sur hello **sur** sous **Capture** Bonjour **concentrateur d’événements créer** panneau portail. 
2. Bonjour **concentrateur d’événements créer** portail panneau, sélectionnez **Azure Data Lake Store** de hello **capturer le fournisseur** boîte.
3. Dans **sélectionnez Data Lake Store**, spécifiez hello compte Data Lake Store que vous avez créé précédemment et hello **le chemin d’accès de données Lake** , entrez le dossier de données hello chemin d’accès toohello vous avez créé.

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>Ajouter ou configurer la fonctionnalité Capture sur un concentrateur d’événements existant

Vous pouvez configurer la fonctionnalité Capture sur des concentrateurs d’événements se trouvant dans des espaces de noms Event Hubs. tooenable de Capture sur un concentrateur d’événements existant, ou toochange vos paramètres de Capture, cliquez sur Bonjour, espace de noms Bonjour tooload **Essentials** panneau, puis cliquez sur le concentrateur d’événements hello pour lequel vous voulez tooenable ou modifiez le paramètre de Capture hello. Enfin, cliquez sur hello **propriétés** section Hello ouvrir le panneau et puis modifiez les paramètres de Capture hello, comme indiqué dans hello suivant chiffres :

### <a name="azure-blob-storage"></a>un stockage Azure Blob

![][2]

### <a name="azure-data-lake-store"></a>Azure Data Lake Store

![][4]

[1]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture1.png
[2]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture2.png
[3]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture3.png
[4]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture4.png
[5]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture5.png
[6]: ./media/event-hubs-capture-enable-through-portal/event-hubs-capture6.png

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez également configurer Event Hubs Capture via des modèles Azure Resource Manager. Pour en savoir plus, consultez la section relative à [l’activation de Capture à l’aide d’un modèle Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md).
