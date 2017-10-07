---
title: aaaUse tooget portail Azure en main Data Lake Store | Documents Microsoft
description: "Utilisez hello toocreate portail Azure un compte Data Lake Store et effectuer des opérations de base Bonjour Data Lake Store"
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
ms.openlocfilehash: 6bb3413f00bfa4393f08aed18bc1d5f8a2f28fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-hello-azure-portal"></a>Prise en main Azure Data Lake Store à l’aide de hello portail Azure
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

Découvrez comment toouse hello toocreate portail Azure un compte Azure Data Lake Store et effectuer des opérations de base telles que créer des dossiers, téléchargent et téléchargement des fichiers de données, supprimez votre compte, un etc.. Pour plus d’informations, consultez l’article [Présentation d’Azure Data Lake Store](data-lake-store-overview.md).

Hello suivant deux vidéos contiennent hello les mêmes informations comme décrit dans cet article :

* [Créer un compte Data Lake Store](https://mix.office.com/watch/1k1cycy4l4gen)
* [Gérer les données dans Data Lake Store à l’aide de hello Explorateur de données](https://mix.office.com/watch/icletrxrh6pc)

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer des éléments suivants de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-an-azure-data-lake-store-account"></a>Créer un compte Azure Data Lake Store

1. Ouverture de session toohello nouvelle [portail Azure](https://portal.azure.com).
2. Cliquez sur **NOUVEAU**, puis sur **Données + Stockage** et enfin sur **Azure Data Lake Store**. Lire les informations de hello Bonjour **Azure Data Lake Store** panneau, puis cliquez sur **créer** dans hello coin inférieur gauche du Panneau de hello.
3. Bonjour **nouveau Data Lake Store** panneau, indiquez les valeurs de hello comme illustré dans hello suivant capture d’écran :
   
    ![Créer un compte Azure Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.New.Account.png "Créer un compte Azure Data Lake")
   
   * **Nom**. Entrez un nom unique pour hello compte Data Lake Store.
   * **Abonnement**. Sélectionnez l’abonnement hello sous lequel vous voulez toocreate un nouveau compte Data Lake Store.
   * **Groupe de ressources**. Sélectionnez un groupe de ressources existant ou hello **nouvel** toocreate option une. Un groupe de ressources est un conteneur réunissant les ressources associées d’une application. Pour plus d’informations, consultez [Groupes de ressources dans Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).
   * **Emplacement**: sélectionnez un emplacement où vous souhaitez compte Data Lake Store de hello toocreate.
   * **Paramètres de chiffrement**. Vous disposez de trois options :
     
     * **Ne pas activer le chiffrement**.
     * **Utiliser les clés gérées par Data Lake Store**.  Si vous souhaitez que Azure Data Lake Store toomanage vos clés de chiffrement.
     * **Choisir des clés dans Azure Key Vault**. Vous pouvez sélectionner un coffre Azure Key Vault existant ou en créer un. clés de hello toouse à partir d’un coffre de clés, vous devez attribuer des autorisations pour hello compte Azure Data Lake Store tooaccess hello Azure Key Vault. Pour obtenir des instructions de hello, consultez [affecter des autorisations tooAzure le coffre de clés](#assign-permissions-to-azure-key-vault).
       
        ![Chiffrement Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-2.png "Chiffrement Data Lake Store")
       
        Cliquez sur **OK** Bonjour **paramètres de chiffrement** panneau.

        Pour plus d’informations, consultez l’article [Chiffrement des données dans Azure Data Lake Store](./data-lake-store-encryption.md).

4. Cliquez sur **Créer**. Si vous avez choisi de tableau de bord toohello toopin hello compte, vous revenez toohello le tableau de bord et vous pouvez voir la progression hello de votre configuration du compte Data Lake Store. Une fois hello compte Data Lake Store est configurée, panneau de compte hello s’affiche.

Vous pouvez également créer un compte Data Lake Store à l’aide de modèles Azure Resource Manager. Ces modèles sont accessibles à partir de la page [Modèles de démarrage rapide Azure](https://azure.microsoft.com/resources/templates/?term=data+lake+store) :

- Sans chiffrement des données : [Deploy Azure Data Lake Store account with no data encryption](https://azure.microsoft.com/en-us/resources/templates/101-data-lake-store-no-encryption/) (Déployer un compte Azure Data Lake Store sans chiffrement des données).
- Avec chiffrement des données à l’aide de Data Lake Store : [Deploy Data Lake Store account with encryption(Data Lake)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-adls/) (Déployer un compte Data Lake Store avec chiffrement (Data Lake)).
- Avec chiffrement des données à l’aide d’Azure Key Vault : [Deploy Data Lake Store account with encryption(Key Vault)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-key-vault/) (Déployer un compte Data Lake Store avec chiffrement (Key Vault)).

### <a name="assign-permissions-to-azure-key-vault"></a>Affecter des autorisations tooAzure le coffre de clés
Si vous avez utilisé des clés de chiffrement tooconfigure Azure Key Vault sur hello compte Data Lake Store, vous devez configurer l’accès entre le compte Data Lake Store de hello et compte de coffre de clés Azure hello. Hello suivant les étapes toodo donc d’effectuer.

1. Si vous avez utilisé des clés à partir de hello Azure Key Vault, panneau hello pour hello compte Data Lake Store affiche un avertissement en haut de hello. Cliquez sur hello de hello avertissement tooopen **configurer des autorisations de coffre de clé** panneau.
   
    ![Chiffrement Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-3.png "Chiffrement Data Lake Store")
2. Panneau de Hello présente deux options tooconfigure accès.
   
   * Dans la première option de hello, cliquez sur **accorder l’autorisation** tooconfigure accès. Hello première option est activée uniquement lorsque hello utilisateur qui a créé le compte Data Lake Store de hello est également un administrateur pour hello Azure Key Vault.
   * Bonjour autre option est applet de commande PowerShell de hello toorun affiché sur le panneau de hello. Vous devez propriétaire hello toobe hello Azure Key Vault ou que vous disposez des autorisations de toogrant de capacité hello sur hello Azure Key Vault. Une fois que vous avez exécuté l’applet de commande hello, revenez toohello panneau, cliquez sur **activer** tooconfigure accès.

## <a name="createfolder"></a>Créer des dossiers dans un compte Azure Data Lake Store
Vous pouvez créer des dossiers sous votre toomanage de compte Data Lake Store et stocker des données.

1. Ouvrez le compte Data Lake Store hello que vous avez créé. Dans le volet gauche de hello, cliquez sur **Parcourir**, cliquez sur **Data Lake Store**, puis à partir du Panneau de Data Lake Store hello, nom du compte sous lequel vous souhaitez que les dossiers de toocreate hello. Si vous avez épinglé hello compte toohello tableau d’accueil, cliquez sur cette vignette de compte.
2. Dans le panneau de votre compte Data Lake Store, cliquez sur **Explorateur de données**.
   
    ![Créer des dossiers dans un compte Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.Folder.png "Créer des dossiers dans un compte Data Lake Store")
3. Dans le panneau de compte Data Lake Store, cliquez sur **nouveau dossier**, entrez un nom pour le nouveau dossier de hello, puis cliquez sur **OK**.
   
    ![Créer des dossiers dans un compte Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Folder.Name.png "Créer des dossiers dans un compte Data Lake Store")
   
    dossier de Hello nouvellement créé est répertorié dans hello **Explorateur de données** panneau. Vous pouvez créer des dossiers imbriqués jusqu'au niveau que vous souhaitez.
   
    ![Créer des dossiers dans un compte Data Lake](./media/data-lake-store-get-started-portal/ADL.New.Directory.png "Créer des dossiers dans un compte Data Lake")

## <a name="uploaddata"></a>Télécharger le compte de données tooAzure Data Lake Store
Vous pouvez télécharger votre tooan données compte Azure Data Lake Store directement dans le dossier de niveau ou tooa de racine hello que vous avez créé dans le compte de hello. Bonjour suivant capture d’écran, procédez comme tooupload d’étapes hello un sous-dossier tooa de fichier à partir de hello **Explorateur de données** panneau. Dans cette capture d’écran, les fichiers hello sont sous-dossier tooa téléchargé indiqué dans les vues miniatures de hello (marquées en rouge).

Si vous recherchez des tooupload de données d’exemple, vous pouvez obtenir hello **Ambulance données** dossier hello [référentiel Git de LAC de données Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

![Charger des données](./media/data-lake-store-get-started-portal/ADL.New.Upload.File.png "Charger des données")

## <a name="properties"></a>Propriétés et actions disponibles sur hello les données stockées
Cliquez sur hello de hello fichier nouvellement ajoutée tooopen **propriétés** panneau. propriétés Hello associées au fichier de hello et les actions de hello que vous pouvez effectuer sur le fichier de hello sont disponibles dans ce panneau. Vous pouvez également copier toofile de chemin d’accès complet hello dans votre compte Azure Data Lake Store, mis en surbrillance dans la zone hello rouge Bonjour suivant capture d’écran :

![Propriétés sur les données de salutation](./media/data-lake-store-get-started-portal/ADL.File.Properties.png "propriétés sur les données de salutation")

* Cliquez sur **aperçu** toosee un aperçu du fichier hello, directement à partir de l’Explorateur de hello. Vous pouvez spécifier le format hello Preview hello également. Cliquez sur **aperçu**, cliquez sur **Format** Bonjour **l’aperçu du fichier** panneau, hello et **Format de fichier aperçu** panneau spécifier hello options telles en tant que nombre de lignes toodisplay, toouse, toouse de délimiteur, etc. de codage.
  
  ![Format de l’aperçu du fichier](./media/data-lake-store-get-started-portal/ADL.File.Preview.png "Format de l’aperçu du fichier")
* Cliquez sur **télécharger** ordinateur de tooyour fichier toodownload hello.
* Cliquez sur **Renommer fichier** fichier hello de toorename.
* Cliquez sur **supprimer le fichier** fichier hello de toodelete.

## <a name="secure-your-data"></a>Sécurisez vos données
Vous pouvez sécuriser les données de salutation stockées dans votre compte Azure Data Lake Store à l’aide d’Azure Active Directory et le contrôle d’accès (ACL). Pour obtenir des instructions sur la façon de toodo qui, consultez [sécurisation des données dans Azure Data Lake Store](data-lake-store-secure-data.md).

## <a name="delete-azure-data-lake-store-account"></a>Supprimer un compte Azure Data Lake Store
Cliquez sur un compte Azure Data Lake Store à partir de votre panneau Data Lake Store, de toodelete **supprimer**. action de hello tooconfirm, vous serez nom de hello tooenter demandées du compte hello que toodelete vous le souhaitez. Entrez le nom hello du compte de hello, puis cliquez sur **supprimer**.

![Supprimer un compte Data Lake](./media/data-lake-store-get-started-portal/ADL.Delete.Account.png "Supprimer un compte Data Lake")

## <a name="next-steps"></a>Étapes suivantes
* [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)
* [Utiliser Azure Data Lake Analytics avec Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Utiliser Azure HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Accéder aux journaux de diagnostic de Data Lake Store](data-lake-store-diagnostic-logs.md)

