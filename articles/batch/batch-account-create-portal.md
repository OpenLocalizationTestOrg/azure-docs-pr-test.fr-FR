---
title: aaaCreate un compte Batch Bonjour portail Azure | Documents Microsoft
description: "Découvrez comment toocreate un traitement par lots Azure compte Bonjour toorun portail Azure, les charges de travail parallèles à grande échelle dans le cloud de hello"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 3fbae545-245f-4c66-aee2-e25d7d5d36db
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2176f88ba0a1a3298023de8f520d46ef28a664b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-portal"></a>Créer un compte de traitement par lots avec hello portail Azure

> [!div class="op_single_selector"]
> * [Portail Azure](batch-account-create-portal.md)
> * [Gestion de lots .NET](batch-management-dotnet.md)
>
>

Découvrez comment toocreate un traitement par lots Azure compte Bonjour [portail Azure][azure_portal], puis choisissez les propriétés de compte hello qui correspondent à votre scénario de calcul. Découvrez où les propriétés du compte important toofind que les clés d’accès et les URL de compte.

Pour plus d’informations sur les comptes de traitement par lots et les scénarios, consultez hello [vue d’ensemble des fonctionnalités](batch-api-basics.md).



## <a name="create-a-batch-account"></a>Création d’un compte Batch

Utiliser toocreate de portail hello un compte Batch de hello deux *les modes d’allocation de pool*: **lot service** mode ou plus récente de hello **abonnement utilisateur** mode, ce qui requiert plus de configuration. Pour plus d’informations sur ces deux modes, consultez hello [vue d’ensemble des fonctionnalités](batch-api-basics.md#account). Pour les fonctionnalités du mode d’abonnement utilisateur hello, voir aussi hello [billet de blog](https://blogs.technet.microsoft.com/windowshpc/2017/03/17/azure-batch-vnet-and-custom-image-support-for-virtual-machine-pools/).

## <a name="batch-service-mode"></a>Mode service Batch



1. Connectez-vous à toohello [portail Azure][azure_portal].
2. Cliquez sur **Nouveau** > **Calcul** > **Service Batch**.

    ![Traitement par lots dans hello Marketplace][marketplace_portal]
3. Hello **compte Batch** panneau s’affiche. Consultez les descriptions de hello ci-dessous de chaque élément du panneau.

    ![Création d’un compte Batch][account_portal]

    a. **Nom du compte**: nom du compte Batch hello vous choisissez doit être unique dans hello région Azure où le compte de hello est créée (voir **emplacement** ci-dessous). nom du compte Hello peut contenir uniquement des caractères en minuscules ou des nombres et doit être de longueur 3 et 24 caractères.

    b. **Abonnement**: hello abonnement dans le hello toocreate compte Batch. Si vous n’avez qu’un seul abonnement, il est sélectionné par défaut.

    c. **Mode d’allocation de pool** : sélectionnez **Service Batch**.

    c. **Groupe de ressources** : sélectionnez un groupe de ressources pour votre nouveau compte Batch (vous pouvez également en créer un).

    d. **Emplacement**: hello région Azure dans le hello toocreate compte Batch. Seules les régions hello pris en charge par votre abonnement et le groupe de ressources sont affichées en tant qu’options.

    e. **Compte de stockage** (facultatif) : compte de stockage Azure à usage général à associer à votre compte Batch. Cela est recommandé pour la plupart des comptes Batch. Pour plus d’informations, consultez la section [Compte Azure Storage lié](#linked-azure-storage-account) disponible plus loin dans cet article.

4. Cliquez sur **créer** compte de hello toocreate.

   portail de Hello indique que le déploiement est en cours d’exécution. Une fois l’opération terminée, la notification **Déploiements réussis** s’affiche dans **Notifications**.

## <a name="user-subscription-mode"></a>Mode Abonnement utilisateur

### <a name="allow-azure-batch-tooaccess-hello-subscription-one-time-operation"></a>Autoriser Azure Batch tooaccess l’abonnement hello (opération à usage unique)
Lorsque vous créez votre premier compte Batch en mode d’abonnement utilisateur, effectuer hello suivant les étapes tooregister votre abonnement avec le lot. (Si vous avez effectué précédemment cette, ignorer toohello la prochaine section.)

1. Connectez-vous à toohello [portail Azure][azure_portal].

2. Cliquez sur **plus Services** > **abonnements**, cliquez sur l’abonnement hello souhaité toouse pour hello compte Batch.

3. Bonjour **abonnement** panneau, cliquez sur **(IAM) de contrôle d’accès** > **ajouter**.

    ![Contrôle d’accès à l’abonnement][subscription_access]

4. Sur hello **ajouter des autorisations** panneau, sélectionnez hello **collaborateur** rôle, recherchez hello API de lot. Recherche de chacune de ces chaînes jusqu'à ce que vous trouviez hello API :
    1. **MicrosoftAzureBatch**.
    2. **Microsoft Azure Batch**. Les locataires Azure AD les plus récents peuvent utiliser ce nom.
    3. **ddbf3205-c6bd-46AE-8127-60eb93363864** ID de hello pour hello API de lot. 

5. Une fois que vous trouvez hello API de lot, sélectionnez-la, puis cliquez sur **enregistrer**.

    ![Ajouter des autorisations Batch][add_permission]

### <a name="create-a-key-vault"></a>Création d’un coffre de clés
Mode d’utilisateur abonnement, un coffre de clés Azure est requis qui appartient toothe même groupe de ressources que hello lot compte toobe est créé. Assurez-vous que le groupe de ressources hello est dans une région où le lot est [disponible](https://azure.microsoft.com/regions/services/) et qui prend en charge de votre abonnement.

1. Bonjour [portail Azure][azure_portal], cliquez sur **nouveau** > **sécurité + identité** > **le coffre de clés** .

2. Bonjour **créer un coffre de clés** panneau, entrez un nom pour le coffre de clés hello et créer un groupe de ressources dans la région de hello souhaité pour votre compte Batch. Laissez hello restant les valeurs par défaut des paramètres, puis cliquez sur **créer**.

### <a name="create-a-batch-account"></a>Création d’un compte Batch

1. Bonjour [portail Azure][azure_portal], cliquez sur **nouveau** > **de calcul** > **le Service Batch**.

    ![Traitement par lots dans hello Marketplace][marketplace_portal]
3. Hello **compte Batch** panneau s’affiche. Consultez les descriptions de hello ci-dessous de chaque élément du panneau.

    ![Création d’un compte Batch][account_portal_byos]

    a. **Nom du compte**: nom du compte Batch hello vous choisissez doit être unique dans hello région Azure où le compte de hello est créée (voir **emplacement** ci-dessous). nom du compte Hello peut contenir uniquement des caractères en minuscules ou des nombres et doit être de longueur 3 et 24 caractères.

    b. **Abonnement**: Si vous avez plusieurs abonnements, sélectionnez l’abonnement hello que vous avez enregistré avec hello service Batch.

    c. **Mode d’allocation de pool** : sélectionnez **Abonnement utilisateur**.

    d. **Coffre de clés**: coffre de clés hello sélectionnez vous avez créé pour votre compte Batch dans la section précédente de hello. Vous pouvez éventuellement créer un coffre de clés. Après avoir sélectionné le coffre de hello, sélectionnez hello case à cocher toogrant Azure Batch accès toohello coffre de clés.

    c. **Groupe de ressources**: groupe de ressources sélectionnez hello dans lequel vous avez créé le coffre de clés hello.

    d. **Emplacement**: hello région Azure dans lequel vous avez créé le coffre de clés hello pour le compte de traitement par lots hello.

    e. **Compte de stockage** (facultatif) : compte de stockage Azure à usage général à associer à votre compte Batch. Cela est recommandé pour la plupart des comptes Batch. Pour plus d’informations, consultez la section [Compte Azure Storage lié](#linked-azure-storage-account) ci-dessous.

4. Cliquez sur **créer** compte de hello toocreate.

   portail de Hello indique que le déploiement est en cours d’exécution. Une fois l’opération terminée, la notification **Déploiements réussis** s’affiche dans **Notifications**.



## <a name="view-batch-account-properties"></a>Afficher les propriétés du compte Batch
Une fois que le compte de hello a été créé, vous pouvez ouvrir hello **Panneau de compte Batch** tooaccess ses paramètres et les propriétés. Vous pouvez accéder tous les paramètres de compte et les propriétés à l’aide du menu de gauche hello du Panneau de compte de traitement par lots hello.

![Panneau de compte Batch dans le portail Azure][account_blade]

* **URL du compte de traitement par lots**: lorsque vous développez une application avec hello [API de lot](batch-apis-tools.md#azure-accounts-for-batch-development), vous aurez besoin de vos ressources de traitement par lots une tooaccess URL de compte. Une URL de compte de traitement par lots a hello suivant le format :

    `https://<account_name>.<region>.batch.azure.com`

![URL de compte Batch dans le portail][account_url]

* **Clés d’accès** (mode de service de lot) : tooauthenticate accès tooyour compte Batch à partir de votre application, vous aurez besoin d’une clé d’accès de compte. (Ce paramètre n’est pas disponible en mode Abonnement utilisateur, dans lequel vous utilisez l’authentification Azure Active Directory.)

    tooview ou régénérer les clés d’accès de votre compte de traitement par lots, entrez `keys` dans le menu de gauche hello **recherche** zone sur le panneau de compte de traitement par lots hello, puis sélectionnez **clés**.

    ![Clés de compte Batch dans le portail Azure][account_keys]

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="linked-azure-storage-account"></a>Compte Azure Storage lié

Vous pouvez éventuellement lier un tooyour de compte de stockage Azure à usage général du compte Batch. Hello [les packages d’applications](batch-application-packages.md) fonctionnalité de traitement par lots utilise le stockage Blob Azure, comme hello [Batch fichier Conventions .NET](batch-task-output.md) bibliothèque. Ces fonctionnalités facultatives vous aideront à déployer des applications hello qui s’exécutent de vos tâches de traitement par lots et conserver les données hello qu'elles produisent.

Nous vous recommandons de créer un compte de stockage dédié à votre compte Batch.

![Créer un compte de stockage à usage général][storage_account]

> [!NOTE]
> Traitement par lots Azure prend actuellement en charge uniquement hello à usage général compte type de stockage. Ce type de compte est décrit à l’étape 5, [Créer un compte de stockage] (../storage/storage-create-storage-account.md#create-a-storage-account), dans [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).
>
>

> [!WARNING]
> Soyez prudent lors de la régénération de clés d’accès hello d’un compte de stockage lié. Régénérer la clé qu’un seul compte de stockage, puis cliquez sur **synchroniser les clés** sur hello liés au panneau de compte de stockage. Attendez cinq minutes tooallow hello clés toopropagate toohello nœuds de calcul dans vos pools, puis régénérer et synchroniser hello autre clé si nécessaire. Si vous régénérez les clés à hello même temps, vos nœuds de calcul ne sera pas en mesure de toosynchronize sur les clés et compte de stockage toohello accès seront perdues.
>
>

![Régénération de clés de compte de stockage][4]

## <a name="batch-service-quotas-and-limits"></a>Quotas et limites du service Batch
Soyez conscient que comme avec votre abonnement Azure et autres Azure services, certains [quotas et limites](batch-quota-limit.md) appliquer tooBatch comptes. Les quotas pour un compte de traitement par lots actuels s’affichent dans le portail hello dans le compte de hello **propriétés**.

![Quotas de compte Batch dans le portail Azure][quotas]



En outre, la plupart de ces quotas peuvent être augmentées simplement avec une demande de support gratuit soumise Bonjour portail Azure. Consultez [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md) pour plus d’informations sur la demande d’augmentation du quota.

## <a name="other-batch-account-management-options"></a>Autres options de gestion de comptes Batch
En outre toousing hello portail Azure, vous pouvez également créer et gérer les comptes de traitement par lots avec les éléments suivants de hello :

* [Applets de commande PowerShell pour Batch](batch-powershell-cmdlets-get-started.md)
* [Interface de ligne de commande Azure](batch-cli-get-started.md)
* [Gestion de lots .NET](batch-management-dotnet.md)

## <a name="next-steps"></a>Étapes suivantes
* Consultez hello [vue d’ensemble de lot](batch-api-basics.md) toolearn plus d’informations sur les fonctionnalités et les concepts du service de traitement par lots. Hello article traite des ressources de traitement principales hello tels que les pools, les nœuds de calcul, les opérations et les tâches et fournit une vue d’ensemble de hello les fonctionnalités du service qui permettent l’exécution de la charge de travail de calcul à grande échelle.
* Principes fondamentaux du développement d’une application activée de lot à l’aide de hello hello [bibliothèque cliente .NET de lot](batch-dotnet-get-started.md) ou [Python](batch-python-tutorial.md). Ces articles d’introduction vous guident dans une application opérationnelle qui utilise hello lot service tooexecute une charge de travail sur plusieurs nœuds de calcul et inclut l’utilisation du stockage Azure pour la récupération et de mise en attente du fichier de charge de travail.

[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx

[azure_portal]: https://portal.azure.com
[batch_pricing]: https://azure.microsoft.com/pricing/details/batch/

[4]: ./media/batch-account-create-portal/batch_acct_04.png "Régénération de clés de compte de stockage"
[marketplace_portal]: ./media/batch-account-create-portal/marketplace_batch.PNG
[account_blade]: ./media/batch-account-create-portal/batch_blade.png
[account_portal]: ./media/batch-account-create-portal/batch_acct_portal.png
[account_keys]: ./media/batch-account-create-portal/account_keys.PNG
[account_url]: ./media/batch-account-create-portal/account_url.png
[storage_account]: ./media/batch-account-create-portal/storage_account.png
[quotas]: ./media/batch-account-create-portal/quotas.png
[subscription_access]: ./media/batch-account-create-portal/subscription_iam.png
[add_permission]: ./media/batch-account-create-portal/add_permission.png
[account_portal_byos]: ./media/batch-account-create-portal/batch_acct_portal_byos.png
