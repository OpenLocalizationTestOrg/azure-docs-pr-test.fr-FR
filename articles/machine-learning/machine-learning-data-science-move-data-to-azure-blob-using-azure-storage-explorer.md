---
title: "tooand de données aaaMove à partir du stockage d’objets Blob avec l’Explorateur de stockage Azure | Documents Microsoft"
description: "Déplacer les données tooand de stockage d’objets Blob Azure à l’aide de l’Explorateur de stockage Azure"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 10bd283f-0875-4c67-af63-6492270b7656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 38d3bc009950c97d8474b0acceaf74814638dac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azure-storage-explorer"></a>Déplacer les données tooand de stockage d’objets Blob Azure à l’aide de l’Explorateur de stockage Azure
Explorateur de stockage Azure est un outil gratuit de Microsoft qui vous permet de toowork avec des données de stockage Azure sur Windows, Mac OS et Linux. Cette rubrique décrit comment toouse il tooupload et téléchargement des données à partir d’Azure stockage d’objets blob. outil de Hello peut être téléchargé à partir de [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Si vous utilisez une machine virtuelle qui a été configuré avec des scripts hello fournies par [des machines virtuelles de science des données dans Azure](machine-learning-data-science-virtual-machines.md), puis de l’Explorateur de stockage Azure est déjà installé sur hello machine virtuelle.
> 
> [!NOTE]
> Pour un stockage d’objets blob tooAzure présentation complète, consultez trop[principes de base Azure Blob](../storage/blobs/storage-dotnet-how-to-use-blobs.md) et [Service d’objets Blob Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).   
> 
> 

## <a name="prerequisites"></a>Composants requis
Ce document suppose que vous disposez d’un abonnement Azure, un compte de stockage et la clé de stockage correspondante hello pour ce compte. Avant de charger ou télécharger des données, vous devez connaître le nom et la clé de votre compte Azure Storage. 

* tooset d’un abonnement Azure, consultez [version d’évaluation d’un mois gratuite](https://azure.microsoft.com/pricing/free-trial/).
* Pour obtenir des instructions sur la création d’un compte de stockage, ainsi que des informations sur le compte et la clé, consultez [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md). Rendre une clé d’accès Remarque hello pour votre compte de stockage que vous avez besoin de ce compte de toohello tooconnect clé avec l’outil d’Explorateur de stockage Azure hello.
* outil d’Explorateur de stockage Azure Hello peut être téléchargé à partir de [Microsoft Azure Storage Explorer](http://storageexplorer.com/). Accepter hello les valeurs par défaut pendant installer.

<a id="explorer"></a>

## <a name="use-azure-storage-explorer"></a>Utiliser Azure Storage Explorer
Hello suivant le document d’étapes comment tooupload/téléchargement des données à l’aide de l’Explorateur de stockage Azure. 

1. Lancez Microsoft Azure Storage Explorer.
2. toobring des hello **tooyour compte de connexion...**  Assistant, sélectionnez **les paramètres de compte Azure** icône, puis **ajouter un compte** vous entrez des informations d’identification. ![Ajouter un compte de stockage Azure](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)
3. toobring des hello **connecter tooAzure stockage** hello Assistant, sélectionnez **connecter tooAzure stockage** icône. ![Se connecter tooAzure stockage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)
4. Entrez la clé d’accès hello à partir de votre compte de stockage Azure sur hello **connecter tooAzure stockage** Assistant, puis **suivant**. ![Se connecter tooAzure stockage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)
5. Entrez le nom de compte de stockage Bonjour **nom de compte** zone, puis sélectionnez **suivant**. ![Attacher un stockage externe](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)
6. le compte de stockage Hello ajouté doit maintenant être affiché. toocreate un conteneur d’objets blob dans un compte de stockage avec le bouton droit hello **conteneurs d’objets Blob** nœud dans ce compte, sélectionnez **créer un conteneur d’objets Blob**et entrez un nom.
7. conteneur de données de tooa tooupload, hello de conteneur et cliquez sur la cible du hello sélectionnez **télécharger** bouton.![ Comptes de stockage](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)
8. Cliquez sur hello **...**  toohello à droite de hello **fichiers** , sélectionnez un ou plusieurs tooupload de fichiers à partir du système de fichiers hello puis cliquez sur **télécharger** toobegin de téléchargement de fichiers de hello.![ Télécharger des fichiers](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)
9. données toodownload, en sélectionnant hello d’objets blob dans toodownload de conteneur correspondant hello et cliquez sur **télécharger**. ![Télécharger des fichiers](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)

