---
title: comptes de stockage Azure pile aaaManage | Documents Microsoft
description: "Découvrez comment toofind, gérer, restaurer et récupérer des comptes de stockage Azure pile"
services: azure-stack
documentationcenter: 
author: AniAnirudh
manager: darmour
editor: 
ms.assetid: 627d355b-4812-45cb-bc1e-ce62476dab34
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/6/2017
ms.author: anirudha
ms.openlocfilehash: 350c92d6b5ce9b1582ede0256c4d3d23bdd94901
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-in-azure-stack"></a>Gérer les comptes de stockage dans Azure Stack
Découvrez comment toomanage les comptes de stockage dans Azure pile toofind, restaurer et récupérer de la capacité de stockage en fonction des besoins de l’entreprise.

## <a name="find"></a>Rechercher un compte de stockage
liste Hello de comptes de stockage dans la région de hello peut être affichée dans la pile Azure par :

1. Dans un navigateur Internet, accédez à https://adminportal.local.azurestack.external.
2. Se connecter toohello portail d’administration Azure pile comme un opérateur cloud (en utilisant les informations d’identification que vous avez fourni pendant le déploiement)
3. Sur le tableau de bord par défaut hello – recherche hello **gestion de la région** liste et cliquez sur la zone hello tooexplore. Par exemple **(local**).
   
   ![](media/azure-stack-manage-storage-accounts/image1.png)
4. Sélectionnez **stockage** de hello **fournisseurs de ressources** liste.
   
   ![](media/azure-stack-manage-storage-accounts/image2.png)
5. Désormais, dans Panneau d’administrateur de fournisseur de ressources de stockage de hello – défiler hello **comptes de stockage** onglet et cliquez dessus.
   
   ![](media/azure-stack-manage-storage-accounts/image3.png)
   
   page résultante de Hello est liste hello de comptes de stockage dans cette région.
   
   ![](media/azure-stack-manage-storage-accounts/image4.png)

Par défaut, hello 10 premiers comptes sont affichés. Vous pouvez choisir toofetch plus en cliquant sur hello **davantage** lien en bas de hello de liste de hello.

OU

Si vous êtes intéressé par un compte de stockage spécifique – vous pouvez **filtre et fetch hello comptes appropriés** uniquement.


**toofilter pour les comptes :**

1. Cliquez sur **filtre** haut hello du Panneau de hello.
2. Dans Panneau de filtre hello, il vous permet de toospecify **nom de compte**, **ID d’abonnement** ou **état** liste de hello ajuster les toofine de stockage comptes toobe affiché. Utilisez-les pour filtrer selon vos besoins.
3. Cliquez sur **Update**. liste de Hello doit actualiser en conséquence.
   
    ![](media/azure-stack-manage-storage-accounts/image5.png)
4. filtre de hello tooreset : cliquez sur **filtre**, effacer les sélections et mettre à jour.

zone de texte Rechercher Hello (en haut de hello du Panneau de liste de comptes de stockage hello) vous permet de mettre en surbrillance le texte hello sélectionné dans la liste hello de comptes. Cela est très pratique dans les cas de hello lors de l’id ou nom complet de hello n’est pas facilement disponible.

Vous pouvez utiliser du texte libre ici, retrouvez toohelp compte hello vous intéressez.

![](media/azure-stack-manage-storage-accounts/image6.png)

## <a name="look-at-account-details"></a>Accéder aux détails du compte
Une fois que vous avez localisé comptes hello que vous intéressez, vous pouvez cliquer hello compte particulier tooview certains détails. Un nouveau panneau s’ouvre avec les détails du compte hello telles que : hello du type de compte de hello, heure de création, l’emplacement, etc..

![](media/azure-stack-manage-storage-accounts/image7.png)

## <a name="recover-a-deleted-account"></a>Récupérer un compte supprimé
Vous pouvez être dans une situation où vous avez besoin de toorecover un compte supprimé.

Dans la pile d’Azure, il existe un moyen très simple de toodo qui :

1. Parcourir la liste de comptes de stockage toohello. Pour plus d’informations, consultez [Rechercher un compte de stockage](#find) dans cette rubrique.
2. Recherchez ce compte dans la liste de hello. Vous devrez peut-être toofilter.
3. Vérifiez hello *état* du compte de hello. Il doit être **Supprimé**.
4. Cliquez sur le compte hello qui ouvre le panneau des détails du compte hello.
5. Au-dessus de ce panneau, recherchez hello **récupérer** bouton et cliquez dessus.
6. Cliquez sur **Oui** tooconfirm.
   
   ![](media/azure-stack-manage-storage-accounts/image8.png)
7. récupération de Hello est maintenant en *traiter... Patientez* pour obtenir une indication si elle a réussi.
   Vous pouvez également cliquez sur hello « cloche » en haut hello du portail hello pour afficher des indications de progression.
   
   ![](media/azure-stack-manage-storage-accounts/image9.png)
   
   Une fois hello récupérée compte est correctement synchronisé, il peut être utilisé à nouveau.

### <a name="some-gotchas"></a>Quelques astuces
* Votre compte supprimé affiche un état **hors conservation**.
  
  Cela signifie que le compte de hello supprimé a dépassé la période de rétention hello et qu’il ne peut pas être récupérée.
* Votre compte supprimé n’affiche pas dans la liste des comptes hello.
  
  Cela peut signifier que les comptes de hello supprimé a déjà été par le garbage collecté. Dans ce cas, il ne peut pas être récupéré. Consultez [Récupérer de la capacité](#reclaim) dans cette rubrique.

## <a name="set-hello-retention-period"></a>Définir la période de rétention hello
définition de période de rétention Hello permet un toospecify d’opérateur de nuage une période en jours (entre 0 et 9 999 jours) pendant le n’importe quel compte supprimé peut potentiellement être récupéré. Hello période de rétention par défaut a la valeur too15 jours. Hello valeur trop « 0 » signifie que n’importe quel compte supprimé est immédiatement en dehors de la rétention et marqué pour un garbage collection périodique.

**période de rétention toochange hello :**

1. Dans un navigateur Internet, accédez à https://adminportal.local.azurestack.external.
2. Se connecter toohello portail d’administration Azure pile comme un opérateur cloud (en utilisant les informations d’identification que vous avez fourni pendant le déploiement)
3. Sur le tableau de bord par défaut hello – recherche hello **gestion de la région** liste et cliquez sur la région de hello souhaité tooexplore – par exemple **(local**).
4. Sélectionnez **stockage** de hello **fournisseurs de ressources** liste.
5. Cliquez sur **paramètres** au panneau de configuration hello hello tooopen supérieur.
6. Cliquez sur **Configuration** puis modifiez la valeur de période de rétention hello.

   Définir hello nombre de jours et enregistrez-le.
   
   Cette valeur est prise en compte immédiatement et est appliquée à toute votre région.

   ![](media/azure-stack-manage-storage-accounts/image10.png)

## <a name="reclaim"></a>Récupérer de la capacité
Un des effets secondaires hello d’avoir une période de rétention est qu’un compte supprimé continue tooconsume capacité jusqu'à ce qu’il s’agit de la période de rétention hello. Comme un cloud opérateur, vous devrez peut-être un Bonjour tooreclaim de façon supprimé espace du compte même si la période de rétention hello n’a pas encore expiré.

Vous pouvez récupérer de la capacité à l’aide du portail de hello ou PowerShell.

**capacité de tooreclaim à l’aide du portail de hello :**
1. Accédez à panneau de comptes de stockage toohello. Consultez [Rechercher un compte de stockage](#find).
2. Cliquez sur **récupérer de l’espace** haut hello du Panneau de hello.
3. Lire le message de type hello et puis cliquez sur **OK**.

    ![](media/azure-stack-manage-storage-accounts/image11.png)
4. Attendez l’icône représentant une cloche de réussite notification voir hello sur le portail hello.

    ![](media/azure-stack-manage-storage-accounts/image12.png)
5. Actualisez la page comptes de stockage hello. les comptes Hello supprimé n’apparaissent plus dans la liste de hello, car ils ont été purgées.

Vous pouvez également utiliser la période de rétention PowerShell tooexplicitly remplacement hello et récupérer immédiatement de la capacité.

**capacité de tooreclaim à l’aide de PowerShell :**   

1. Vérifiez qu’Azure PowerShell est installé et configuré. Si ce n’est pas le cas, utilisez hello suivant les instructions : 
   * tooinstall hello version la plus récente d’Azure PowerShell et associez-le à votre abonnement Azure, consultez [comment tooinstall et configurer Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).
   Pour plus d’informations sur les applets de commande Azure Resource Manager, consultez [Utilisation d’Azure PowerShell avec Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767).
2. Exécutez hello suivant l’applet de commande :

> [!NOTE]
> Si vous exécutez cette applet de commande vous supprimez définitivement le compte de hello et son contenu. Il n’est pas récupérable. Utilisez cette option avec précaution.


        Clear-ACSStorageAccount -ResourceGroupName system.local -FarmName <farm ID>


Pour plus d’informations, consultez trop[documentation de pile d’Azure powershell.](https://msdn.microsoft.com/library/mt637964.aspx)
 

## <a name="migrate-a-container"></a>Migrer un conteneur
En raison de l’utilisation du stockage toouneven par les locataires, un opérateur cloud peut trouver une ou plus sous-jacent locataire partages à l’aide de davantage d’espace que d’autres. Si cela se produit, opérateur de cloud hello peut essayer de toofree l’espace sur le partage d’accentuée hello en effectuant une migration manuellement certains partage tooanother de conteneurs blob. 

Vous devez utiliser PowerShell toomigrate conteneurs.
> [!NOTE]
>La migration de conteneurs d’objets blob ne prend pas en charge la migration dynamique et est actuellement une opération hors connexion. Pendant la migration et qu’elle soit terminée hello sous-jacente des objets BLOB que le conteneur ne peut pas être utilisés et sont « hors connexion ». 

**conteneurs de toomigrate à l’aide de PowerShell :**

1. Vérifiez qu’Azure PowerShell est installé et configuré. Si ce n’est pas le cas, utilisez hello suivant les instructions :
    * tooinstall hello version la plus récente d’Azure PowerShell et associez-le à votre abonnement Azure, consultez [comment tooinstall et configurer Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/). Pour plus d’informations sur les applets de commande Azure Resource Manager, consultez [Utilisation d’Azure PowerShell avec Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767).
2. Obtenir le nom de la batterie hello : 
      
      `$farm = Get-ACSFarm -ResourceGroupName system.local`
3. Obtenir les partages hello : 

   `$shares = Get-ACSShare -ResourceGroupName system.local -FarmName $farm.FarmName`

4. Obtenir les conteneurs hello pour un partage donné. Notez que les paramètres Count et Intent sont facultatifs :
            
   `$containers = Get-ACSContainer -ResourceGroupName system.local -FarmName $farm.FarmName -ShareName $shares[0].ShareName -Count 4 -Intent Migration`  

   Examinez ensuite $containers :

   `$containers`

    ![](media/azure-stack-manage-storage-accounts/image13.png)
5. Obtenir les partages de destination meilleures hello pour la migration de conteneur hello :

    `$destinationshares= Get-ACSSharesForMigration  -ResourceGroupName system.local -FarmName $farm.farmname -SourceShareName $shares[0].ShareName`

    Examinez ensuite $destinationshares :

    `$destinationshares`

    ![](media/azure-stack-manage-storage-accounts/image14.png)
6. Lancer la migration d’un conteneur, notez que ce étant une implémentation asynchrone, une boucle tous les conteneurs dans un état hello partage et du suivi à l’aide des id de tâche retournée de hello.

    `$jobId = Start-ACSContainerMigration -ResourceGroupName system.local -FarmName $farm.farmname -ContainerToMigrate $containers[1] -DestinationShareUncPath $destinationshares.UncPath`

    Examiner ensuite $jobId :

   ```
   $jobId
   d1d5277f-6b8d-4923-9db3-8bb00fa61b65
   ```
7. Vérifiez le statut de tâche de migration hello par son id de tâche. Après la migration de conteneur hello, MigrationStatus est défini trop « terminé ».

    `Get-ACSContainerMigrationStatus -ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image15.png)

8. Vous pouvez annuler une tâche de migration en cours d’exécution. Il s’agit à nouveau d’une opération asynchrone, qui peut être suivie en utilisant $jobid :

    `Stop-ACSContainerMigration-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId-Verbose`

    ![](media/azure-stack-manage-storage-accounts/image16.png)

    Vous pouvez réactiver état hello d’annulation de migration hello :

    `Get-ACSContainerMigrationStatus-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image17.png)




  
  