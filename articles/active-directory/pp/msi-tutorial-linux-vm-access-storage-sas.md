---
title: "Utiliser une MSI de machine virtuelle Linux pour accéder à Stockage Azure en utilisant des informations d’identification SAP"
description: "Didacticiel montrant comment utiliser une MSI (Managed Service Identity) de machine virtuelle Linux pour accéder à Stockage Azure en utilisant des informations d’identification SAP au lieu d’une clé d’accès au compte de stockage."
services: active-directory
documentationcenter: 
author: BryanLa
manager: mbaldwin
editor: bryanla
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/15/2017
ms.author: bryanla
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: f947d1c0a26a92e6ec179b82ca5015df5e45a634
ms.sourcegitcommit: a648f9d7a502bfbab4cd89c9e25aa03d1a0c412b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="use-a-linux-vm-managed-service-identity-to-access-azure-storage-via-a-sas-credential"></a>Utiliser une MSI (Managed Service Identity) de machine virtuelle Linux pour accéder à Stockage Azure à l’aide d’informations d’identification SAP

[!INCLUDE[preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

Ce didacticiel montre comment activer MSI pour une machine virtuelle Linux, puis utiliser la MSI pour obtenir des informations d’identification SAP (Signature d’Accès Partagé) de stockage. Plus précisément, des [informations d’identification SAP de service](~/articles/storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json#types-of-shared-access-signatures). 

Une SAP de service offre la possibilité d’accorder un accès limité à des objets dans un compte de stockage, pendant une durée limitée et pour un service spécifique (en l’occurrence, le service BLOB), sans exposer de clé d’accès de compte. Vous pouvez utiliser des informations d’identification SAP comme d’habitude lors de l’exécution d’opérations de stockage, par exemple, lors de l’utilisation du SDK Stockage Azure. Ce didacticiel montre le chargement et le téléchargement d’un objet blob à l’aide de l’interface de ligne de commande de Stockage Azure. Vous apprendrez à :


> [!div class="checklist"]
> * Activer l’identité du service administré sur une machine virtuelle Linux 
> * Autoriser votre machine virtuelle à accéder à la SAP d’un compte stockage dans le Gestionnaire des ressources 
> * Obtenir un jeton d’accès à l’aide de l’identité de votre machine virtuelle et l’utiliser pour récupérer la SAP à partir du Gestionnaire des ressources 

## <a name="prerequisites"></a>configuration requise

[!INCLUDE [msi-core-prereqs](~/includes/active-directory-msi-core-prereqs-ua.md)]

[!INCLUDE [msi-tut-prereqs](~/includes/active-directory-msi-tut-prereqs.md)]

## <a name="sign-in-to-azure"></a>Connexion à Azure
Connectez-vous au portail Azure depuis l’adresse [https://portal.azure.com](https://portal.azure.com).


## <a name="create-a-linux-virtual-machine-in-a-new-resource-group"></a>Créer une machine virtuelle Linux dans un nouveau groupe de ressources

Pour ce didacticiel, nous créons une machine virtuelle Linux. Vous pouvez également activer l’identité du service administré sur une machine virtuelle existante.

1. Cliquez sur le bouton **+/Créer un service** dans l’angle supérieur gauche du portail Azure.
2. Sélectionnez **Compute**, puis sélectionnez **Ubuntu Server 16.04 LTS**.
3. Saisissez les informations de la machine virtuelle. Dans **Type d’authentification**, sélectionnez **Clé publique SSH** ou **Mot de passe**. Les informations d’identification créées vous permettent de vous connecter à la machine virtuelle.

    ![Texte de remplacement d’image](~/articles/active-directory/media/msi-tutorial-linux-vm-access-arm/msi-linux-vm.png)

4. Choisissez un **Abonnement** pour la machine virtuelle dans la liste déroulante.
5. Pour sélectionner un nouveau **Groupe de ressources** dans lequel vous souhaitez créer la machine virtuelle, choisissez **Créer nouveau**. Lorsque vous avez terminé, cliquez sur **OK**.
6. Choisissez la taille de la machine virtuelle. Pour voir plus de tailles, sélectionnez **Afficher tout** ou modifiez le filtre de type de disque pris en charge. Conservez les valeurs par défaut dans le panneau des paramètres et cliquez sur **OK**.

## <a name="enable-msi-on-your-vm"></a>Activer l’identité du service administré sur votre machine virtuelle

L’identité du service administré d’une machine virtuelle permet d’obtenir des jetons d’accès d’Azure AD sans avoir à placer des informations d’identification dans votre code. En arrière-plan, l’activation de l’identité du service administré entraîne deux actions : elle installe l’extension de l’identité du service administré de la machine virtuelle et active l’identité du service administré pour la machine virtuelle.  

1. Accédez au groupe de ressources de votre nouvelle machine virtuelle et sélectionnez la machine virtuelle que vous avez créée à l’étape précédente.
2. Dans les paramètres de la machine virtuelle situés sur la gauche, cliquez sur **Configuration**.
3. Pour enregistrer et activer l’identité du service administré, sélectionnez **Oui**. Si vous souhaitez la désactiver, sélectionnez Non.
4. Assurez-vous d’avoir cliqué sur **Enregistrer** pour enregistrer la configuration.

    ![Texte de remplacement d’image](~/articles/active-directory/media/msi-tutorial-linux-vm-access-arm/msi-linux-extension.png)

5. Si vous souhaitez vérifier les extensions présentes sur la machine virtuelle, cliquez sur **Extensions**. Si l’identité du service administré est activée, **ManagedIdentityExtensionforLinux** apparaît dans la liste.

    ![Texte de remplacement d’image](~/articles/active-directory/media/msi-tutorial-linux-vm-access-arm/msi-extension-value.png)

## <a name="create-a-storage-account"></a>Créez un compte de stockage. 

Si vous n’en avez pas déjà un, vous allez maintenant créer un compte de stockage.  Vous pouvez également ignorer cette étape et accorder l’accès MSI de votre machine virtuelle aux clés d’un compte de stockage existant. 

1. Cliquez sur le bouton **+/Créer un service** dans l’angle supérieur gauche du portail Azure.
2. Cliquez sur **Stockage**, puis **Compte de stockage**, et un nouveau panneau « Créer un compte de stockage » s’affiche.
3. Saisissez un **nom** pour le compte de stockage, vous l’utiliserez ultérieurement.  
4. **Modèle de déploiement** et **Type de compte** doivent être respectivement définis sur « Gestionnaire de ressources » et « Usage général ». 
5. Assurez-vous que les champs **Abonnement** et **Groupe de ressources** correspondent à ceux que vous avez spécifiés lorsque vous avez créé votre machine virtuelle à l’étape précédente.
6. Cliquez sur **Créer**.

    ![Créer un nouveau compte de stockage](~/articles/active-directory/media/msi-tutorial-linux-vm-access-storage/msi-storage-create.png)

## <a name="create-a-blob-container-in-the-storage-account"></a>Création d’un conteneur d’objets blob dans le compte de stockage

Plus tard, nous chargerons et téléchargerons un fichier vers le nouveau compte de stockage. Étant donné que les fichiers nécessitent un stockage d’objets blob, nous devons créer un conteneur d’objets blob dans lequel stocker le fichier.

1. Revenez à votre compte de stockage nouvellement créé.
2. Cliquez sur le lien **Conteneurs** dans le panneau de gauche, sous « Service BLOB ».
3. Cliquez sur **+ Conteneur** en haut de la page et un panneau « Nouveau conteneur » apparait.
4. Nommez le conteneur, sélectionnez un niveau d’accès, puis cliquez sur **OK**. Le nom spécifié sera utilisé plus loin dans le didacticiel. 

    ![Créer un conteneur de stockage](~/articles/active-directory/media/msi-tutorial-linux-vm-access-storage/create-blob-container.png)

## <a name="grant-your-vms-msi-access-to-use-a-storage-sas"></a>Accorder à la MSI de votre machine virtuelle l’accès pour utiliser une SAP de stockage 

Le stockage Azure ne prend pas en charge l’authentification Azure AD en mode natif.  Toutefois, vous pouvez utiliser une MSI pour récupérer une SAP de stockage à partir du Gestionnaire de ressources, puis utiliser cette SAP pour accéder au stockage.  Dans cette étape, vous accordez à votre MSI de machine virtuelle l’accès à votre SAP de compte de stockage.   

1. Revenez au compte de stockage que vous venez de créer.   
2. Cliquez sur le lien **(IAM) de contrôle d’accès** dans le panneau de gauche.  
3. Cliquez sur **+ Ajouter** en haut de la page pour ajouter une nouvelle attribution de rôle pour votre machine virtuelle.
4. Définissez **Rôle** sur « Contributeur de comptes de stockage » sur le côté droit de la page. 
5. Dans la liste déroulante suivante, définissez **Attribuer l’accès à** sur la ressource « Machine virtuelle ».  
6. Ensuite, assurez-vous que l’abonnement approprié est répertorié dans la liste déroulante **Abonnement**, puis définissez **Groupe de ressources** sur « Tous les groupes de ressources ».  
7. Enfin, sous **Sélectionner**, choisissez votre machine virtuelle Linux dans la liste déroulante, puis cliquez sur **Enregistrer**.  

    ![Texte de remplacement d’image](~/articles/active-directory/media/msi-tutorial-linux-vm-access-storage/msi-storage-role-sas.png)

## <a name="get-an-access-token-using-the-vms-identity-and-use-it-to-call-azure-resource-manager"></a>Obtenir un jeton d’accès à l’aide de l’identité de la machine virtuelle et l’utiliser pour appeler Azure Resource Manager

Pour la suite de ce didacticiel, nous allons utiliser la machine virtuelle que nous avons créée précédemment.

Pour effectuer cette procédure, vous avez besoin d'un client SSH. Si vous utilisez Windows, vous pouvez utiliser le client SSH dans le [Sous-système Windows pour Linux](https://msdn.microsoft.com/commandline/wsl/install_guide). Si vous avez besoin d’aide pour configurer les clés de votre client SSH, consultez [Comment utiliser les clés SSH avec Windows sur Azure](~/articles/virtual-machines/linux/ssh-from-windows.md), ou [Comment créer et utiliser une paire de clés publique et privée SSH pour les machines virtuelles Linux dans Azure](~/articles/virtual-machines/linux/mac-create-ssh-keys.md).

1. Dans le portail Azure, accédez à **Machines virtuelles**, accédez à votre machine virtuelle Linux, puis, en haut de la page **Vue d’ensemble**, cliquez sur **Se connecter**. Copiez la chaîne permettant de se connecter à votre machine virtuelle. 
2. Connectez-vous à votre machine virtuelle en utilisant votre client SSH.  
3. Ensuite, vous serez invité à entrer le **Mot de passe** que vous avez ajouté à la création de la **machine virtuelle Linux**. Vous devez être connecté.  
4. Utilisez CURL pour obtenir un jeton d’accès à partir de Azure Resource Manager.  

    La requête et la réponse CURL pour le jeton d’accès se trouvent ci-dessous :
    
    ```bash
    curl http://localhost:50342/oauth2/token --data "resource=https://management.azure.com/" -H Metadata:true    
    ```
    
    > [!NOTE]
    > Dans la requête précédente, la valeur du paramètre « resource » doit correspondre exactement à ce qu’Azure AD attend. Lorsque vous utilisez l’ID de ressource Azure Resource Manager, vous devez inclure la barre oblique de fin à l’URI.
    > Dans la réponse suivante, l’élément access_token a été raccourci par souci de concision.
    
    ```bash
    {"access_token":"eyJ0eXAiOiJ...",
    "refresh_token":"",
    "expires_in":"3599",
    "expires_on":"1504130527",
    "not_before":"1504126627",
    "resource":"https://management.azure.com",
    "token_type":"Bearer"} 
     ```

## <a name="get-a-sas-credential-from-azure-resource-manager-to-make-storage-calls"></a>Obtenir des informations d’identification SAP d’Azure Resource Manager pour effectuer des appels de stockage

À présent, utilisez CURL pour appeler le Gestionnaire des ressources à l’aide du jeton d’accès récupéré dans la section précédente, afin de créer des informations d’identification SAP. Une fois les informations d’identification SAP récupérées, nous pouvons appeler des opérations de chargement/téléchargement de stockage.

Pour cette demande, nous allons utiliser les paramètres de requête HTTP suivants pour créer les informations d’identification SAP :

```JSON
{
    "canonicalizedResource":"/blob/<STORAGE ACCOUNT NAME>/<CONTAINER NAME>",
    "signedResource":"c",              // The kind of resource accessible with the SAS, in this case a container (c).
    "signedPermission":"rcw",          // Permissions for this SAS, in this case (r)ead, (c)reate, and (w)rite.  Order is important.
    "signedProtocol":"https",          // Require the SAS be used on https protocol.
    "signedExpiry":"<EXPIRATION TIME>" // UTC expiration time for SAS in ISO 8601 format, for example 2017-09-22T00:06:00Z.
}
```

Ces paramètres sont inclus dans le corps POST de la requête pour les informations d’identification SAP. Pour plus d’informations concernant les paramètres pour la création d’informations d’identification SAP, voir [Afficher la référence REST de SAP de service](/rest/api/storagerp/storageaccounts/listservicesas).

Utilisez la demande CURL suivante pour obtenir les informations d’identification SAP. N’oubliez pas de remplacer les valeurs des paramètres `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>`, `<STORAGE ACCOUNT NAME>`, `<CONTAINER NAME>` et `<EXPIRATION TIME>` par vos propres valeurs. Remplacez la valeur de `<ACCESS TOKEN>` par le jeton d’accès que vous avez récupéré précédemment :

```bash 
curl https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Storage/storageAccounts/<STORAGE ACCOUNT NAME>/listServiceSas/?api-version=2017-06-01 -X POST -d "{\"canonicalizedResource\":\"/blob/<STORAGE ACCOUNT NAME>/<CONTAINER NAME>\",\"signedResource\":\"c\",\"signedPermission\":\"rcw\",\"signedProtocol\":\"https\",\"signedExpiry\":\"<EXPIRATION TIME>\"}" -H "Authorization: Bearer <ACCESS TOKEN>"
```

> [!NOTE]
> Le texte de l’URL précédente respectant la casse, veillez à respecter les majuscules et les minuscules pour vos groupes de ressources. En outre, il est important de savoir qu’il s’agit d’une demande POST et non d’une demande GET.

La réponse CURL retourne les informations d’identification SAP :  

```bash 
{"serviceSasToken":"sv=2015-04-05&sr=c&spr=https&st=2017-09-22T00%3A10%3A00Z&se=2017-09-22T02%3A00%3A00Z&sp=rcw&sig=QcVwljccgWcNMbe9roAJbD8J5oEkYoq%2F0cUPlgriBn0%3D"} 
```

Créez un exemple de fichier blob à charger dans votre conteneur de stockage d’objets blob. Ceci peut se faire sur une machine virtuelle Linux avec la commande suivante : 

```bash
echo "This is a test file." > test.txt
```

Ensuite, authentifiez-vous à l’aide de la commande `az storage` de l’interface de ligne de commande en utilisant les informations d’identification SAP, puis chargez le fichier dans le conteneur d’objets blob. Pour cette étape, vous devez [installer la dernière version d’Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) sur votre machine virtuelle, si ce n’est déjà fait.

```azurecli-interactive
 az storage blob upload --container-name 
                        --file 
                        --name
                        --account-name 
                        --sas-token
```

Réponse : 

```JSON
Finished[#############################################################]  100.0000%
{
  "etag": "\"0x8D4F9929765C139\"",
  "lastModified": "2017-09-21T03:58:56+00:00"
}
```

Vous pouvez également télécharger le fichier à l’aide d’Azure CLI et vous authentifier avec les informations d’identification SAP. 

Demande : 

```azurecli-interactive
az storage blob download --container-name
                         --file 
                         --name 
                         --account-name
                         --sas-token
```

Réponse : 

```JSON
{
  "content": null,
  "metadata": {},
  "name": "testblob",
  "properties": {
    "appendBlobCommittedBlockCount": null,
    "blobType": "BlockBlob",
    "contentLength": 16,
    "contentRange": "bytes 0-15/16",
    "contentSettings": {
      "cacheControl": null,
      "contentDisposition": null,
      "contentEncoding": null,
      "contentLanguage": null,
      "contentMd5": "Aryr///Rb+D8JQ8IytleDA==",
      "contentType": "text/plain"
    },
    "copy": {
      "completionTime": null,
      "id": null,
      "progress": null,
      "source": null,
      "status": null,
      "statusDescription": null
    },
    "etag": "\"0x8D4F9929765C139\"",
    "lastModified": "2017-09-21T03:58:56+00:00",
    "lease": {
      "duration": null,
      "state": "available",
      "status": "unlocked"
    },
    "pageBlobSequenceNumber": null,
    "serverEncrypted": false
  },
  "snapshot": null
}
```

## <a name="next-steps"></a>étapes suivantes

- Pour une vue d’ensemble de l’identité du service administré, consultez [Vue d’ensemble de l’identité du service administré](msi-overview.md).
- Pour savoir comment suivre ce didacticiel en utilisant une clé de compte de stockage, voir [Utiliser une MSI de machine virtuelle Linux pour accéder à Stockage Azure](msi-tutorial-linux-vm-access-storage.md).
- Pour plus d’informations sur la fonctionnalité de SAP de compte de Stockage Azure, voir :
  - [Utilisation des signatures d’accès partagé (SAP)](~/articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)
  - [Construction d’un service SAP](/rest/api/storageservices/Constructing-a-Service-SAS.md)

Utilisez la section Commentaires suivante pour donner votre avis et nous aider à affiner et à mettre en forme notre contenu.
