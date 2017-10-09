---
title: aaaEncryption dans Azure Data Lake Store | Documents Microsoft
description: "Comprendre le fonctionnement du chiffrement et de la rotation des clés dans Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: yagupta
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 4/14/2017
ms.author: yagupta
ms.openlocfilehash: a9f3a2dce8232deba93005594d1e6a21e9c0cbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encryption-of-data-in-azure-data-lake-store"></a>Chiffrement des données dans Azure Data Lake Store

Le chiffrement dans Azure Data Lake Store vous permet de protéger vos données, de mettre en œuvre des stratégies de sécurité d’entreprise et de répondre aux exigences de conformité réglementaire. Cet article fournit une vue d’ensemble de la conception de hello et traite des aspects techniques de hello d’implémentation.

Data Lake Store prend en charge le chiffrement des données au repos et en transit. Pour les données au repos, Data Lake Store s’appuie sur un chiffrement transparent « activé par défaut ». Voici, plus en détails, ce que ces termes signifient :

* **Sur par défaut**: lorsque vous créez un nouveau compte Data Lake Store, le paramètre par défaut de hello Active le chiffrement. Par la suite, données qui sont stockées dans Data Lake Store sont toujours chiffrée toostoring préalable sur un support permanent. Il s’agit comportement hello pour toutes les données et il ne peut pas être modifié après la création d’un compte.
* **Transparent**: Data Lake Store chiffre toopersisting préalable des données automatiquement et déchiffre tooretrieval préalable des données. le chiffrement Hello est configuré et géré à hello au niveau de Data Lake Store par un administrateur. Aucune modification n’est apportée toohello données accéder aux API. Aucune modification n’est donc requise dans les applications et services qui interagissent avec Data Lake Store en raison du chiffrement.

Les données en transit (ou données en mouvement) sont également toujours chiffrées dans Data Lake Store. En outre tooencrypting données toostoring préalable toopersistent média, les données de salutation sont également toujours protégées en transit à l’aide de HTTPS. HTTPS est hello seul protocole pris en charge pour hello que REST de magasin de données Lake interfaces. Hello diagramme suivant montre comment les données sont chiffrées dans Data Lake Store :

![Diagramme du chiffrement des données dans Data Lake Store](./media/data-lake-store-encryption/fig1.png)


## <a name="set-up-encryption-with-data-lake-store"></a>Configuration du chiffrement avec Data Lake Store

Le chiffrement pour Data Lake Store est configuré lors de la création de compte et est toujours activé par défaut. Vous pouvez gérer les clés de hello ou autoriser Data Lake Store toomanage pour vous (il s’agit par défaut de hello).

Pour plus d’informations, consultez [Prise en main](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).

## <a name="how-encryption-works-in-data-lake-store"></a>Fonctionnement du chiffrement dans Data Lake Store

Hello informations suivantes couvrent comment les clés de chiffrement principale toomanage et elle explique hello trois différents types de clés que vous pouvez utiliser dans le chiffrement des données pour Data Lake Store.

### <a name="master-encryption-keys"></a>Clés de chiffrement principales

Data Lake Store propose deux modes de gestion des clés de chiffrement principales (MEK). Pour le moment, supposons que cette clé de chiffrement principale hello est la clé de niveau supérieur hello. Clé de chiffrement principale accès toohello est requis toodecrypt toutes les données stockées dans Data Lake Store.

modes de Hello deux pour la gestion de clé de chiffrement principale hello sont les suivantes :

*   Clés gérées par le service
*   Clés gérées par le client

Dans les deux modes, la clé de chiffrement principale hello est sécurisée en les stockant dans Azure Key Vault. Le coffre de clés est un service entièrement géré, hautement sécurisé sur Azure qui peut être des clés de chiffrement toosafeguard utilisé. Pour plus d’informations, consultez [Key Vault](https://azure.microsoft.com/services/key-vault).

Voici une brève comparaison des fonctions fournies par hello deux modes de gestion hello MEKs.

|  | Clés gérées par le service | Clés gérées par le client |
| --- | --- | --- |
|Comment les données sont stockées ?|Toobeing préalable toujours chiffrée stockée.|Toobeing préalable toujours chiffrée stockée.|
|Où est stockée les hello clé de chiffrement principale ?|Key Vault|Key Vault|
|Sont toutes les clés stockées dans hello désactivez le chiffrement en dehors du coffre de clés ? |Non|Non|
|Hello MEK peut être récupérée par le coffre de clés ?|Non. Après avoir hello que MEK est stocké dans le coffre de clés, il peut être utilisé uniquement pour le chiffrement et le déchiffrement.|Non. Après avoir hello que MEK est stocké dans le coffre de clés, il peut être utilisé uniquement pour le chiffrement et le déchiffrement.|
|Qui est propriétaire d’instance de coffre de clés hello et hello MEK ?|Hello les service Data Lake Store|Vous êtes propriétaire d’instance de coffre de clés hello, qui appartienne à votre propre abonnement Azure. Hello MEK dans le coffre de clés peut être géré par un logiciel ou matériel.|
|Vous pouvez révoquer l’accès toohello MEK pourquoi les service Data Lake Store ?|Non|Oui. Vous pouvez gérer des listes de contrôle d’accès dans le coffre de clés et supprimer l’identité du service accès contrôle entrées toohello pourquoi les service Data Lake Store.|
|Peut supprimer définitivement hello MEK ?|Non|Oui. Si vous supprimez hello MEK de coffre de clés, ne peut pas déchiffrer les données de hello Bonjour compte Data Lake Store par tout le monde, y compris hello Data Lake Store service. <br><br> Si vous avez explicitement sauvegardé toodeleting préalable de MEK hello il à partir du coffre de clés, hello MEK peut être restaurée et les données de salutation peuvent ensuite être récupérées. Toutefois, si vous n'avez pas sauvegardé toodeleting préalable de hello MEK il à partir du coffre de clés, données hello Bonjour compte Data Lake Store peuvent jamais être déchiffrées par la suite.|


À part cette différence de qui gère les hello MEK et instance coffre de clés hello dans lequel il réside, reste hello de conception de hello est hello même pour les deux modes.

Il est suivant de hello tooremember important lorsque vous choisissez mode hello hello pour les clés de chiffrement principale :

*   Vous pouvez choisir si toouse client géré clés ou les clés de service géré lorsque vous configurez un compte Data Lake Store.
*   Une fois configuré, un compte Data Lake Store ne peuvent pas modifier le mode de hello.

### <a name="encryption-and-decryption-of-data"></a>Chiffrement et déchiffrement des données

Il existe trois types de clés qui sont utilisées dans la conception de hello du chiffrement des données. Hello tableau suivant fournit un résumé :

| Clé                   | Abréviation | Associée à | Emplacement de stockage                             | Type       | Remarques                                                                                                   |
|-----------------------|--------------|-----------------|----------------------------------------------|------------|---------------------------------------------------------------------------------------------------------|
| Clé de chiffrement principale | MEK          | Compte Data Lake Store | Key Vault                              | Asymétrique | Peut être gérée par Data Lake Store ou par vous.                                                              |
| Clé de chiffrement des données   | DEK          | Compte Data Lake Store | Stockage permanent, géré par le service Data Lake Store | Symétrique  | Hello DEK est chiffré par hello MEK. Hello que DEK chiffré est ce qui est stocké sur un support permanent. |
| Clé de chiffrement de bloc  | BEK          | Un bloc de données | Aucun                                         | Symétrique  | Hello BEK est dérivée de hello DEK et bloc de données hello.                                                      |

Hello suivant le diagramme illustre ces concepts :

![Clés dans le chiffrement des données](./media/data-lake-store-encryption/fig2.png)

#### <a name="pseudo-algorithm-when-a-file-is-toobe-decrypted"></a>Algorithme de pseudo lorsqu’un fichier est toobe déchiffré :
1.  Vérifiez si hello DEK compte Data Lake Store de hello est mis en cache et prête pour utilisation.
    - Si ce n’est pas le cas, lire hello chiffré DEK à partir d’un stockage persistant et envoyez-le toobe de coffre tooKey déchiffré. Hello du cache déchiffrer la clé DEK en mémoire. Il est maintenant prêt toouse.
2.  Pour chaque bloc de données dans le fichier de hello :
    - Lecture hello chiffrée du bloc de données à partir d’un stockage persistant.
    - Générer hello BEK de hello DEK et bloc de chiffrées hello de données.
    - Utiliser des données de toodecrypt BEK hello.


#### <a name="pseudo-algorithm-when-a-block-of-data-is-toobe-encrypted"></a>Algorithme de pseudo lorsqu’un bloc de données est toobe chiffrée :
1.  Vérifiez si hello DEK compte Data Lake Store de hello est mis en cache et prête pour utilisation.
    - Si ce n’est pas le cas, lire hello chiffré DEK à partir d’un stockage persistant et envoyez-le toobe de coffre tooKey déchiffré. Hello du cache déchiffrer la clé DEK en mémoire. Il est maintenant prêt toouse.
2.  Générer un BEK unique pour le bloc hello de données à partir de hello DEK.
3.  Chiffrer le bloc de données hello avec hello BEK, à l’aide du chiffrement AES-256.
4.  Bloc de données chiffrées magasin hello des données sur le stockage persistant.

> [!NOTE] 
> Pour des raisons de performances, hello DEK Bonjour effacer est mis en cache en mémoire pendant une courte période et est effacé immédiatement après. Sur un support persistant, il est toujours chiffrée par hello MEK.

## <a name="key-rotation"></a>Rotation des clés

Lorsque vous utilisez des clés de gérée par le client, vous pouvez faire pivoter hello MEK. toolearn tooset d’un compte Data Lake Store avec des clés gérée par le client, voir [mise en route](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).

### <a name="prerequisites"></a>Composants requis

Lorsque vous configurez hello compte Data Lake Store, vous avez choisi toouse vos propres clés. Cette option ne peut pas être modifiée une fois hello compte a été créé. Hello étapes suivantes supposent que vous utilisez des clés de gérée par le client (autrement dit, vous avez choisi vos propres clés de coffre de clés).

Notez que si vous utilisez les options par défaut de hello pour le chiffrement, vos données sont toujours chiffrées à l’aide de clés gérés par Data Lake Store. Dans cette option, vous n’avez les clés de capacité toorotate hello, qu’ils sont gérés par Data Lake Store.

### <a name="how-toorotate-hello-mek-in-data-lake-store"></a>Comment toorotate hello MEK dans Data Lake Store

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Parcourir l’instance de coffre de clés toohello qui stocke vos clés associés à votre compte Data Lake Store. Sélectionnez **Clés**.

    ![Capture d’écran de Key Vault](./media/data-lake-store-encryption/keyvault.png)

3.  Sélectionnez la clé hello associée à votre compte Data Lake Store et créer une nouvelle version de cette clé. Notez que Data Lake Store actuellement prend uniquement en charge la rotation des clés tooa nouvelle version d’une clé. Il ne prend en charge la rotation tooa autre clé.

   ![Capture d’écran de la fenêtre Clés, avec Nouvelle version en surbrillance](./media/data-lake-store-encryption/keynewversion.png)

4.  Recherchez le compte de stockage toohello Data Lake Store, puis sélectionnez **chiffrement**.

    ![Capture d’écran de la fenêtre du compte de stockage Data Lake Store, avec Chiffrement en surbrillance](./media/data-lake-store-encryption/select-encryption.png)

5.  Un message vous avertit qu’une nouvelle version de clé de la clé de hello est disponible. Cliquez sur **pivoter une clé** nouvelle version tooupdate hello toohello clé.

    ![Capture d’écran de la fenêtre Data Lake Store avec le message et Rotation de clé en surbrillance](./media/data-lake-store-encryption/rotatekey.png)

Cette opération doit prendre moins de deux minutes, et il n’existe aucun temps d’indisponibilité attendu en raison de la rotation de tookey. Une fois hello terminée, hello nouvelle version de clé de hello est en cours d’utilisation.
