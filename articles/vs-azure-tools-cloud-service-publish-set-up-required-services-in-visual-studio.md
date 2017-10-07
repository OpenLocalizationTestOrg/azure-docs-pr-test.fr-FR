---
title: "aaaPrepare toopublish ou déployer une application Windows Azure à partir de Visual Studio | Documents Microsoft"
description: "En savoir plus tooset de procédures hello des services de compte de stockage et de cloud et configurer votre application Windows Azure."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 92ee2f9e-ec49-4c7a-900d-620abe5e9d8a
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: b5231d400e2ad9e20c3f21bad48a77c328b1f7a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-toopublish-or-deploy-an-azure-application-from-visual-studio"></a>Préparer tooPublish ou déployer une Application Azure depuis Visual Studio
## <a name="overview"></a>Vue d'ensemble
Avant de pouvoir publier un projet de service cloud, vous devez configurer hello suivant services :

* A **service de cloud computing** toorun vos rôles Bonjour environnement Azure
* A **compte de stockage** qui fournit l’accès toohello des services Blob, file d’attente et Table.

Hello suivant tooset procédures ces services et de configurer votre application

## <a name="create-a-cloud-service"></a>Création d'un service cloud
toopublish un tooAzure de service cloud, vous devez d’abord créer un service cloud, qui exécute vos rôles Bonjour environnement Azure. Vous pouvez créer un service cloud dans hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), comme décrit dans la section de hello **toocreate un service cloud à l’aide de hello portail Azure classic**, plus loin dans cette rubrique. Vous pouvez également créer un service cloud dans Visual Studio à l’aide de l’Assistant Publication de hello.

### <a name="toocreate-a-cloud-service-by-using-visual-studio"></a>toocreate un service cloud à l’aide de Visual Studio
1. Ouvrez le menu contextuel hello hello projet Windows Azure, puis choisissez **publier**.

    ![VST_PublishMenu](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/vst-publish-menu.png)
2. Si vous n’avez pas encore connecté, connectez-vous avec votre nom d’utilisateur et un mot de passe pour le compte Microsoft de hello ou un compte professionnel associé à votre abonnement Azure.
3. Choisissez hello **suivant** bouton tooadvance toohello **paramètres** page.

    ![Paramètres courants de l'Assistant Publication](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/publish-settings-page.png)
4. Bonjour **Services de cloud computing** , choisissez **créer un nouveau**. Hello **créer des Services Azure** boîte de dialogue s’affiche.
5. Entrez le nom hello de votre service cloud. nom de Hello constitue une partie de l’URL de hello pour votre service et par conséquent doit être globalement unique. nom de Hello n’est pas sensible à la casse.

### <a name="toocreate-a-cloud-service-by-using-hello-azure-classic-portal"></a>toocreate un service cloud à l’aide de hello portail Azure classic
1. Connectez-vous à toohello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkId=253103) sur le site Web de Microsoft hello.
2. toodisplay (facultatif) une liste de services de cloud computing que vous avez déjà créées, choisissez le lien des Services de cloud computing hello sur le côté gauche de hello de page de hello.
3. Choisissez hello  **+**  icône hello en bas à gauche dans le coin inférieur droit, puis choisissez **Service Cloud** sur le menu hello qui s’affiche. Un autre écran s’affiche avec deux options, **Création rapide** et **Création personnalisée**. Si vous choisissez **création rapide**, vous pouvez créer un service cloud simplement en spécifiant son URL et hello la région où il sera physiquement hébergé. Si vous sélectionnez **Création personnalisée**, vous pouvez publier immédiatement un service cloud en spécifiant un package (fichier .cspkg), un fichier de configuration (.cscfg) et un certificat. Création personnalisée n’est pas nécessaire si vous avez l’intention de toopublish votre service cloud à l’aide de hello **publier** dans un projet Windows Azure. Hello **publier** commande est disponible dans le menu contextuel de hello pour un projet Windows Azure.
4. Choisissez **création rapide** toolater publier votre service cloud à l’aide de Visual Studio.
5. Spécifiez un nom pour votre service cloud. URL complète de Hello apparaît nom toohello suivant.
6. Dans la liste hello, choisissez la région hello où se trouvent la plupart de vos utilisateurs.
7. En bas de hello de fenêtre hello, choisissez hello **créer un Service Cloud** lien.

## <a name="create-a-storage-account"></a>Créez un compte de stockage.
Un compte de stockage fournit l’accès toohello des services Blob, file d’attente et Table. Vous pouvez créer un compte de stockage à l’aide de Visual Studio ou hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkId=253103).

### <a name="toocreate-a-storage-account-by-using-visual-studio"></a>toocreate un compte de stockage à l’aide de Visual Studio
1. Dans **l’Explorateur de solutions**, ouvrez hello sur le menu contextuel hello **stockage** nœud, puis choisissez **créer un compte de stockage**.

    ![Créer un compte de stockage Azure](./media/vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio/IC744166.png)
2. Sélectionnez ou entrez hello suivant les informations de compte de stockage hello Bonjour **créer un compte de stockage** boîte de dialogue.

   * Bonjour toowhich abonnement Azure vous souhaitez que le compte de stockage tooadd hello.
   * Hello nom toouse hello nouveau compte de stockage.
   * région de Hello ou un groupe d’affinités (par exemple, ouest des États-Unis ou Asie orientale).
   * Hello du type de réplication que vous souhaitez toouse hello compte de stockage, telles que géo-redondant.
3. Lorsque vous avez terminé, choisissez **créer**.hello nouveau compte de stockage apparaît dans hello **stockage** liste **l’Explorateur de serveurs**.

### <a name="toocreate-a-storage-account-by-using-hello-azure-classic-portal"></a>toocreate un compte de stockage à l’aide de hello portail Azure classic
1. Connectez-vous à toohello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkId=253103) sur le site Web de Microsoft hello.
2. (Facultatif) tooview vos comptes de stockage, choisissez hello **stockage** lien dans le panneau de configuration hello sur hello à gauche de la page de hello.
3. Dans l’angle inférieur gauche de hello de page de hello, choisissez hello  **+**  icône.
4. Dans le menu hello qui s’affiche, choisissez **stockage**, puis choisissez **création rapide**.
5. Nommez compte de stockage hello qui génère une url unique.
6. Attribuez un nom à votre service cloud. URL complète de Hello apparaît nom toohello suivant.
7. Dans la liste de hello des régions, choisissez une région où se trouvent la plupart de vos utilisateurs.
8. Spécifier si vous souhaitez tooenable géo-réplication. Si vous activez la géo-réplication, vos données seront enregistrées dans plusieurs risques de hello tooreduce emplacements physiques de perte. Cette fonctionnalité permet de stockage plus onéreux, mais vous pouvez réduire le coût de hello en activant la géolocalisation lorsque vous créez le compte de stockage hello au lieu d’ajouter des fonctionnalités de hello plus tard. Pour plus d’informations, consultez [Géo-réplication](http://go.microsoft.com/fwlink/?LinkId=253108).
9. En bas de hello de fenêtre hello, choisissez hello **créer un compte de stockage** lien.

Après avoir créé votre compte de stockage, vous verrez hello URL que vous pouvez utiliser les ressources tooaccess dans chacun des services de stockage Azure hello et hello également les clés d’accès primaire et secondaire pour votre compte. Vous utilisez ces clés tooauthenticate les demandes effectuées auprès des services de stockage hello.

> [!NOTE]
> clé d’accès secondaire Hello fournit hello même accéder au compte de stockage tooyour en tant que clé d’accès primaire hello et est générée comme une sauvegarde de votre clé d’accès primaire du doit être compromis. En outre, il est recommandé de régénérer régulièrement vos clés d'accès. Vous pouvez modifier une connexion chaîne paramètre toouse hello clé secondaire pendant la régénération de clé primaire de hello, puis vous pouvez la modifier clé primaire de toouse hello régénérée pendant la régénération de la clé secondaire de hello.
>
>

## <a name="configure-your-app-toouse-services-provided-by-hello-storage-account"></a>Configurer vos services de toouse application fournies par le compte de stockage hello
Vous devez configurer un rôle qui accède au stockage toouse hello stockage Azure des services que vous avez créés. toodo, vous pouvez utiliser plusieurs configurations de service pour votre projet Windows Azure. Par défaut, deux sont créées dans votre projet Azure. À l’aide de plusieurs configurations de service, vous pouvez utiliser hello connexion même chaîne dans votre code, mais ont une valeur différente pour une chaîne de connexion dans chaque configuration de service. Par exemple, vous pouvez utiliser un toorun de configuration de service et déboguer votre application localement à l’aide d’émulateur de stockage Azure hello et un toopublish de configuration de service différent tooAzure de votre application. Pour plus de configuration sur les configurations de service, consultez la page [Configuration de votre projet Azure à l’aide de plusieurs configurations de service](vs-azure-tools-multiple-services-project-configurations.md).

### <a name="tooconfigure-your-application-toouse-services-that-hello-storage-account-provides"></a>Fournit des services de toouse votre application hello compte de stockage tooconfigure
1. Dans Visual Studio, ouvrez votre solution Azure. Dans l’Explorateur de solutions, ouvrez le menu contextuel de hello pour chaque rôle dans votre projet Windows Azure qui accède aux services de stockage hello et choisissez **propriétés**. Une page avec le nom hello du rôle de hello est affichée dans l’éditeur de Visual Studio hello. page de Hello affiche les champs de hello pour hello **Configuration** onglet.
2. Dans les pages de propriétés hello pour le rôle de hello, choisissez **paramètres**.
3. Bonjour **Configuration du Service** , choisissez nom hello de configuration du service hello que vous souhaitez tooedit. Si vous souhaitez tooall de modifications toomake des configurations de service hello pour ce rôle, vous pouvez choisir **toutes les Configurations**.  Pour plus d’informations sur comment tooupdate configurations de service, consultez la section de hello **gérer les chaînes de connexion pour les comptes de stockage** dans la rubrique de hello [configurer des rôles de hello pour un Service de Cloud Azure avec Visual Studio ](vs-azure-tools-configure-roles-for-cloud-service.md).
4. toomodify des paramètres de chaîne de connexion, choisissez hello **...** bouton paramètre toohello suivant. Hello **créer une chaîne de connexion stockage** boîte de dialogue s’affiche.
5. Sous **se connecter à l’aide de**, choisissez hello **votre abonnement** option.
6. Bonjour **abonnement** , choisissez votre abonnement. Si la liste hello des abonnements n’inclut pas hello celui que vous voulez, choisissez hello **télécharger les paramètres de publication** lien.
7. Bonjour **nom de compte** , sélectionnez le nom de votre compte de stockage. Windows Azure Tools Obtient les informations d’identification du compte de stockage automatiquement à l’aide du fichier .publishsettings de hello. toospecify informations d’identification de votre compte de stockage manuellement, choisissez hello **manuellement les informations d’identification entrées** option, puis continuez cette procédure. Vous pouvez obtenir votre nom de compte de stockage et la clé primaire à partir de hello [portail Azure classic](http://go.microsoft.com/fwlink/p/?LinkID=213885). Si vous ne souhaitez pas toospecify paramètres de votre compte de stockage manuellement, cliquez hello **OK** boîte de dialogue bouton tooclose hello.
8. Choisissez hello **Entrez le compte de stockage** lien des informations d’identification.
9. Bonjour **nom de compte** , entrez le nom hello de votre compte de stockage.

   > [!NOTE]
   > Ouvrez une session sur hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), puis choisissez hello **stockage** bouton. portail de Hello affiche une liste de comptes de stockage. Si vous sélectionnez un compte, une page associée s'ouvre. Vous pouvez copier le nom hello hello du compte de stockage à partir de cette page. Si vous utilisez une version précédente du portail classique de hello, nom hello de votre compte de stockage apparaît dans hello **comptes de stockage** vue. toocopy ce nom, de mettre en surbrillance dans hello **propriétés** de cette fenêtre d’afficher, puis appuyez sur les touches Ctrl-C de hello. nom de hello toopaste dans Visual Studio, choisissez hello **nom de compte** texte zone, puis choisissez les touches Ctrl + V de hello.
   >
   >
10. Bonjour **clé de compte** , entrez votre clé primaire, ou copiez et collez-le à partir de hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885).
     toocopy cette clé :

    1. Bas hello de page hello hello compte de stockage approprié, choisissez hello **gérer les clés** bouton.
    2. Sur hello **gérer l’accès aux clés** page, sélectionner le texte hello de clé d’accès primaire hello, puis choisissez les touches Ctrl + C de hello.
    3. Dans Windows Azure Tools, collez la clé de hello dans hello **clé de compte** boîte.
    4. Vous devez sélectionner une des hello suivant options toodetermine comment le service de hello accédera compte de stockage hello :

       * **Utiliser HTTP**. Il s’agit d’option standard de hello. Par exemple, `http://<account name>.blob.core.windows.net`.
       * **Utiliser HTTPS** pour une connexion sécurisée. Par exemple, `https://<accountname>.blob.core.windows.net`.
       * **Spécifiez les points de terminaison personnalisés** pour chacun des services de hello trois. Vous pouvez ensuite saisir ces points de terminaison dans le champ hello pour un service spécifique de hello.

         > [!NOTE]
         > Si vous créez des points de terminaison personnalisés, vous pouvez créer une chaîne de connexion plus complexe. Lorsque vous utilisez ce format de chaîne, vous pouvez spécifier des points de terminaison stockage service qui incluent un nom de domaine personnalisé que vous avez enregistré pour votre compte de stockage avec hello service Blob. Vous pouvez également accorder l’accès tooblob uniquement les ressources dans un seul conteneur via une signature d’accès partagé. Pour plus d’informations sur la façon toocreate des points de terminaison personnalisés, consultez [configurer des chaînes de connexion de stockage Azure](storage/common/storage-configure-connection-string.md).
         >
         >
11. toosave ces modifications de chaîne de connexion, choisissez hello **OK** bouton, puis choisissez hello **enregistrer** bouton de barre d’outils hello. Après avoir enregistré ces modifications, vous pouvez obtenir la valeur hello de cette chaîne de connexion dans votre code à l’aide de [GetConfigurationSettingValue](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.getconfigurationsettingvalue.aspx). Lorsque vous publiez votre application tooAzure, choisissez la configuration du service hello qui contient le compte de stockage Azure hello pour la chaîne de connexion hello. Une fois que votre application est publiée, vérifiez que l’application hello fonctionne comme prévu en fonction des services de stockage Azure hello

## <a name="next-steps"></a>Étapes suivantes
toolearn savoir plus sur la publication tooAzure d’applications à partir de Visual Studio, consultez [publication d’un Service Cloud à l’aide des outils d’Azure hello](vs-azure-tools-publishing-a-cloud-service.md).
