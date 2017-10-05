---
title: "Activer Azure Event Hubs Capture à l’aide du portail | Microsoft Docs"
description: "Activez la fonctionnalité Event Hubs Capture à l’aide du portail Azure."
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
ms.openlocfilehash: 0cbf45dce922647f2996f929d2c7cf885a2f4db4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="enable-event-hubs-capture-using-the-azure-portal"></a>Activer Event Hubs Capture à l’aide du portail Azure

Vous pouvez configurer la fonctionnalité Capture lors de la création du concentrateur d’événements, à l’aide du [portail Azure](https://portal.azure.com). Vous pouvez capturer les données vers un conteneur de [Stockage Blob](https://azure.microsoft.com/services/storage/blobs/) Azure, ou vers un compte [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).

## <a name="capture-data-to-an-azure-storage-account"></a>Capturer des données vers un compte de stockage Azure  

Lorsque vous créez un concentrateur d’événements, vous pouvez activer la Capture en cliquant sur le **sur** situé dans le **concentrateur d’événements créer** panneau portail. Précisez ensuite le compte et le conteneur de stockage à utiliser en cliquant sur **Stockage Azure** dans la zone **Fournisseur de capture**. Comme Event Hubs Capture utilise l’authentification de service à service avec le stockage, il est inutile de spécifier une chaîne de connexion de stockage. Le sélecteur de ressources sélectionne automatiquement l’URI de ressource pour votre compte de stockage. Si vous utilisez Azure Resource Manager, vous devez fournir explicitement cet URI en tant que chaîne.

La fenêtre temporelle par défaut est de cinq minutes. La valeur minimum est 1, la valeur maximum 15. La fenêtre **Taille** présente une plage de 10 à 500 Mo.

![][1]

## <a name="capture-data-to-an-azure-data-lake-store-account"></a>Capturer des données vers un compte Azure Data Lake Store

Pour capturer des données vers Azure Data Lake Store, vous créez un compte Data Lake Store et un concentrateur d’événements :

### <a name="create-an-azure-data-lake-store-account-and-folders"></a>Créer un compte Azure Data Lake Store et des dossiers

1. Pour créer un compte Data Lake Store, suivez les instructions de [Prise en main d’Azure Data Lake Store avec le portail Azure](../data-lake-store/data-lake-store-get-started-portal.md). 
2. Pour créer un dossier dans ce compte, suivez les instructions dans la section [Créer des dossiers dans un compte Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md#createfolder).
3. Dans le panneau de compte Data Lake Store, cliquez sur **Explorateur de données**.
4. Cliquez sur **Access** (Accès).
5. Cliquez sur **Add**.
6. Dans la zone **Search by name or email**(Recherche par nom ou e-mail), tapez **Microsoft.EventHubs** et sélectionnez cette option. 
7. L’onglet **Permissions** s’affiche. Définissez les autorisations comme indiqué dans la figure suivante :

    ![][6]

8. Cliquez sur **OK**.
9. Créez maintenant un dossier dans le dossier racine en naviguant vers le dossier cible et en cliquant sur son nom.
10. Cliquez sur **Access** (Accès).
11. Cliquez sur **Add**.
12. Dans la zone **Search by name or email**(Recherche par nom ou e-mail), tapez **Microsoft.EventHubs** et sélectionnez cette option.
13. L’onglet **Permissions** s’affiche de nouveau. Définissez les autorisations comme indiqué dans la figure suivante :

    ![][5]

### <a name="create-an-event-hub"></a>Création d'un concentrateur d'événements

1. Remarque : le concentrateur d’événements doit se trouver dans le même abonnement Azure que le compte Azure Data Lake Store que vous venez de créer. Créer le concentrateur d’événements, en cliquant sur le **sur** sous **capturer** dans les **concentrateur d’événements créer** panneau portail. 
2. Dans le **concentrateur d’événements créer** portail panneau, sélectionnez **Azure Data Lake Store** à partir de la **capturer le fournisseur** boîte.
3. Dans **Sélectionner Data Lake Store**, spécifiez le compte Data Lake Store que vous avez créé précédemment, puis entrez le chemin d’accès au dossier de données que vous avez créé dans le champ **Chemin d’accès Data Lake**.

    ![][3]

## <a name="add-or-configure-capture-on-an-existing-event-hub"></a>Ajouter ou configurer la fonctionnalité Capture sur un concentrateur d’événements existant

Vous pouvez configurer la fonctionnalité Capture sur des concentrateurs d’événements se trouvant dans des espaces de noms Event Hubs. Pour activer Capture sur un concentrateur d’événements existant, ou pour modifier les paramètres de cette fonctionnalité, cliquez sur l’espace de noms afin de charger le panneau **Essentials**, puis cliquez sur le concentrateur d’événements pour lequel vous souhaitez activer ou modifier la configuration de Capture. Enfin, cliquez sur le **propriétés** section du panneau ouvert, puis modifiez les paramètres de Capture, comme indiqué dans les figures suivantes :

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
