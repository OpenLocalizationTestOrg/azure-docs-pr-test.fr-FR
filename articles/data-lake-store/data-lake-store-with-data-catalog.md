---
title: "données aaaRegister Data Lake Store dans Azure Data Catalog | Documents Microsoft"
description: "Référencer des données de Data Lake Store dans Azure Data Catalog"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3294d91e-a723-41b5-9eca-ace0ee408a4b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3e895b42cab4ba39d288950763312a243883cbdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-from-data-lake-store-in-azure-data-catalog"></a>Référencer des données de Data Lake Store dans Azure Data Catalog
Dans cet article, vous allez apprendre comment toointegrate Azure Data Lake stocker avec Azure Data Catalog toomake vos données détectables au sein d’une organisation en l’intégrant avec le catalogue de données. Pour plus d’informations sur le catalogage des données, consultez [Azure Data Catalog](../data-catalog/data-catalog-what-is-data-catalog.md). toounderstand les scénarios dans lesquels vous pouvez utiliser le catalogue de données, consultez [scénarios courants d’Azure Data Catalog](../data-catalog/data-catalog-common-scenarios.md).

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Activez votre abonnement Azure** pour la version d’évaluation publique de Data Lake Store. Consultez les [instructions](data-lake-store-get-started-portal.md).
* **Compte Azure Data Lake Store**. Suivez les instructions de hello à [prise en main Azure Data Lake Store à l’aide de hello Azure Portal](data-lake-store-get-started-portal.md). Pour ce didacticiel, créons un compte Data Lake Store appelé **datacatalogstore**.

    Une fois que vous avez créé le compte de hello, téléchargez un tooit de jeu de données d’exemple. Pour ce didacticiel, nous télécharger tous les fichiers .csv hello hello **AmbulanceData** dossier Bonjour [référentiel Git de LAC de données Azure](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/). Vous pouvez utiliser différents clients, tels que [Azure Storage Explorer](http://storageexplorer.com/), conteneur d’objets blob tooa tooupload données.
* **Azure Data Catalog**. Votre organisation doit déjà avoir un catalogue de données Azure créé pour votre organisation. Un seul catalogue est autorisé pour chaque organisation.

## <a name="register-data-lake-store-as-a-source-for-data-catalog"></a>Inscrire Data Lake Store comme source pour Data Catalog

> [!VIDEO https://channel9.msdn.com/Series/AzureDataLake/ADCwithADL/player]

1. Accédez trop`https://azure.microsoft.com/services/data-catalog`, puis cliquez sur **prise en main**.
2. Vous connecter au portail d’Azure Data Catalog hello, puis cliquez sur **publier des données**.

    ![Référencer une source de données](./media/data-lake-store-with-data-catalog/register-data-source.png "Référencer une source de données")
3. Dans la page suivante de hello, cliquez sur **lancer l’Application**. Cela télécharge le fichier manifeste d’application hello sur votre ordinateur. Double-cliquez sur hello fichier manifeste toostart hello application.
4. Dans la page d’accueil hello, cliquez sur **connecter**et entrez vos informations d’identification.

    ![Écran d’accueil](./media/data-lake-store-with-data-catalog/welcome.screen.png "Écran d’accueil")
5. Sur la page Sélectionner une Source de données de hello, sélectionnez **Azure Data Lake**, puis cliquez sur **suivant**.

    ![Sélectionner une source de données](./media/data-lake-store-with-data-catalog/select-source.png "Sélectionner une source de données")
6. Sur la page suivante de hello, fournissent hello nom du compte Data Lake Store que vous souhaitez tooregister dans le catalogue de données. Hello autres options par défaut et cliquez sur **connexion**.

    ![Se connecter toodata source](./media/data-lake-store-with-data-catalog/connect-to-source.png "Connect toodata source")
7. page suivante de Hello peut être divisé en hello suivant des segments.

    a. Hello **hiérarchie serveur** boîte représente la structure de dossiers de compte Data Lake Store hello. **$Root** représente hello racine du compte Data Lake Store, et **AmbulanceData** représente hello dossier créé à la racine hello hello compte Data Lake Store.

    b. Hello **objets disponibles** zone répertorie les fichiers hello et des dossiers sous hello **AmbulanceData** dossier.

    c. **Objets toobe inscrit boîte** hello de listes de fichiers et dossiers que vous souhaitez tooregister dans Azure Data Catalog.

    ![Afficher la structure des données](./media/data-lake-store-with-data-catalog/view-data-structure.png "Afficher la structure des données")
8. Pour ce didacticiel, vous devez inscrire tous les fichiers hello dans le répertoire de hello. Pour ce faire, cliquez sur hello (![déplacer des objets](./media/data-lake-store-with-data-catalog/move-objects.png "déplacer des objets")) toomove bouton tous hello trop de fichiers**toobe objets inscrits** boîte.

    Étant donné que les données de salutation seront inscrit dans un catalogue de données à l’échelle de l’organisation, il est un recommandé tooadd des métadonnées que vous pouvez utiliser ultérieurement tooquickly localiser les données de salutation. Par exemple, vous pouvez ajouter une adresse de messagerie pour le propriétaire de données hello (par exemple, une qui transfère les données de salutation) ou ajouter une étiquette de données hello tooidentify. capture d’écran Hello ci-dessous montre une balise que nous ajoutons toohello données.

    ![Afficher la structure des données](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "Afficher la structure des données")

    Cliquez sur **S'inscrire**.
9. Hello capture d’écran suivante indique que les données de salutation sont correctement inscrite dans hello catalogue de données.

    ![Référencement terminé](./media/data-lake-store-with-data-catalog/registration-complete.png "Afficher la structure des données")
10. Cliquez sur **vue Portal** toogo toohello portail du catalogue de données de sauvegarde et vérifiez que vous pouvez maintenant hello d’accès enregistré les données à partir du portail de hello. les données de salutation toosearch, vous pouvez utiliser balise hello que vous avez utilisé lors de l’enregistrement des données de salutation.

     ![Rechercher des données dans le catalogue](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "Rechercher des données dans le catalogue")
11. Vous pouvez désormais effectuer les opérations telles que l’ajout d’annotations et données toohello de documentation. Pour plus d’informations, consultez hello suivant liens.

    * [Annoter des sources de données dans Data Catalog](../data-catalog/data-catalog-how-to-annotate.md)
    * [Documenter des sources de données dans Data Catalog](../data-catalog/data-catalog-how-to-documentation.md)

## <a name="see-also"></a>Voir aussi
* [Annoter des sources de données dans Data Catalog](../data-catalog/data-catalog-how-to-annotate.md)
* [Documenter des sources de données dans Data Catalog](../data-catalog/data-catalog-how-to-documentation.md)
* [Intégrer Data Lake Store à d’autres services Azure](data-lake-store-integrate-with-other-services.md)
