---
title: "aaaGet a démarré avec l’Explorateur de stockage (version préliminaire) | Documents Microsoft"
description: "Gérer les ressources de stockage Azure avec l’Explorateur de stockage (version préliminaire)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1ed0f096-494d-49c4-ab71-f4164ee19ec8
ms.service: storage
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/17/2017
ms.author: kraigb
ms.openlocfilehash: 57737b51baace92858eb07c7dbc3139bd7e041f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-storage-explorer-preview"></a>Prise en main de l’Explorateur de stockage (version préliminaire)
## <a name="overview"></a>Vue d'ensemble
Explorateur de stockage Azure (aperçu) est une application autonome qui vous permet de travail tooeasily avec des données de stockage Azure sur Windows, Mac OS et Linux. Dans cet article, vous découvrez hello différentes manières de se connecter tooand gestion de vos comptes de stockage Azure.

![Explorateur de stockage Microsoft Azure (version préliminaire)][15]

## <a name="prerequisites"></a>Composants requis
* [Télécharger et installer l’Explorateur de stockage (version préliminaire)](http://www.storageexplorer.com)

## <a name="connect-tooa-storage-account-or-service"></a>Connexion de compte de stockage tooa ou service
Explorateur de stockage (version préliminaire) offre plusieurs moyens tooconnect toostorage comptes. Vous pouvez par exemple afficher :
* Se connecter toostorage les comptes associés à vos abonnements Azure.
* Se connecter toostorage comptes et les services qui sont partagés à partir d’autres abonnements Azure.
* Se connecter tooand gérer le stockage local à l’aide de hello émulateur de stockage Azure. 

En outre, vous pouvez utiliser des comptes de stockage Azure à l’échelle internationale et nationale :

* [Se connecter tooan abonnement Azure](#connect-to-an-azure-subscription): gérer les ressources de stockage qui appartiennent tooyour abonnement Azure.
* [Utilisez un stockage de développement local](#work-with-local-development-storage): gérer le stockage local à l’aide de hello émulateur de stockage Azure.
* [Attacher tooexternal stockage](#attach-or-detach-an-external-storage-account): gérer les ressources de stockage qui appartiennent tooanother abonnement Azure ou qui sont sous nationales clouds Azure à l’aide du compte de stockage hello nom, clé et points de terminaison.
* [Attacher un compte de stockage à l’aide d’un SAS](#attach-storage-account-using-sas): gérer les ressources de stockage qui appartiennent tooanother abonnement Azure à l’aide d’une signature d’accès partagé (SAS).
* [Attachez un service à l’aide d’un SAS](#attach-service-using-sas): gérer un service de stockage spécifique (conteneur d’objets blob, file d’attente ou table) qui appartient tooanother abonnement Azure à l’aide d’un SAS.

## <a name="connect-tooan-azure-subscription"></a>Se connecter tooan abonnement Azure
> [!NOTE]
> Si vous ne possédez pas de compte Azure, vous pouvez [vous inscrire à un essai gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) ou [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
>
>

1. Dans l’Explorateur de stockage (version préliminaire), sélectionnez les **paramètres de compte Azure**.

    ![paramètres de compte Azure][0]

2. volet de gauche de Hello affiche tous les comptes de Microsoft hello que vous êtes connecté. tooconnect tooanother compte, sélectionnez **ajouter un compte**, puis suivez toosign d’instructions hello avec un compte Microsoft associé au moins un abonnement Azure actif.

    >[!NOTE]
    >Connexion toonational Azure (par exemple, Azure situés en Allemagne, Azure Government et en Chine Azure via la connexion) n’est pas pris en charge actuellement. Consultez hello » attacher ou détacher d’un compte de stockage externe « section sur la manière de tooconnect toonational des comptes de stockage Azure.

3. Après avoir correctement connectez-vous avec un compte Microsoft, hello gauche volet est rempli avec hello Azure abonnements associés à ce compte. Sélectionnez hello abonnements Azure que vous souhaitez toowork avec, puis sélectionnez **appliquer**. (En sélectionnant **tous les abonnements** bascule en sélectionnant la totalité ou aucun de hello répertoriés abonnements Azure.)

    ![Sélectionner les abonnements Azure][3]  
    volet de gauche Hello affiche les comptes de stockage hello associées aux abonnements Azure de hello sélectionné.

    ![Abonnements Azure sélectionnés][4]

## <a name="connect-tooan-azure-stack-subscription"></a>Connecter tooan Azure pile abonnement

Pour plus d’informations sur l’abonnement de Azure pile tooan connexion, consultez [connecter l’Explorateur de stockage tooan abonnement de Azure pile](azure-stack/azure-stack-storage-connect-se.md).

## <a name="work-with-local-development-storage"></a>Utilisation du stockage de développement local
Avec l’Explorateur de stockage (version préliminaire), vous pouvez travailler sur le stockage local à l’aide de hello émulateur de stockage Azure. Cette approche vous permet d’écrire du code par rapport à et stockage de test sans nécessairement disposer d’un compte de stockage déployé sur Azure, car le compte de stockage hello est émulé par hello émulateur de stockage Azure.

> [!NOTE]
> Hello émulateur de stockage Azure est actuellement pris en charge uniquement pour Windows.
>
>

1. Dans hello du volet de gauche de l’Explorateur de stockage (version préliminaire), développez hello **(locale et associés)** > **comptes de stockage** > **(développement)** nœud.

    ![Nœud de développement local][21]

2. Si vous n’avez pas encore installé hello émulateur de stockage Azure, vous êtes invité à toodo ce via une barre d’informations. Si la barre d’informations hello s’affiche, sélectionnez **version la plus récente hello téléchargement**, puis installez les émulateur hello.

    ![Invite de téléchargement de l’émulateur de stockage Azure][22]

3. Une fois que l’émulateur de hello est installé, vous pouvez créer et travailler avec des objets BLOB local, les files d’attente et les tables. toolearn comment toowork avec chaque compte de stockage de type, consultez hello suivantes :

    * [Manage Azure blob storage resources (Gérer les ressources Azure Blob Storage)](vs-azure-tools-storage-explorer-blobs.md)
    * Manage Azure file share storage resources (Gérer les ressources de stockage de partage de fichiers Azure) - *Bientôt disponible*
    * Manage Azure queue storage resources (Gérer les ressources de stockage File d’attente Azure) - *Bientôt disponible*
    * Manage Azure table storage resources (Gérer les ressources de stockage Table Azure) - *Bientôt disponible*

## <a name="attach-or-detach-an-external-storage-account"></a>Attacher ou détacher un compte de stockage externe
Avec l’Explorateur de stockage (version préliminaire), vous pouvez joindre des comptes de stockage tooexternal afin que les comptes de stockage peuvent être facilement partagées. Cette section explique comment tooattach too(and detach from) comptes de stockage externe.

### <a name="get-hello-storage-account-credentials"></a>Obtenir des informations d’identification de compte de stockage hello
tooshare un compte de stockage externe, propriétaire hello de ce compte doit tout d’abord obtenir les informations d’identification hello (nom de compte et de la clé) pour le compte de la hello et ensuite partager ces informations avec personne hello qui souhaite tooattach toothat (externe) compte. Vous pouvez obtenir des informations d’identification du compte de stockage hello via hello portail Azure en effectuant hello des opérations suivantes :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).

2. Sélectionnez **Parcourir**.

3. Sélectionnez **Comptes de stockage**.

4. Sur hello **comptes de stockage** panneau, le compte de stockage hello sélectionnez souhaité.

5. Sur hello **paramètres** panneau pour hello sélectionné compte de stockage, sélectionnez **clés d’accès**.

    ![Option Clés d’accès][5]

6. Sur hello **clés d’accès** panneau, hello de copie **nom de compte de stockage** et **key1** valeurs à utiliser lors de l’attachement du compte de stockage toohello.

    ![Clés d’accès][6]

### <a name="attach-tooan-external-storage-account"></a>Attacher le compte de stockage externe tooan
compte de stockage externe tooattach tooan, vous devez nom et la clé du compte hello. Hello « Get hello stockage compte informations d’identification » section explique comment ces valeurs à partir de tooobtain hello portail Azure. Toutefois, dans le portail hello, clé de compte hello est appelé **key1**. Par conséquent, lorsque l’Explorateur de stockage (version préliminaire) demande une clé de compte, vous entrez hello **key1** valeur.

1. Dans l’Explorateur de stockage (version préliminaire), sélectionnez **connecter tooAzure**.

    ![Option de stockage tooAzure de connexion][23]

2. Bonjour **connecter tooAzure stockage** boîte de dialogue, spécifiez la clé de compte hello (hello **key1** valeur hello portail Azure), puis sélectionnez **suivant**.

    > [!NOTE]
    > Vous pouvez entrer la chaîne de connexion de stockage hello à partir d’un compte de stockage sur Azure national. Par exemple, comptes de stockage tooconnect tooAzure Allemagne, entrez connexion chaînes similaires toohello informations suivantes : 
    >
    >* DefaultEndpointsProtocol=https
    >* AccountName=cawatest03
    >* AccountKey=<storage_account_key>
    >* EndpointSuffix=core.cloudapi.de
    
    >Vous pouvez obtenir la chaîne de connexion hello de hello Azure portail Bonjour même façon comme décrit dans hello section de « Obtenir les informations d’identification de compte de stockage hello ».

    ![Boîte de dialogue stockage tooAzure connexion][24]

3. Bonjour **attacher un stockage externe** la boîte de dialogue hello **nom de compte** zone, entrez le nom de compte de stockage hello, spécifiez les autres paramètres de votre choisis, puis sélectionnez **suivant**.

    ![Boîte de dialogue Attacher un stockage externe][8]

4. Bonjour **connexion Résumé** boîte de dialogue, vérifiez les informations de hello. Si vous souhaitez toochange n’est pas défini, sélectionnez **nouveau** et réentrer les paramètres de hello souhaité. 

5. Sélectionnez **Connecter**.

6. Une fois connecté, le compte de stockage externe hello s’affiche avec **(externe)** ajouté toohello nom de compte de stockage.

    ![Résultat de la connexion de compte de stockage externe tooan][9]

### <a name="detach-from-an-external-storage-account"></a>Détachement d’un compte de stockage externe
1. Cliquez sur le compte de stockage externe hello que vous souhaitez toodetach, puis sélectionnez **détachement**.

    ![Option Détacher d’un compte de stockage][10]

2. Dans le message de confirmation hello, sélectionnez **Oui** le détachement de hello tooconfirm à partir du compte de stockage externe hello.

## <a name="attach-a-storage-account-by-using-an-sas"></a>Attachement d’un compte de stockage à l’aide d’une SAP
Un [SAS](storage/common/storage-dotnet-shared-access-signature-part-1.md) admin hello d’un abonnement Azure vous permet d’accorder le compte de stockage d’un accès temporaire tooa sans avoir les informations d’identification de tooprovide abonnement Azure.

tooillustrate ce scénario, nous allons dire que l’UtilisateurA est un administrateur d’un abonnement Azure et l’UtilisateurA veut tooallow UserB tooaccess est un stockage de compte pour une durée limitée avec certaines autorisations :

1. UserA génère un SAS (composé de chaîne de connexion de hello pour le compte de stockage hello) pour une heure spécifique période et avec des autorisations hello souhaité.

2. L’UtilisateurA partages hello SAS hello personne (utilisateur b, dans notre exemple) souhaite que le compte de stockage toohello accès.  

3. UserB utilise l’Explorateur de stockage (version préliminaire) tooattach toohello compte appartenant tooUserA à l’aide de hello fourni SAS.

### <a name="get-an-sas-for-hello-account-you-want-tooshare"></a>Obtenir un SAS pour le compte hello tooshare
1. Dans l’Explorateur de stockage (version préliminaire), cliquez sur le compte de stockage hello vous souhaitez partager, puis sélectionnez **obtenir une Signature d’accès partagé**.

    ![Option de menu contextuel Obtenir une signature d’accès partagé][13]

2. Bonjour **Signature d’accès partagé** boîte de dialogue, spécifiez un intervalle de temps hello et les autorisations que vous souhaitez pour le compte de hello, puis sélectionnez **créer**.

    ![Boîte de dialogue Obtenir une signature d’accès partagé][14]  
    Hello **Signature d’accès partagé** boîte de dialogue s’ouvre et affiche hello SAS.

3. Toohello suivant **chaîne de connexion**, sélectionnez **copie** toocopy il toohello Presse-papiers, puis sélectionnez **fermer**.

### <a name="attach-toohello-shared-account-by-using-hello-sas"></a>Attacher toohello partagé compte à l’aide de hello SAS
1. Dans l’Explorateur de stockage (version préliminaire), sélectionnez **connecter tooAzure**.

    ![Option de stockage tooAzure de connexion][23]

2. Bonjour **connecter tooAzure stockage** boîte de dialogue, spécifiez la chaîne de connexion hello et sélectionnez **suivant**.

    ![Boîte de dialogue stockage tooAzure connexion][24]

3. Bonjour **connexion Résumé** boîte de dialogue, vérifiez les informations de hello. toomake change, sélectionnez **dans**, puis entrez les paramètres hello souhaités. 

4. Sélectionnez **Connecter**.

5. Une fois qu’il est associé, le compte de stockage hello s’affiche avec **(SAS)** ajouté toohello nom du compte que vous avez fournies.

    ![Résultat du compte tooan attaché à l’aide de SAP][17]

## <a name="attach-a-service-by-using-an-sas"></a>Attacher un service à l’aide d’une SAP
section de « Liaison » un compte de stockage à l’aide d’un SAS Hello explique comment un administrateur d’abonnement Azure peut accorder le compte de stockage d’un accès temporaire tooa en générant et en partage un SAS pour le compte de stockage hello. De la même façon, une SAP peut être générée pour un service spécifique (conteneur de blobs, file d’attente ou table) dans un compte de stockage.  

### <a name="generate-an-sas-for-hello-service-that-you-want-tooshare"></a>Générer une SAP pour le service hello que vous souhaitez tooshare
Dans ce contexte, un service peut être un conteneur d’objets blob, une file d’attente ou une table. toogenerate hello SAS pour un service de liste, consultez :

* [Obtenir hello SAS pour un conteneur d’objets blob](vs-azure-tools-storage-explorer-blobs.md#get-the-sas-for-a-blob-container)
* Obtenir hello SAS pour un partage de fichiers : *sera bientôt disponible*
* Obtenir hello SAS pour une file d’attente : *sera bientôt disponible*
* Obtenir hello SAS pour une table : *sera bientôt disponible*

### <a name="attach-toohello-shared-account-service-by-using-hello-sas"></a>Attacher le compte toohello partagé service à l’aide de hello SAS
1. Dans l’Explorateur de stockage (version préliminaire), sélectionnez **connecter tooAzure**.

    ![Option de stockage tooAzure de connexion][23]

2. Bonjour **connecter tooAzure stockage** boîte de dialogue, spécifiez hello URI SAS, puis sélectionnez **suivant**.

    ![Boîte de dialogue stockage tooAzure connexion][24]

3. Bonjour **connexion Résumé** boîte de dialogue, vérifiez les informations de hello. toomake change, sélectionnez **dans**, puis entrez les paramètres hello souhaités. 

4. Sélectionnez **Connecter**.

5. Une fois qu’il est associé, hello service récemment attachée est affiché sous hello **(Service SAP)** nœud.

    ![Résultat de l’attachement tooa partagé service à l’aide d’un SAS][20]

## <a name="search-for-storage-accounts"></a>Recherche de comptes de stockage
Si vous avez une longue liste des comptes de stockage, un toolocate rapidement un compte de stockage spécifique est zone de recherche toouse hello haut hello du volet de gauche hello.

Lorsque vous tapez dans la zone de recherche hello, hello volet gauche affiche les comptes de stockage hello qui correspondent à valeur de recherche hello saisis toothat point. Par exemple, une recherche de tous les comptes de stockage dont le nom contient **tarcher** figure dans hello suivant capture d’écran :

![Recherche de compte de stockage][11]

## <a name="next-steps"></a>Étapes suivantes
* [Gérer les ressources de Stockage Blob Azure avec l’Explorateur de stockage (version préliminaire)](vs-azure-tools-storage-explorer-blobs.md)

[0]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/settings-icon.png
[1]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-account-link.png
[3]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/subscriptions-list.png
[4]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-accounts-list.png
[5]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys.png
[6]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/access-keys-copy.png
[8]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-external-storage-dlg.png
[9]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/external-storage-account.png
[10]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage.png
[11]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/storage-account-search.png
[12]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/detach-external-storage-confirmation.png
[13]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-context-menu.png
[14]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/get-sas-dlg1.png
[15]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/mase.png
[17]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-account-using-sas-finished.png
[20]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/attach-service-using-sas-finished.png
[21]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/local-storage-drop-down.png
[22]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/download-storage-emulator.png
[23]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-icon.png
[24]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/connect-to-azure-storage-next.png
[25]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-certificate-azure-stack.png
[26]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/export-root-cert-azure-stack.png
[27]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/import-azure-stack-cert-storage-explorer.png
[28]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-target-azure-stack.png
[29]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/add-azure-stack-account.png
[30]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/select-accounts-azure-stack.png
[31]: ./media/vs-azure-tools-storage-manage-with-storage-explorer/azure-stack-storage-account-list.png
