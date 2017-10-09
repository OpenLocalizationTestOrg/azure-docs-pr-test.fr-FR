---
title: "aaaRun n’importe quelle application Windows sur n’importe quel appareil avec Azure RemoteApp | Documents Microsoft"
description: "Découvrez comment tooshare n’importe quelle application Windows avec vos utilisateurs à l’aide d’Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 961d40ca-9673-4977-aa54-d6b22fc61ce1
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 750f3b881e0cb671ff6e8f3e851bccdf2262d156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-any-windows-app-on-any-device-with-azure-remoteapp"></a>Exécuter n’importe quelle application Windows sur n’importe quel appareil avec Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Vous pouvez exécuter une application Windows n’importe où et sur n’importe quel appareil. Pour cela, il vous suffit d’utiliser Azure RemoteApp. S’il s’agit d’une application personnalisée écrite il y a 10 ans, ou une application Office, vos utilisateurs n’ont plus toobe liée tooa système d’exploitation spécifique (par exemple, Windows XP) pour les applications peu.

Avec Azure RemoteApp, vos utilisateurs peuvent également utiliser leur propres Android ou get et Apple hello la même expérience qu’ils ont été sur Windows (ou sur les appareils Windows Phone). Pour obtenir ce résultat, votre application Windows est hébergée sur une collection de machines virtuelles Windows via Azure, auxquelles vos utilisateurs peuvent accéder depuis n’importe quel lieu connecté à Internet. 

Lisez la suite pour obtenir un exemple d’exactement comment toodo cela.

Dans cet article, nous allons tooshare accès avec tous nos utilisateurs. Toutefois, vous pouvez utiliser n'importe quelle application. Tant que vous pouvez installer votre application sur un ordinateur Windows Server 2012 R2, vous pouvez le partager à l’aide des étapes hello ci-dessous. Vous pouvez passer en revue hello [spécifications des applications](remoteapp-appreqs.md) toomake que votre application de fonctionner.

Notez qu’étant donné que l’accès est une base de données, et nous souhaitons que toobe de base de données utiles, nous prévoyez d’effectuer quelques étapes supplémentaires toolet utilisateurs Accédez partage de données Access hello. Si votre application n’est pas une base de données, ou vous n’avez pas besoin votre tooaccess en mesure des utilisateurs toobe un partage de fichiers, vous pouvez ignorer ces étapes dans ce didacticiel

> [!NOTE]
> <a name="note"></a>Vous avez besoin une toocomplete compte Azure ce didacticiel :
> 
> * Vous pouvez [ouvrir un compte Azure gratuitement](https://azure.microsoft.com/free/?WT.mc_id=A261C142F): vous obtenez des crédits vous pouvez utiliser tootry à payer des services Azure et même après qu’ils soient utilisés jusqu'à vous pouvez conserver le compte de hello et libérer de l’utilisation des services Azure, comme les sites Web. Votre carte de crédit ne sera jamais facturé, sauf si vous explicitement modifiez vos paramètres et demandez toobe facturé.
> * Vous pouvez [activer les avantages de l’abonnement MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): votre abonnement MSDN vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants.
> 
> 

## <a name="create-a-collection-in-remoteapp"></a>Création d’une collection dans RemoteApp
Commencez par créer une collection. collection de Hello sert de conteneur pour vos applications et les utilisateurs. Chaque collection est basée sur une image ; vous pouvez créer votre propre image ou utiliser celle fournie avec votre abonnement. Pour ce didacticiel, nous utilisons une image d’évaluation de hello Office 2013 - il contient l’application hello que nous souhaitons tooshare.

1. Bonjour portail Azure, faites défiler vers le bas dans l’arborescence de navigation de gauche hello jusqu'à RemoteApp. Ouvrez cette page.
2. Cliquez sur **Créer une collection RemoteApp**.
3. Cliquez sur **Création rapide** et entrez un nom pour votre collection.
4. Sélectionnez hello région toouse toocreate votre collection. Pour une expérience optimale de hello, sélectionnez la région hello est le plus proche géographiquement emplacement toohello où vos utilisateurs auront accès à application hello. Par exemple, dans ce didacticiel, les utilisateurs de hello se situeront à Redmond, Washington. région Azure le plus proche de Hello est **ouest des États-Unis**.
5. Sélectionnez le plan de facturation hello souhaité toouse. plan de facturation base Hello place 16 utilisateurs sur une machine virtuelle Azure volumineux, tandis que le plan de facturation standard hello a 10 utilisateurs sur une machine virtuelle Azure large. Exemple général, plan de base hello fonctionne bien pour le workflow de type d’entrée de données. Pour une application de productivité, comme Office, vous souhaiteriez plan standard de hello.
6. Enfin, sélectionnez image d’Office 2013 Professionnel hello. Cette image contient les applications d’Office 2013. Rappel - cette image est uniquement valable pour les collections d'évaluation et les POC. Vous ne pouvez pas utiliser cette image dans une collection de production.
7. Cliquez à présent sur **Créer une collection RemoteApp**.

![Création d’une collection cloud dans RemoteApp](./media/remoteapp-anyapp/ra-anyappcreatecollection.png)

Cela démarre la création de votre collection, mais peut prendre jusqu'à une heure de tooan.

Maintenant vous êtes prêt tooadd vos utilisateurs.

## <a name="share-hello-app-with-users"></a>Application de hello partage avec des utilisateurs
Une fois que votre collection a été créée avec succès, il est temps toopublish accès toousers et ajoutez les utilisateurs de hello qui doivent avoir accès tooit.

Si vous avez accédé en s’éloignant de nœud d’Azure RemoteApp hello pendant la création de collection de hello, commencez par effectuer votre façon de nouveau tooit hello page d’accueil Azure.

1. Cliquez sur la collection hello vous avez créé des options supplémentaires tooaccess antérieure et configurer la collecte de hello.
   ![Une nouvelle collection cloud RemoteApp](./media/remoteapp-anyapp/ra-anyappcollection.png)
2. Sur hello **publication** , cliquez sur **publier** bas hello écran hello, puis cliquez sur **programmes du menu Démarrer de publication**.
   ![Publication d’un programme RemoteApp](./media/remoteapp-anyapp/ra-anyapppublish.png)
3. Sélectionnez applications hello toopublish à partir de la liste de hello. Dans notre cas, nous avons choisi Access. Cliquez sur **Terminé**. Attendez que la publication toofinish hello applications.
   ![Publication d’Access dans RemoteApp](./media/remoteapp-anyapp/ra-anyapppublishaccess.png)
4. Une fois que l’application hello a fini sa publication, rendez-vous sur toohello **accès utilisateur** onglet tooadd tous les utilisateurs de hello qui doivent accéder aux applications ; tooyour. Entrez les noms d’utilisateur (adresse e-mail) de vos utilisateurs, puis cliquez sur **Enregistrer**.

![Ajouter des utilisateurs tooRemoteApp](./media/remoteapp-anyapp/ra-anyappaddusers.png)

1. À présent, il est temps tootell vos utilisateurs sur ces nouvelles applications et comment tooaccess les. toodo, envoyer un e-mail pointant vers les URL de téléchargement du client Bureau à distance toohello.
   ![URL de téléchargement du client de Hello pour RemoteApp](./media/remoteapp-anyapp/ra-anyappurl.png)

## <a name="configure-access-tooaccess"></a>Configurer l’accès tooAccess
Certaines applications nécessitent une configuration supplémentaire après leur déploiement via RemoteApp. En particulier, pour l’accès, nous sommes toocreate continu un partage de fichiers sur Azure n’importe quel utilisateur peut accéder. (Si vous ne souhaitez pas toodo que vous pouvez créer un [collection hybride](remoteapp-create-hybrid-deployment.md) [au lieu de notre collection cloud] qui permet aux utilisateurs d’accéder aux fichiers et des informations sur votre réseau local.) Ensuite, nous devrons tootell notre toomap utilisateurs un lecteur local sur leur toohello ordinateur système de fichiers Azure.

Hello première partie en tant qu’administrateur de hello procéder. Dans un second temps, nous allons demander à vos utilisateurs de procéder à quelques étapes.

1. Commencez par l’interface de ligne de commande hello publication (cmd.exe). Bonjour **publication** onglet, sélectionnez **cmd**, puis cliquez sur **publier > programme de publication à l’aide du chemin d’accès**.
2. Entrez le nom hello de l’application hello et chemin d’accès hello. Dans notre cas, utilisez « Explorateur de fichiers » comme nom de hello et « % SYSTEMDRIVE%\windows\explorer.exe » en tant que chemin d’accès hello.
   ![Fichier de cmd.exe hello de publication.](./media/remoteapp-anyapp/ra-publishcmd.png)
3. Maintenant vous devez toocreate Azure [compte de stockage](../storage/common/storage-create-storage-account.md). Nous avons appelé le nôtre « accessstorage », par conséquent, choisissez un nom qui est significatif tooyou. (toomisquote Highlander, il peut y avoir qu’un seul « accessstorage ».) ![Compte de stockage Azure notre](./media/remoteapp-anyapp/ra-anyappazurestorage.png)
4. Revenez maintenant tooyour le tableau de bord afin d’obtenir du stockage de tooyour hello chemin d’accès (emplacement de point de terminaison). Vous allez l’utiliser dans peu de temps, veillez donc à le copier quelque part.
   ![chemin d’accès de compte de stockage Hello](./media/remoteapp-anyapp/ra-anyappstoragelocation.png)
5. Une fois que le compte de stockage hello a été créé, vous devez ensuite clé d’accès primaire hello. Cliquez sur **gérer les clés d’accès**et puis copie hello clé primaire.
6. Maintenant, définir le contexte de hello hello du compte de stockage et créer un nouveau partage de fichiers pour l’accès. Exécutez hello suivant d’applets de commande dans une fenêtre Windows PowerShell avec élévation de privilèges :
   
        $ctx=New-AzureStorageContext <account name> <account key>
        $s = New-AzureStorageShare <share name> -Context $ctx
   
    Par conséquent, pour notre part, il s’agit hello les applets de commande qu'est exécutée :
   
        $ctx=New-AzureStorageContext accessstorage <key>
        $s = New-AzureStorageShare <share name> -Context $ctx

À présent, il s’agit de désactiver de l’utilisateur hello. Tout d’abord, demandez à vos utilisateurs d’installer un [client RemoteApp](remoteapp-clients.md). Ensuite, les utilisateurs de hello doivent toomap un lecteur à partir de leur toothat compte Azure fichier partage que vous avez créé et ajouter leur accès aux fichiers. Voici comment ces derniers doivent procéder :

1. Dans le client de RemoteApp hello, hello d’accès aux applications publiées. Démarrer le programme de cmd.exe hello.
2. Exécutez hello suivant commande toomap un lecteur de votre ordinateur toohello partage de fichiers :
   
        net use z: \\<accountname>.file.core.windows.net\<share name> /u:<user name> <account key>
   
    Si vous définissez hello **/ persistent** paramètre tooyes, hello lecteur mappé persistera à travers les sessions.
3. Maintenant, lancez application de l’Explorateur de fichiers hello de RemoteApp. Copiez les fichiers d’accès souhaité toouse dans le partage de fichiers toohello hello application partagée.
   ![Ajout de fichiers Access dans un partage Azure](./media/remoteapp-anyapp/ra-anyappuseraccess.png)
4. Enfin, ouvrez Access et ouvrez une base de données hello que vous venez de partager. Vous devez voir vos données dans Access en cours d’exécution à partir du cloud de hello.
   ![Une base de données réel en cours d’exécution à partir du cloud de hello](./media/remoteapp-anyapp/ra-anyapprunningaccess.png)

Vous pouvez désormais utiliser Access sur n’importe lequel de vos appareils. Veillez simplement à installer un client RemoteApp.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous maîtrisez la création d’une collection, essayez de créer une [collection utilisant Office 365](remoteapp-tutorial-o365anywhere.md). Vous pouvez également créer une [collection hybride ](remoteapp-create-hybrid-deployment.md)ayant accès à votre réseau local.

<!--Image references-->

