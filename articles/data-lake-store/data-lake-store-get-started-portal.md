---
title: "Prise en main de Data Lake Store à l’aide du Portail Azure | Microsoft Docs"
description: "Utiliser le Portail Azure pour créer un compte Data Lake Store et effectuer des opérations de base dans Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: fea324d0-ad1a-4150-81f0-8682ddb4591c
ms.service: data-lake-store
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/06/2017
ms.author: nitinme
ms.openlocfilehash: fa13266993017374ba49709f8e22fbe6b03a28c7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-data-lake-store-using-the-azure-portal"></a>Prise en main d’Azure Data Lake Store à l’aide du portail Azure
> [!div class="op_single_selector"]
> * [Portail](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Kit SDK .NET](data-lake-store-get-started-net-sdk.md)
> * [Kit SDK Java](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.JS](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Apprenez à utiliser le portail Azure pour créer un compte Azure Data Lake Store et effectuer des opérations de base telles que la création de dossiers, le chargement et le téléchargement de fichiers de données, la suppression de votre compte, etc. Pour plus d’informations, consultez l’article [Présentation d’Azure Data Lake Store](data-lake-store-overview.md).

Les deux vidéos ci-après contiennent les mêmes informations que celles décrites dans cet article :

* [Créer un compte Data Lake Store](https://mix.office.com/watch/1k1cycy4l4gen)
* [Manage data in Data Lake Store using the Data Explorer (Gérer les données dans Data Lake Store à l’aide de l’Explorateur de données)](https://mix.office.com/watch/icletrxrh6pc)

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-an-azure-data-lake-store-account"></a>Créer un compte Azure Data Lake Store

1. Inscrivez-vous au nouveau [portail Azure](https://portal.azure.com).
2. Cliquez sur **NOUVEAU**, puis sur **Données + Stockage** et enfin sur **Azure Data Lake Store**. Lisez les informations contenues dans le panneau **Azure Data Lake Store**, puis cliquez sur **Créer** dans le coin inférieur gauche du panneau.
3. Dans le panneau **Nouveau magasin Data Lake Store**, fournissez les valeurs indiquées dans la capture d’écran suivante :
   
    ![Créer un compte Azure Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.New.Account.png "Créer un compte Azure Data Lake")
   
   * **Nom**. Entrez un nom unique pour le compte Data Lake Store.
   * **Abonnement**. Sélectionnez l’abonnement sous lequel vous souhaitez créer un nouveau compte Data Lake Store.
   * **Groupe de ressources**. Sélectionnez un groupe de ressources existant ou sélectionnez l’option **Créer** pour en créer un. Un groupe de ressources est un conteneur réunissant les ressources associées d’une application. Pour plus d’informations, consultez [Groupes de ressources dans Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).
   * **Emplacement**: sélectionnez l'emplacement où vous souhaitez créer le compte Data Lake Store.
   * **Paramètres de chiffrement**. Vous disposez de trois options :
     
     * **Ne pas activer le chiffrement**.
     * **Utiliser les clés gérées par Data Lake Store**.  Sélectionnez cette option si vous voulez qu’Azure Data Lake Store gère vos clés de chiffrement.
     * **Choisir des clés dans Azure Key Vault**. Vous pouvez sélectionner un coffre Azure Key Vault existant ou en créer un. Pour utiliser les clés d’un coffre Key Vault, vous devez attribuer des autorisations permettant au compte Azure Data Lake Store d’accéder à Azure Key Vault. Pour obtenir les instructions correspondantes, reportez-vous à la section [Attribuer des autorisations à Azure Key Vault](#assign-permissions-to-azure-key-vault).
       
        ![Chiffrement Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-2.png "Chiffrement Data Lake Store")
       
        Cliquez sur **OK** dans le panneau **Paramètres de chiffrement**.

        Pour plus d’informations, consultez l’article [Chiffrement des données dans Azure Data Lake Store](./data-lake-store-encryption.md).

4. Cliquez sur **Create**. Si vous choisissez d’épingler le compte au tableau de bord, vous serez renvoyé au tableau de bord et vous pourrez voir la progression de l’approvisionnement de votre compte Data Lake Store. Une fois le compte Data Lake Store approvisionné, le panneau du compte s'affiche.

Vous pouvez également créer un compte Data Lake Store à l’aide de modèles Azure Resource Manager. Ces modèles sont accessibles à partir de la page [Modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/?term=data+lake+store) :

- Sans chiffrement des données : [Deploy Azure Data Lake Store account with no data encryption](https://azure.microsoft.com/en-us/resources/templates/101-data-lake-store-no-encryption/) (Déployer un compte Azure Data Lake Store sans chiffrement des données).
- Avec chiffrement des données à l’aide de Data Lake Store : [Deploy Data Lake Store account with encryption(Data Lake)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-adls/) (Déployer un compte Data Lake Store avec chiffrement (Data Lake)).
- Avec chiffrement des données à l’aide d’Azure Key Vault : [Deploy Data Lake Store account with encryption(Key Vault)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-key-vault/) (Déployer un compte Data Lake Store avec chiffrement (Key Vault)).

### <a name="assign-permissions-to-azure-key-vault"></a>Attribuer des autorisations à Azure Key Vault
Si vous avez utilisé des clés d’un coffre Azure Key Vault pour configurer le chiffrement sur le compte Data Lake Store, vous devez configurer l’accès entre le compte Data Lake Store et le compte Azure Key Vault. Pour ce faire, procédez comme suit.

1. Si vous avez utilisé des clés du coffre Azure Key Vault, un avertissement s’affiche en haut du panneau du compte Data Lake Store. Cliquez dessus pour ouvrir le panneau **Configurer les autorisations de Key Vault**.
   
    ![Chiffrement Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-3.png "Chiffrement Data Lake Store")
2. Le panneau affiche deux options possibles pour configurer l’accès.
   
   * Dans la première option, cliquez sur **Accorder l’autorisation** pour configurer l’accès. La première option est activée uniquement lorsque l’utilisateur qui a créé le compte Data Lake Store est également administrateur du coffre Azure Key Vault.
   * L’autre option consiste à exécuter l’applet de commande PowerShell qui s’affiche dans le panneau. Vous devez être propriétaire de coffre Azure Key Vault ou avoir le droit d’accorder des autorisations sur le coffre Azure Key Vault. Après avoir exécuté l’applet de commande, revenez au panneau et cliquez sur **Activer** pour configurer l’accès.

## <a name="createfolder"></a>Créer des dossiers dans un compte Azure Data Lake Store
Vous pouvez créer des dossiers sous votre compte Data Lake Store pour gérer et stocker des données.

1. Ouvrez le compte Data Lake Store que vous avez créé. Dans le volet gauche, cliquez sur **Parcourir**, puis sur **Data Lake Store**. Ensuite, dans le panneau Data Lake Store, cliquez sur le nom du compte sous lequel vous souhaitez créer des dossiers. Si vous avez épinglé le compte au tableau d'accueil, cliquez sur la vignette de ce compte.
2. Dans le panneau de votre compte Data Lake Store, cliquez sur **Explorateur de données**.
   
    ![Créer des dossiers dans un compte Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.Folder.png "Créer des dossiers dans un compte Data Lake Store")
3. Dans le panneau de votre compte Data Lake Store, cliquez sur **Nouveau dossier**, entrez un nom pour le nouveau dossier, puis cliquez sur **OK**.
   
    ![Créer des dossiers dans un compte Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Folder.Name.png "Créer des dossiers dans un compte Data Lake Store")
   
    Le dossier que vous venez de créer apparaît dans le panneau **Explorateur de données**. Vous pouvez créer des dossiers imbriqués jusqu'au niveau que vous souhaitez.
   
    ![Créer des dossiers dans un compte Data Lake](./media/data-lake-store-get-started-portal/ADL.New.Directory.png "Créer des dossiers dans un compte Data Lake")

## <a name="uploaddata"></a>Télécharger des données sur un compte Azure Data Lake Store
Vous pouvez télécharger vos données sur un compte Azure Data Lake Store directement à la racine ou dans un dossier que vous avez créé dans le compte. Suivez les étapes de la capture d’écran ci-après pour charger un fichier vers un sous-dossier du panneau **Explorateur de données**. Dans cette capture d’écran, le fichier est chargé vers un sous-dossier visible dans l’arborescence de navigation (encadré en rouge).

Si vous recherchez des exemples de données à charger, vous pouvez récupérer le dossier **Données Ambulance** dans le [Référentiel Git Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

![Charger des données](./media/data-lake-store-get-started-portal/ADL.New.Upload.File.png "Charger des données")

## <a name="properties"></a>Propriétés et actions disponibles sur les données stockées
Cliquez sur le fichier nouvellement ajouté pour ouvrir le panneau **Propriétés** . Les propriétés associées au fichier et les actions que vous pouvez effectuer sur le fichier sont disponibles dans ce panneau. Vous pouvez également copier la totalité du chemin d’accès au fichier dans votre compte Azure Data Lake Store, encadré en rouge dans la capture d’écran suivante :

![Propriétés sur les données](./media/data-lake-store-get-started-portal/ADL.File.Properties.png "Propriétés sur les données")

* Cliquez sur **Aperçu** pour afficher un aperçu du fichier, directement à partir du navigateur. Vous pouvez également spécifier le format de l'aperçu. Cliquez sur **Aperçu**, puis sur **Format** dans le panneau **Aperçu du fichier**. Ensuite, dans le panneau **Format de l’aperçu du fichier**, spécifiez les options comme le nombre de lignes à afficher, l’encodage à utiliser, le séparateur à utiliser, etc.
  
  ![Format de l’aperçu du fichier](./media/data-lake-store-get-started-portal/ADL.File.Preview.png "Format de l’aperçu du fichier")
* Cliquez sur **Télécharger** pour télécharger le fichier sur votre ordinateur.
* Cliquez sur **Renommer le fichier** pour renommer le fichier.
* Cliquez sur **Supprimer le fichier** pour supprimer le fichier.

## <a name="secure-your-data"></a>Sécurisez vos données
Vous pouvez sécuriser les données stockées dans votre compte Azure Data Lake Store à l'aide d'Azure Active Directory et Access Control (ACL). Pour savoir comment procéder, consultez [Sécurisation des données dans Azure Data Lake Store](data-lake-store-secure-data.md).

## <a name="delete-azure-data-lake-store-account"></a>Supprimer un compte Azure Data Lake Store
Pour supprimer un compte Azure Data Lake Store, cliquez sur **Supprimer**dans le panneau de votre Data Lake Store. Pour confirmer l'action, vous devrez entrer le nom du compte que vous souhaitez supprimer. Entrez le nom du compte, puis cliquez sur **Supprimer**.

![Supprimer un compte Data Lake](./media/data-lake-store-get-started-portal/ADL.Delete.Account.png "Supprimer un compte Data Lake")

## <a name="next-steps"></a>Étapes suivantes
* [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)
* [Utiliser Azure Data Lake Analytics avec Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Utiliser Azure HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Accéder aux journaux de diagnostic de Data Lake Store](data-lake-store-diagnostic-logs.md)

