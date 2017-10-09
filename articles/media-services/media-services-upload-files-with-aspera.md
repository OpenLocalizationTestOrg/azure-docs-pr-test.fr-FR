---
title: "fichiers aaaUpload à un compte Azure Media Services à l’aide de Aspera | Documents Microsoft"
description: "Ce didacticiel vous guide tout au long des étapes hello du téléchargement des fichiers dans un compte de stockage qui est associé à un compte de service de média à l’aide de hello ** Aspera Server sur la demande ** le service sur Azure."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a>Télécharger des fichiers dans un compte Media Services à l’aide de hello Aspera Server On Demand service sur Azure

## <a name="overview"></a>Vue d'ensemble

**Aspera** est un logiciel de transfert de fichiers à haut débit. Le service **Aspera Server On Demand** pour Azure permet de charger et télécharger rapidement des fichiers volumineux directement dans un espace de stockage d’objets blob Azure. Pour plus d’informations sur **Aspera On Demand**, consultez hello [Aspera Cloud](http://cloud.asperasoft.com/) site. 
  
**Serveur de Aspera On Demand** pour Azure est disponible à l’achat de hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/). Dans commande toocomplete un achat de **Aspera Server On Demand** pour Azure, veuillez vous connecter à Azure Marketplace avec votre Windows Live ID.

Ce didacticiel vous guide tout au long des étapes hello du téléchargement des fichiers dans un compte de stockage qui est associé à un compte de service de média à l’aide de hello **Aspera Server On Demand** service sur Azure. 

Vous trouverez un exemple qui montre comment toouse Azure fonctionne avec Aspera et Media Services [ici](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).

>[!NOTE]
>Il existe une limite toohello taille maximale prise en charge pour le traitement des processeurs de support (PA) avec Azure Media Services. Consultez [cela](media-services-quotas-and-limitations.md) pour plus d’informations sur la limite de taille de fichier hello.
>

## <a name="prerequisites"></a>Composants requis 

toocomplete ce didacticiel, vous devez :

* Un identifiant Windows Live.
* Un [compte Azure](https://azure.microsoft.com). Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/). 
* Un [compte Azure Media Services](media-services-portal-create-account.md).

## <a name="purchase-aspera-on-demand-for-azure"></a>Acheter Aspera On Demand pour Azure

Une fois que vous êtes connecté à Azure Marketplace, suivez ces étapes de base de toocomplete votre achat de Aspera On Demand pour Azure.

1. Recherchez Aspera et sélectionnez « Server On Demand ».

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. Passez en revue les plans d’abonnement hello et cliquez sur « S’inscrire »

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. Renseignez les spécificités de hello pour votre serveur d’abonnement de la demande.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. Cliquez sur hello **niveau tarifaire** et sélectionnez votre volume mensuel souhaité dans le panneau de configuration hello sub. Bonjour **détails du Plan** Panneau de configuration, sélectionnez **OK**. Ensuite, dans hello **Choisissez votre niveau tarifaire** du panneau, cliquez sur **sélectionnez**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. Cliquez sur **juridiques** tooview et acceptez les conditions juridiques de hello dans Panneau de configuration hello sub. Une fois que vous avez consulté les conditions juridiques hello, cliquez sur **bon**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. Terminer l’achat de hello en cliquant sur **créer**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. annonce Hello du tableau de bord Azure approvisionne les service hello.  Une fois qu’il est terminé avec l’allocation, vous trouverez un nouvel abonnement hello en effectuant une recherche dans les ressources nom hello du service de hello. Lorsque vous avez trouvé le service hello, double-cliquez sur portail de gestion du service toolaunch hello.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. Lancez le portail de gestion Aspera hello. Une fois que vous avez trouvé votre nouveau service Aspera, vous pouvez obtenir le portail de gestion toohello accès, en cliquant sur le service de hello.  Un nouveau panneau s’ouvre. Dans ce nouveau panneau de configuration, vous devez tooclick sur hello **nom de la ressource** de votre nouveau service.  Bonjour suivant capture d’écran, le nom de ressource de hello est 'AsperaTransferDemo'. Une fois que vous cliquez sur le nom de la ressource hello, un autre panneau est lancé. Ce panneau contient un lien « Gérer ». Cliquez sur hello le portail de gestion Aspera 'Gérer' lien toolaunch hello.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. En cliquant sur hello lien gérer, vous obtiendrez une page d’inscription toohello, ce qui est nécessaire tooaccess hello service.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. À ce stade, vous aurez accès toohello Aspera portail de gestion, où vous pouvez créer des touches d’accès rapide, téléchargez Aspera clients et les licences, afficher l’utilisation et en savoir plus sur les API de hello.

    Hello capture d’écran suivante montre la création de l’accès hello. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    Hello capture d’écran suivante montre l’utilisation de hello reporting interfaces dans le portail de hello. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a>Chargement de fichiers avec Aspera

1. Téléchargez et installez le logiciel client hello Aspera :
    
    * [Plug-in de navigateur](http://downloads.asperasoft.com/connect2/)
    * [Client enrichi](http://downloads.asperasoft.com/en/downloads/2)

2. Effectuez votre premier transfert. Dans l’ordre toouse hello Aspera client tootransfer avec le service de transfert Aspera de hello, vous toocomplete hello éléments suivants sont nécessaires : 

    1. Créer une clé d’accès, à l’aide du portail de Aspera hello.  
    2. Téléchargement et installation client de licence hello Aspera (logiciel sont accessibles dans le portail de Aspera hello).  

    >[!NOTE]
    >Lisez le guide du client hello Aspera des informations de configuration.
    
    3. Récupérer des informations de votre compte de stockage qui est associé à votre compte de média Azure à l’aide de hello [portail Azure](https://portal.azure.com/). Plus précisément, nom et la clé et nom de conteneur stockage hello dans toowhich vous souhaitez tooplace votre contenu. 

        * informations de stockage hello tooget à partir du portail de hello : recherchez votre compte de stockage, cliquez sur les touches d’accès hello et copier hello hello et nom de la clé de votre compte.
        * nom du conteneur tooget hello : recherchez votre compte de stockage, sélectionnez **BLOB**, sélectionnez nom hello de conteneur hello contenu tooupload hello. 

    Voici la capture d’écran de hello du client de Aspera hello **Gestionnaire de connexions** où vous devez spécifier le type de stockage 'Azure' hello et informations d’identification ainsi que de conteneur d’objets blob hello.

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a>Ressources

Hello suivant des ressources ont été mentionné dans cet article. 

* [Plug-in de connexion de navigateur](http://downloads.asperasoft.com/connect2/)
* [Guide de connexion](http://downloads.asperasoft.com/en/documentation/8)
* [Client Aspera](http://downloads.asperasoft.com/en/downloads/2)
* [Guide client](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez désormais [copier des objets blob d’un compte de stockage dans un compte AMS](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).

## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

