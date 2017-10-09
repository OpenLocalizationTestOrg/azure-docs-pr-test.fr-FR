---
title: "rôles de hello aaaConfigure pour Azure cloud service avec Visual Studio | Documents Microsoft"
description: "Découvrez comment tooset installer et configurer des rôles pour les services de cloud computing Azure à l’aide de Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: d3c62eb57040ebe987787e73b17b468bb82122bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a>Configurer des rôles de service cloud Azure avec Visual Studio
Un service cloud Azure peut avoir un ou plusieurs rôles de travail ou rôles web. Pour chaque rôle, vous devez toodefine comment configurer ce rôle et également configurez la façon dont ce rôle s’exécute. toolearn savoir plus sur les rôles dans les services de cloud computing, consultez la vidéo de hello [tooAzure de présentation des Services de cloud computing](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services). 

informations de Hello pour votre service cloud sont stockées dans hello fichiers suivants :

- **ServiceDefinition.csdef** -fichier de définition de service hello définit les paramètres d’exécution de hello pour votre service cloud dont les rôles requis, points de terminaison et taille de machine virtuelle. Aucune des données hello stockées dans `ServiceDefinition.csdef` peut être modifiée lorsque votre rôle est en cours d’exécution.
- **ServiceConfiguration.cscfg** - fichier de configuration de service hello configure le nombre d’instances d’un rôle est exécuté et les valeurs des paramètres de hello hello définis pour un rôle. Hello des données stockées dans `ServiceConfiguration.cscfg` peut être modifié pendant l’exécution de votre rôle.

toostore différentes valeurs pour les paramètres de hello, qui contrôle comment un rôle s’exécute, vous pouvez définir plusieurs configurations de service. Vous pouvez utiliser une configuration de service différente pour chaque environnement de déploiement. Par exemple, vous pouvez définir votre compte connexion chaîne toouse hello local de stockage Azure l’émulateur de stockage dans une configuration de service local et créer un autre service de configuration toouse le stockage Azure dans le cloud de hello.

Lorsque vous créez un service cloud Azure dans Visual Studio, deux configurations de service sont automatiquement créées et ajoutés tooyour projet Windows Azure :

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a>Configurer un service cloud Azure
Vous pouvez configurer un service cloud Azure à partir de l’Explorateur de solutions dans Visual Studio, comme indiqué dans hello comme suit :

1. Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.

1. Dans **l’Explorateur de solutions**, cliquez sur le projet de hello et, dans le menu contextuel de hello, sélectionnez **propriétés**.
   
    ![Menu contextuel de projet dans l’Explorateur de solutions](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. Dans la page de propriétés du projet hello, sélectionnez hello **développement** onglet. 

    ![Page de propriétés du projet : onglet développement](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. Bonjour **Configuration du Service** liste, le nom hello select de configuration du service que vous souhaitez tooedit hello. (Si vous souhaitez toomake modifie les configurations de service tooall hello pour ce rôle, sélectionnez **toutes les Configurations**.)
   
    > [!IMPORTANT]
    > Si vous choisissez une configuration de service spécifique, certaines propriétés sont désactivées parce qu’elles peuvent être définies uniquement pour toutes les configurations. tooedit ces propriétés, vous devez sélectionner **toutes les Configurations**.
    > 
    > 
   
    ![Liste Configuration du service pour un service cloud Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-hello-number-of-role-instances"></a>Modifier le nombre hello d’instances de rôle
performances de hello tooimprove de votre service cloud, vous pouvez modifier le nombre hello d’instances d’un rôle qui sont en cours d’exécution, en fonction du nombre de hello d’utilisateurs ou de la charge de hello attendue pour un rôle particulier. Une machine virtuelle distincte est créée pour chaque instance d’un rôle lorsque le service de cloud computing hello s’exécute dans Azure. Cela affecte la facturation de hello pour le déploiement de hello de ce service cloud. Pour plus d’informations sur la facturation, consultez [Comprendre votre facture Microsoft Azure](billing/billing-understand-your-bill.md).

1. Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.

1. Dans **l’Explorateur de solutions**, développez le nœud de projet hello. Sous hello **rôles** nœud, de clic droit un rôle hello vous souhaitez tooupdate et, dans le menu contextuel de hello, sélectionnez **propriétés**.

    ![Menu contextuel de rôle Azure dans l’Explorateur de solutions](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Sélectionnez hello **Configuration** onglet.

    ![Onglet Configuration](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. Bonjour **Configuration du Service** liste, la configuration du service que vous souhaitez tooupdate sélectionnez hello.
   
    ![Liste Configuration du service](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. Bonjour **le nombre d’instances** texte, entrez le nombre de hello d’instances que vous souhaitez toostart pour ce rôle. Chaque instance s’exécute sur un ordinateur virtuel distinct lorsque vous publiez hello cloud service tooAzure.

    ![Nombre d’instances de hello mise à jour](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. À partir de hello Visual Studio, barre d’outils, sélectionnez **enregistrer**.

## <a name="manage-connection-strings-for-storage-accounts"></a>Gérer des chaînes de connexion pour des comptes de stockage
Vous pouvez ajouter, supprimer ou modifier des chaînes de connexion pour vos configurations de service. Par exemple, vous pouvez vouloir une chaîne de connexion locale pour une configuration de service local qui a pour valeur `UseDevelopmentStorage=true`. Vous pouvez également vous tooconfigure une configuration de service cloud qui utilise un compte de stockage dans Azure.

> [!WARNING]
> Lorsque vous entrez des informations clés de compte stockage Azure hello pour une chaîne de connexion de compte de stockage, ces informations sont stockées localement dans le fichier de configuration de service hello. Toutefois, ces informations ne sont pas stockées sous forme de texte chiffré pour le moment.
> 
> 

En utilisant une valeur différente pour chaque configuration de service, ne pas avoir toouse différentes chaînes de connexion dans votre service cloud ni modifier votre code lorsque vous publiez votre tooAzure de service cloud. Vous pouvez utiliser hello même nom pour la chaîne de connexion hello dans la valeur de votre code et hello est différent, selon la configuration du service hello que vous sélectionnez lorsque vous générez votre service cloud ou quand vous le publiez.

1. Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.

1. Dans **l’Explorateur de solutions**, développez le nœud de projet hello. Sous hello **rôles** nœud, de clic droit un rôle hello vous souhaitez tooupdate et, dans le menu contextuel de hello, sélectionnez **propriétés**.

    ![Menu contextuel de rôle Azure dans l’Explorateur de solutions](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Sélectionnez hello **paramètres** onglet.

    ![Onglet Paramètres](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. Bonjour **Configuration du Service** liste, la configuration du service que vous souhaitez tooupdate sélectionnez hello.

    ![Configuration du service](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. tooadd une chaîne de connexion, sélectionnez **ajouter un paramètre**.

    ![Ajouter une chaîne de connexion](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Une fois que le nouveau paramètre de hello a été ajouté toohello liste, mettre à jour de ligne hello dans la liste de hello avec les informations nécessaires hello.

    ![New connection string](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Nom** -Entrez le nom hello que vous souhaitez toouse pour la chaîne de connexion hello.
    - **Type** : sélectionnez **chaîne de connexion** à partir de la liste déroulante de hello.
    - **Valeur** -vous pouvez soit entrer la chaîne de connexion hello directement dans hello **valeur** cellule ou toowork de points de suspension (...) sélectionnez hello Bonjour **créer une chaîne de connexion stockage** boîte de dialogue.  

1. Bonjour **créer une chaîne de connexion stockage** boîte de dialogue, sélectionnez une option pour **se connecter à l’aide de**. Suivez ensuite les instructions hello pour option hello sélectionnée :

    - **Émulateur Microsoft Azure storage** -si vous sélectionnez cette option, les paramètres restants de hello sur la boîte de dialogue hello sont désactivées car ils s’appliquent uniquement tooAzure. Sélectionnez **OK**.
    - **Votre abonnement** : Si vous sélectionnez cette option, utilisez hello déroulante liste, sélectionnez tooeither et un signe un compte Microsoft, ou ajoutez un compte Microsoft. Sélectionnez un abonnement et un compte de stockage Azure. Sélectionnez **OK**.
    - **Entrées manuellement les informations d’identification** - Entrez le nom de compte de stockage hello et soit hello clé primaire ou secondaire. Sélectionnez une option pour **Connexion** (le protocole HTTPS est recommandé pour la plupart des scénarios.) Sélectionnez **OK**.

1. toodelete une chaîne de connexion, sélectionnez la chaîne de connexion hello et sélectionnez **supprimer un paramètre**.

1. À partir de hello Visual Studio, barre d’outils, sélectionnez **enregistrer**.

## <a name="programmatically-access-a-connection-string"></a>Accéder par programme à une chaîne de connexion

Hello étapes suivantes montrent comment tooprogrammatically accéder à une chaîne de connexion à l’aide de c#.

1. Ajoutez hello qui suit à l’aide du fichier de directives de tooa c# où vous allez paramètre hello de toouse :

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Hello de code suivant illustre un exemple de procédure tooaccess une chaîne de connexion. Remplacez hello &lt;ConnectionStringName > espace réservé avec la valeur appropriée de hello. 

    ```csharp
    // Setup hello connection tooAzure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-toouse-in-your-azure-cloud-service"></a>Ajouter des paramètres personnalisés toouse dans votre service cloud Azure
Paramètres personnalisés dans le fichier de configuration de service hello vous permettent d’ajouter un nom et une valeur pour une chaîne pour une configuration de service spécifique. Vous pouvez choisir toouse cette tooconfigure paramètre une fonctionnalité dans votre service cloud en lisant la valeur hello hello définition et l’utilisation de cette logique de hello toocontrol valeur dans votre code. Vous pouvez modifier ces valeurs de configuration de service sans avoir à toorebuild votre package de services ou lorsque votre service cloud est en cours d’exécution. Votre code peut vérifier les notifications produites lorsqu’un paramètre est modifié. Consultez [RoleEnvironment.Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).

Vous pouvez ajouter, supprimer ou modifier des paramètres personnalisés pour vos configurations de service. Vous pouvez vouloir différentes valeurs pour ces chaînes pour différentes configurations de service.

En utilisant une valeur différente pour chaque configuration de service, ne pas avoir toouse des chaînes différentes dans votre service cloud ni modifier votre code lorsque vous publiez votre tooAzure de service cloud. Vous pouvez utiliser hello même nom pour la chaîne hello dans votre code et hello est différent, selon la configuration du service hello que vous sélectionnez lorsque vous générez votre service cloud ou quand vous le publiez.

1. Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.

1. Dans **l’Explorateur de solutions**, développez le nœud de projet hello. Sous hello **rôles** nœud, de clic droit un rôle hello vous souhaitez tooupdate et, dans le menu contextuel de hello, sélectionnez **propriétés**.

    ![Menu contextuel de rôle Azure dans l’Explorateur de solutions](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Sélectionnez hello **paramètres** onglet.

    ![Onglet Paramètres](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. Bonjour **Configuration du Service** liste, la configuration du service que vous souhaitez tooupdate sélectionnez hello.

    ![Liste Configuration du service](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. tooadd un paramètre personnalisé, sélectionnez **ajouter un paramètre**.

    ![Ajouter un paramètre personnalisé](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Une fois que le nouveau paramètre de hello a été ajouté toohello liste, mettre à jour de ligne hello dans la liste de hello avec les informations nécessaires hello.

    ![Nouveau paramètre personnalisé](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Nom** -Entrez le nom hello du paramètre de hello.
    - **Type** : sélectionnez **chaîne** à partir de la liste déroulante de hello.
    - **Valeur** -Entrez la valeur hello du paramètre de hello. Vous pouvez soit entrer la valeur de hello directement dans hello **valeur** cellule ou valeur hello Sélectionnez points de suspension (...) tooenter hello hello **modification de la chaîne** boîte de dialogue.  

1. toodelete un paramètre personnalisé, sélectionnez le paramètre de hello, puis **supprimer un paramètre**.

1. À partir de hello Visual Studio, barre d’outils, sélectionnez **enregistrer**.

## <a name="programmatically-access-a-custom-settings-value"></a>Accéder par programme à la valeur d’un paramètre personnalisé
 
Hello étapes suivantes montrent comment tooprogrammatically accéder à un paramètre personnalisé à l’aide de c#.

1. Ajoutez hello qui suit à l’aide du fichier de directives de tooa c# où vous allez paramètre hello de toouse :

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. Hello de code suivant illustre un exemple de procédure tooaccess un paramètre personnalisé. Remplacez hello &lt;SettingName > espace réservé avec la valeur appropriée de hello. 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a>Gérer le stockage local pour chaque instance de rôle
Vous pouvez ajouter le stockage de système de fichiers local pour chaque instance d’un rôle. données de salutation stockées dans le stockage n’est pas accessible par d’autres instances de rôle hello pour le hello données sont stockées, ou par les autres rôles.  

1. Créez ou ouvrez un projet de service cloud Azure dans Visual Studio.

1. Dans **l’Explorateur de solutions**, développez le nœud de projet hello. Sous hello **rôles** nœud, de clic droit un rôle hello vous souhaitez tooupdate et, dans le menu contextuel de hello, sélectionnez **propriétés**.

    ![Menu contextuel de rôle Azure dans l’Explorateur de solutions](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Sélectionnez hello **stockage Local** onglet.

    ![Onglet Stockage local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. Bonjour **Configuration du Service** liste, vérifiez que **toutes les Configurations** est sélectionné comme paramètres de stockage local hello appliquent des configurations de service tooall. Toute autre valeur entraîne de tous les champs d’entrée hello sur la page hello en cours de désactivation. 

    ![Liste Configuration du service](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. tooadd une entrée de stockage local, sélectionnez **ajouter un stockage Local**.

    ![Ajouter le stockage local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. Une fois la nouvelle entrée de stockage local hello a été ajoutée toohello liste, mettre à jour de ligne hello dans la liste de hello avec les informations nécessaires hello.

    ![Nouvelle entrée de stockage local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - **Nom** -Entrez le nom hello que vous souhaitez toouse de stockage local hello.
    - **Taille (Mo)** -Entrez la taille de hello en Mo dont vous avez besoin de stockage local hello.
    - **Nettoyage de recyclage des rôles** -sélectionner ces données de hello tooremove option dans le stockage local nouvelle hello lors de la machine virtuelle de hello pour le rôle de hello est recyclé.

1. toodelete une entrée de stockage local, sélectionnez l’entrée de hello et sélectionnez **supprimer le stockage Local**.

1. À partir de hello Visual Studio, barre d’outils, sélectionnez **enregistrer**.

## <a name="programmatically-accessing-local-storage"></a>Accès par programme au stockage local

Cette section illustre comment accéder à l’aide de c# en écrivant un fichier texte de test de stockage local tooprogrammatically `MyLocalStorageTest.txt`.  

### <a name="write-a-text-file-toolocal-storage"></a>Écrire un stockage toolocal du fichier texte

Hello suivant de code montre comment toowrite un texte toolocal stockage de fichiers. Remplacez hello &lt;LocalStorageName > espace réservé avec la valeur appropriée de hello. 

    ```csharp
    // Retrieve an object that points toohello local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define hello file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-toolocal-storage"></a>Rechercher un fichier écrit toolocal stockage

fichier de hello tooview créée par le code hello dans la section précédente de hello, procédez comme suit :
    
1.  Hello la zone de notification Windows, avec le bouton droit hello icône Windows Azure et, dans le menu contextuel de hello, sélectionnez **Show Compute Emulator UI**. 

    ![Afficher l’émulateur de calcul Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. Sélectionnez un rôle web de hello.

    ![Émulateur de calcul Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. Sur hello **émulateur de calcul Azure Microsoft** menu, sélectionnez **outils** > **ouvrir magasin local**.

    ![Élément du menu Ouvrir magasin local](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. Lors de la fenêtre de l’Explorateur Windows hello s’ouvre, entrez « MyLocalStorageTest.txt'' dans hello **recherche** zone de texte, puis sélectionnez **entrée** recherche de hello toostart. 

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur les projets Azure dans Visual Studio en lisant [Configuration d’un projet Azure](vs-azure-tools-configuring-an-azure-project.md). En savoir plus sur le schéma de service cloud hello en lisant [référence du schéma](https://msdn.microsoft.com/library/azure/dd179398).

