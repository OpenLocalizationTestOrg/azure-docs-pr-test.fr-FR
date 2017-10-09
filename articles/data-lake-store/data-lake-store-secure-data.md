---
title: "aaaSecuring les données stockées dans Azure Data Lake Store | Documents Microsoft"
description: "Découvrez comment les listes de contrôle de données toosecure dans Azure Data Lake Store à l’aide de groupes et l’accès"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ca35e65f-3986-4f1b-bf93-9af6066bb716
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 2b4ed7e322e1843ca47d6968ec8801ac19ea6399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-data-stored-in-azure-data-lake-store"></a>Sécurisation des données stockées dans Azure Data Lake Store
La sécurisation des données dans Azure Data Lake Store se fait en trois étapes.

1. Commencez par créer des groupes de sécurité dans Azure Active Directory (AAD). Ces groupes de sécurité sont utilisés tooimplement contrôle d’accès basé sur un rôle (RBAC) dans le portail Azure. Pour plus d'informations, consultez la page [Contrôle d'accès en fonction du rôle dans Microsoft Azure](../active-directory/role-based-access-control-configure.md).
2. Affecter le compte Azure Data Lake Store toohello de groupes hello AAD sécurité. Ce paramètre contrôle accès toohello Data Lake Store compte des opérations de gestion et de portail hello du portail de hello ou les API.
3. Affecter des groupes de sécurité AAD hello comme les listes de contrôle d’accès (ACL) sur le système de fichiers hello Data Lake Store.
4. En outre, vous pouvez également définir une plage d’adresses IP pour les clients qui peuvent accéder aux données hello dans Data Lake Store.

Cet article explique comment toouse hello hello tooperform portail Azure au-dessus des tâches. Pour obtenir des informations détaillées sur comment Data Lake Store implémente la sécurité au niveau de compte et les données hello, consultez [sécurité dans Azure Data Lake Store](data-lake-store-security-overview.md). Pour des informations détaillées sur la façon dont les listes de contrôle d’accès sont implémentées dans Azure Data Lake Store, consultez [Overview of Access Control in Data Lake Store](data-lake-store-access-control.md) (Vue d’ensemble du contrôle d’accès dans Data Lake Store).

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un compte Azure Data Lake Store**. Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md)

## <a name="create-security-groups-in-azure-active-directory"></a>Créer des groupes de sécurité dans Azure Active Directory
Pour obtenir des instructions sur la façon de groupes de sécurité AAD toocreate et comment tooadd du groupe utilisateurs toohello, consultez [la gestion des groupes de sécurité dans Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).

> [!NOTE] 
> Vous pouvez ajouter des utilisateurs et des autres groupes tooa groupe dans Azure AD à l’aide de hello portail Azure. Toutefois, dans une commande tooadd un groupe tooa principal de service, utilisez [module PowerShell d’Azure AD](../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md).
> 
> ```powershell
> # Get hello desired group and service principal and identify hello correct object IDs
> Get-AzureADGroup -SearchString "<group name>"
> Get-AzureADServicePrincipal -SearchString "<SPI name>"
> 
> # Add hello service principal toohello group
> Add-AzureADGroupMember -ObjectId <Group object ID> -RefObjectId <SPI object ID>
> ```
 
## <a name="assign-users-or-security-groups-tooazure-data-lake-store-accounts"></a>Affecter des utilisateurs ou des groupes de sécurité des comptes Data Lake Store tooAzure
Lorsque vous affectez des utilisateurs ou des comptes Data Lake Store tooAzure les groupes de sécurité, vous contrôlez les opérations de gestion de toohello accès sur compte hello hello portail Azure et les API du Gestionnaire de ressources Azure. 

1. Ouvrez un compte Azure Data Lake Store. Dans le volet gauche de hello, cliquez sur **Parcourir**, cliquez sur **Data Lake Store**, puis cliquez sur toowhich de nom de compte hello souhaité tooassign un utilisateur ou groupe de sécurité à partir du panneau hello Data Lake Store.

2. Dans le panneau des paramètres de votre compte Data Lake Store, cliquez sur **Contrôle d’accès (IAM)**. panneau Hello par les listes par défaut **administrateurs d’abonnements** groupe en tant que propriétaire.
   
    ![Affecter le compte de sécurité groupe tooAzure Data Lake Store](./media/data-lake-store-secure-data/adl.select.user.icon.png "affecter le compte de sécurité groupe tooAzure Data Lake Store")

    Il existe deux façons tooadd un groupe et affecter des rôles appropriés.
   
    * Ajouter un compte d’utilisateur/groupe toohello et puis affectez un rôle, ou
    * Ajouter un rôle, puis attribuez les utilisateurs/groupes toorole.
     
    Dans cette section, nous allons à la première approche de hello, ajout d’un groupe, puis en attribuant les rôles. Vous pouvez exécuter la sélection de toofirst étapes similaires un rôle, puis attribuez rôle toothat de groupes.
4. Bonjour **utilisateurs** panneau, cliquez sur **ajouter** tooopen hello **ajouter un accès** panneau. Bonjour **ajouter un accès** panneau, cliquez sur **sélectionner un rôle**, puis sélectionnez un rôle pour hello/groupe d’utilisateurs.
   
    ![Ajouter un rôle d’utilisateur de hello](./media/data-lake-store-secure-data/adl.add.user.1.png "ajouter un rôle d’utilisateur de hello")
   
    Hello **propriétaire** et **collaborateur** rôle fournissent accès tooa des fonctions d’administration sur le compte hello data lake. Pour les utilisateurs qui interagissent avec les données de LAC de données hello, vous pouvez les ajouter toohello ** lecteur ** rôle. Hello traite de ces rôles toohello limité gestion opérations connexes toohello compte Azure Data Lake Store.
   
    Pour les données les autorisations de système de fichiers individuels operations définissent ce que peuvent faire les utilisateurs hello. Par conséquent, un rôle de lecture d’un utilisateur peut uniquement afficher paramètres d’administration associés au compte de hello mais peuvent potentiellement lire et écrire données en fonction des autorisations de système de fichiers affectées toothem. Les autorisations de système de fichiers Data Lake Store sont décrites sur [le groupe de sécurité attribuer en tant que les ACL toohello système de fichiers Azure Data Lake Store](#filepermissions).
5. Bonjour **ajouter un accès** panneau, cliquez sur **ajouter des utilisateurs** tooopen hello **ajouter des utilisateurs** panneau. Dans ce panneau, recherchez le groupe de sécurité hello que vous avez créé précédemment dans Azure Active Directory. Si vous avez un grand nombre de toosearch de groupes à partir de, utilisez la zone de texte de hello à toofilter supérieur de hello sur le nom du groupe hello. Cliquez sur **Sélectionner**.
   
    ![Ajouter un groupe de sécurité](./media/data-lake-store-secure-data/adl.add.user.2.png "Ajouter un groupe de sécurité")
   
    Si vous voulez tooadd un utilisateur ou le groupe qui n’est pas répertorié, vous pouvez les inviter à l’aide de hello **inviter** icône et en spécifiant l’adresse de messagerie hello hello/groupe d’utilisateurs.
6. Cliquez sur **OK**. Vous devez voir le groupe de sécurité hello ajouté comme indiqué ci-dessous.
   
    ![Groupe de sécurité ajouté](./media/data-lake-store-secure-data/adl.add.user.3.png "Groupe de sécurité ajouté")

7. Votre groupe de sécurité de l’utilisateur/a maintenant un compte d’accès à Azure Data Lake Store toohello. Si vous souhaitez que les utilisateurs de toospecific tooprovide accès, vous pouvez ajouter les groupe de sécurité toohello. De même, si vous souhaitez accéder toorevoke pour un utilisateur, vous pouvez les supprimer du groupe de sécurité hello. Vous pouvez également affecter plusieurs groupes de sécurité tooan compte. 

## <a name="filepermissions"></a>Affecter des utilisateurs ou groupe de sécurité comme les ACL toohello système de fichiers Azure Data Lake Store
En affectant des groupes de sécurité de l’utilisateur/système de fichiers Azure Data Lake toohello, vous définir de contrôle d’accès aux données hello stockées dans Azure Data Lake Store.

1. Dans le panneau de votre compte Data Lake Store, cliquez sur **Explorateur de données**.
   
    ![Créer des répertoires dans un compte Data Lake Store](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Créer des répertoires dans un compte Data Lake Store")
2. Bonjour **Explorateur de données** panneau, cliquez sur le fichier de hello ou un dossier pour lequel vous souhaitez tooconfigure hello ACL, puis cliquez sur **accès**. fichier de tooa tooassign ACL, vous devez cliquer sur **accès** de hello **l’aperçu du fichier** panneau.
   
    ![Définir des ACL sur le système de fichiers Data Lake](./media/data-lake-store-secure-data/adl.acl.1.png "Définir des ACL sur le système de fichiers Data Lake")
3. Hello **accès** panneau répertorie les accès standard hello et accès personnalisé déjà affecté toohello racine. Cliquez sur hello **ajouter** icône tooadd personnalisée au niveau du ACL.
   
    ![Lister les accès standard et personnalisés](./media/data-lake-store-secure-data/adl.acl.2.png "Lister les accès standard et personnalisés")
   
   * **Accès standard** est hello accès de style UNIX, où vous spécifiez lire, écrire, exécuter des classes d’utilisateurs distincts (rwx) toothree : propriétaire, groupe et autres.
   * **Accès personnalisé** correspond ACL POSIX toohello qui vous permet de tooset autorisations pour utilisateurs nommés spécifiques ou groupes et non seulement du fichier hello propriétaire ou groupe. 
     
     Pour plus d'informations, consultez la page [ACL HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). Pour plus d’informations sur l’implémentation des ACL dans Data Lake Store, consultez [Contrôle d’accès dans Data Lake Store](data-lake-store-access-control.md).
4. Cliquez sur hello **ajouter** hello de tooopen icône **ajouter un accès personnalisé à** panneau. Dans ce panneau, cliquez sur **sélectionner utilisateur ou groupe**, puis dans **sélectionner utilisateur ou groupe** panneau, recherchez le groupe de sécurité hello vous avez créé précédemment dans Azure Active Directory. Si vous avez un grand nombre de toosearch de groupes à partir de, utilisez la zone de texte de hello à toofilter supérieur de hello sur le nom du groupe hello. Cliquez sur le groupe hello tooadd et puis cliquez sur **sélectionnez**.
   
    ![Ajouter un groupe](./media/data-lake-store-secure-data/adl.acl.3.png "Ajouter un groupe")
5. Cliquez sur **autorisations Select**, sélectionnez les autorisations hello et si vous souhaitez définir des autorisations hello tooassign comme une ACL par défaut, accès ACL, ou les deux. Cliquez sur **OK**.
   
    ![Affecter des autorisations toogroup](./media/data-lake-store-secure-data/adl.acl.4.png "affecter des autorisations toogroup")
   
    Pour plus d’informations sur les autorisations dans Data Lake Store et sur les ACL par défaut ou d’accès, consultez [Contrôle d’accès dans Azure Data Lake Store](data-lake-store-access-control.md).
6. Bonjour **ajouter un accès personnalisé à** panneau, cliquez sur **OK**. Hello récemment ajouté de groupe, avec des autorisations hello associée, est maintenant listée dans hello **accès** panneau.
   
    ![Affecter des autorisations toogroup](./media/data-lake-store-secure-data/adl.acl.5.png "affecter des autorisations toogroup")
   
   > [!IMPORTANT]
   > Dans la version actuelle de hello, vous ne pouvez avoir 9 entrées sous **personnalisé accès**. Si vous souhaitez tooadd les utilisateurs plus de 9, vous devez créer des groupes de sécurité, ajouter des utilisateurs toosecurity groupes, ajouter fournir un accès à des groupes de sécurité toothose hello compte Data Lake Store.
   > 
   > 
7. Si nécessaire, vous pouvez également modifier les autorisations d’accès hello après avoir ajouté le groupe de hello. Désactivez ou activez hello case à cocher pour chaque autorisation de type (lire, écrire, exécuter) selon que vous souhaitez tooremove ou affecter à ce groupe de sécurité toohello autorisation. Cliquez sur **enregistrer** modifications hello toosave ou **ignorer** modifications de hello tooundo.

## <a name="set-ip-address-range-for-data-access"></a>Définir la plage d’adresses IP pour accéder aux données
Azure Data Lake Store vous permet de verrouiller de toofurther de magasin de données access tooyour au niveau du réseau. Vous pouvez activer le pare-feu, spécifier une adresse IP ou définir une plage d’adresses IP pour vos clients approuvés. Une fois activée, seuls les clients qui ont des adresses IP de hello au sein de la plage définie peuvent se connecter toohello magasin.

![Paramètres de pare-feu et accès IP](./media/data-lake-store-secure-data/firewall-ip-access.png "Paramètres de pare-feu et accès IP")

## <a name="remove-security-groups-for-an-azure-data-lake-store-account"></a>Supprimer les groupes de sécurité d'un compte Azure Data Lake Store
Lorsque vous supprimez des groupes de sécurité à partir de comptes Azure Data Lake Store, vous modifiez uniquement les opérations de gestion de l’accès toohello sur compte hello hello portail Azure et les API du Gestionnaire de ressources Azure.

1. Dans le panneau de votre compte Data Lake Store, cliquez sur **Paramètres**. À partir de hello **paramètres** panneau, cliquez sur **utilisateurs**.
   
    ![Affecter le compte de sécurité groupe tooAzure Data Lake](./media/data-lake-store-secure-data/adl.select.user.icon.png "affecter le compte de sécurité groupe tooAzure Data Lake")
2. Bonjour **utilisateurs** panneau sur le groupe de sécurité de hello souhaité tooremove.
   
    ![Tooremove de groupe de sécurité](./media/data-lake-store-secure-data/adl.add.user.3.png "tooremove de groupe de sécurité")
3. Dans le panneau de hello pour le groupe de sécurité hello, cliquez sur **supprimer**.
   
    ![Groupe de sécurité supprimé](./media/data-lake-store-secure-data/adl.remove.group.png "Groupe de sécurité supprimé")

## <a name="remove-security-group-acls-from-azure-data-lake-store-file-system"></a>Supprimer les ACL d'un groupe de sécurité du système de fichiers Azure Data Lake Store
Lorsque vous supprimez des groupes de sécurité ACL de système de fichiers Azure Data Lake Store, vous modifiez les accès aux données toohello hello Data Lake Store.

1. Dans le panneau de votre compte Data Lake Store, cliquez sur **Explorateur de données**.
   
    ![Créer des répertoires dans un compte Data Lake](./media/data-lake-store-secure-data/adl.start.data.explorer.png "Créer des répertoires dans un compte Data Lake")
2. Bonjour **Explorateur de données** panneau, cliquez sur le fichier de hello ou un dossier pour lequel vous souhaitez tooremove hello ACL, puis cliquez dans le panneau de votre compte, hello **accès** icône. tooremove ACL pour un fichier, vous devez cliquer sur **accès** de hello **l’aperçu du fichier** panneau.
   
    ![Définir des ACL sur le système de fichiers Data Lake](./media/data-lake-store-secure-data/adl.acl.1.png "Définir des ACL sur le système de fichiers Data Lake")
3. Bonjour **accès** panneau, à partir de hello **personnalisé accès** , cliquez sur le groupe de sécurité hello souhaité tooremove. Bonjour **personnalisé accès** panneau, cliquez sur **supprimer** puis cliquez sur **OK**.
   
    ![Affecter des autorisations toogroup](./media/data-lake-store-secure-data/adl.remove.acl.png "affecter des autorisations toogroup")

## <a name="see-also"></a>Voir aussi
* [Présentation d'Azure Data Lake Store](data-lake-store-overview.md)
* [Copier des données d’objets BLOB de stockage Azure tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md)
* [Utiliser Azure Data Lake Analytics avec Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Utiliser Azure HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Prise en main de Data Lake Store avec PowerShell](data-lake-store-get-started-powershell.md)
* [Prise en main de Data Lake Store avec le Kit de développement logiciel (SDK) .NET](data-lake-store-get-started-net-sdk.md)
* [Accéder aux journaux de diagnostic de Data Lake Store](data-lake-store-diagnostic-logs.md)

