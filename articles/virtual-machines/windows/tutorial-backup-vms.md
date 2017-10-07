---
title: aaaBackup les machines virtuelles Windows Azure | Des documents Microsoft
description: "Protégez vos machines virtuelles Windows en les sauvegardant à l’aide de Sauvegarde Azure."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a>Sauvegarde de machines virtuelles Windows dans Azure

Vous pouvez protéger vos données en effectuant des sauvegardes à intervalles réguliers. Azure Backup crée des points de récupération stockés dans des coffres de récupération géoredondants. Lorsque vous restaurez à partir d’un point de récupération, vous pouvez restaurer hello toute machine virtuelle ou des fichiers spécifiques. Cet article explique comment toorestore un seul fichier tooa machine virtuelle exécutant Windows Server et IIS. Si vous n’avez pas encore un toouse de machine virtuelle, vous pouvez en créer un à l’aide de hello [démarrage rapide de Windows](quick-create-portal.md). Ce didacticiel vous explique comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer une sauvegarde de machine virtuelle
> * Planifier une sauvegarde quotidienne
> * Restaurer un fichier à partir d’une sauvegarde




## <a name="backup-overview"></a>Présentation de la sauvegarde

Hello service Azure Backup lorsqu’une opération de sauvegarde, il déclenche hello extension de sauvegarde tootake un instantané de point-à-temps. Hello service Azure Backup utilise hello _VMSnapshot_ extension. extension de Hello est installée au cours de la première sauvegarde de machine virtuelle hello si hello machine virtuelle est en cours d’exécution. Si hello machine virtuelle ne fonctionne pas, hello service de sauvegarde prend un instantané de hello stockage sous-jacent (dans la mesure où aucune écriture de l’application se produire lors de la machine virtuelle est arrêtée de hello).

Lorsque vous prenez un instantané de machines virtuelles Windows, service de sauvegarde hello coordonne hello Volume Shadow Copy Service (VSS) tooget un instantané cohérent des disques de l’ordinateur virtuel de hello. Une fois que hello service Azure Backup prend un instantané de hello, données de hello sont transférées toohello coffre. l’efficacité toomaximize, hello service identifie et transfère uniquement les blocs de hello de données qui ont été modifiés depuis la sauvegarde précédente de hello.

Lorsque le transfert de données hello est terminé, les instantanés hello sont supprimé et un point de récupération est créé.


## <a name="create-a-backup"></a>Création d'une sauvegarde
Créer une simple planifiée quotidienne sauvegarde tooa coffre Recovery Services. 

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Dans le menu hello hello gauche, sélectionnez **virtuels**. 
3. À partir de la liste de hello, sélectionnez un tooback de machine virtuelle.
4. Dans Panneau de machine virtuelle hello, Bonjour **paramètres** , cliquez sur **sauvegarde**. Hello **Active la sauvegarde** panneau s’ouvre.
5. Dans **de coffre Recovery Services**, cliquez sur **nouvel** et fournir le nom hello pour le coffre hello. Un nouvel archivage est créé dans hello même groupe de ressources et l’emplacement en tant que machine virtuelle de hello.
6. Cliquez sur **Stratégie de sauvegarde**. Pour cet exemple, conservez les valeurs par défaut hello et cliquez sur **OK**.
7. Sur hello **Active la sauvegarde** panneau, cliquez sur **activez la sauvegarde**. Cette opération crée une sauvegarde quotidienne selon une planification par défaut hello.
10. toocreate un point de récupération initial sur hello **sauvegarde** cliquez sur le panneau **sauvegarder maintenant**.
11. Sur hello **sauvegarde maintenant** panneau, cliquez sur icône du calendrier hello, utilisez Bonjour calendrier contrôle tooselect Bonjour dernier jour de ce point de récupération est conservé, puis cliquez sur **sauvegarde**.
12. Bonjour **sauvegarde** panneau pour votre machine virtuelle, vous verrez nombre hello de points de récupération qui sont terminées.

    ![Points de récupération](./media/tutorial-backup-vms/backup-complete.png)
    
première sauvegarde de Hello prend environ 20 minutes. Continuer toohello la partie suivante de ce didacticiel, une fois la sauvegarde terminée.

## <a name="recover-a-file"></a>Récupérer un fichier

Si vous supprimez ou rendre le fichier tooa des modifications, vous pouvez utiliser le fichier de récupération de fichier toorecover hello votre coffre de sauvegarde. Récupération de fichiers utilise un script qui s’exécute sur hello machine virtuelle, point de récupération toomount hello en tant que lecteur local. Ces lecteurs restera montés pendant 12 heures, afin que vous pouvez copier les fichiers de point de récupération hello et restaurez-les toohello machine virtuelle.  

Dans cet exemple, nous montrons comment toorecover hello fichier image qui est utilisée dans la page web de hello par défaut pour IIS. 

1. Ouvrez un navigateur et se connecter à adresse IP de toohello de page IIS hello VM tooshow hello par défaut.

    ![Page web IIS par défaut](./media/tutorial-backup-vms/iis-working.png)

2. Se connecter toohello machine virtuelle.
3. Sur la machine virtuelle de hello, ouvrez **l’Explorateur de fichiers** et de naviguer too\inetpub\wwwroot et supprimer le fichier de hello **iisstart.png**.
4. Sur votre ordinateur local, l’actualisation hello navigateur toosee qui hello image sur la page d’IIS par défaut hello a disparu.

    ![Page web IIS par défaut](./media/tutorial-backup-vms/iis-broken.png)

5. Sur votre ordinateur local, ouvrez un nouvel onglet et un accédez Bonjour Bonjour [portail Azure](https://portal.azure.com).
6. Dans le menu hello hello gauche, sélectionnez **virtuels** et sélectionnez hello VM écran hello liste.
8. Dans Panneau de machine virtuelle hello, Bonjour **paramètres** , cliquez sur **sauvegarde**. Hello **sauvegarde** panneau s’ouvre. 
9. Dans le menu hello haut hello du Panneau de hello, sélectionnez **récupération de fichier**. Hello **récupération de fichier** panneau s’ouvre.
10. Dans **étape 1 : sélectionnez le point de récupération**, sélectionnez un point de récupération à partir de hello de liste déroulante.
11. Dans **étape 2 : télécharger le script toobrowse et récupérer les fichiers**, cliquez sur hello **télécharger le fichier exécutable** bouton. Enregistrer hello fichier tooyour **télécharge** dossier.
12. Sur votre ordinateur local, ouvrez **l’Explorateur de fichiers** et accédez tooyour **télécharge** dossier et copie hello téléchargé un fichier .exe. nom de fichier Hello sera être préfixé par votre nom d’ordinateur virtuel. 
13. Sur votre machine virtuelle (sur hello connexion RDP) Coller toohello de fichier .exe hello bureau de votre machine virtuelle. 
14. Accédez bureau toohello de votre machine virtuelle et double-cliquez sur hello .exe. Vous lancez une invite de commandes et puis montez le point de récupération hello en tant que vous pouvez accéder à un partage de fichiers. Quand elle est terminée création hello partage, tapez **q** tooclose hello invite de commandes.
15. Sur votre machine virtuelle, ouvrez **l’Explorateur de fichiers** et accédez de lettre de lecteur toohello qui a été utilisé pour le partage de fichiers hello.
16. Accédez too\inetpub\wwwroot et copie **iisstart.png** à partir du fichier de hello partager et collez-le dans \inetpub\wwwroot. Par exemple, copiez F:\inetpub\wwwroot\iisstart.png et collez-le dans le fichier de hello toorecover c:\inetpub\wwwroot.
17. Sur votre ordinateur local, ouvrez l’onglet de navigateur hello où vous êtes connecté adresse toohello de hello VM écran hello IIS par défaut de la page. Appuyez sur CTRL + F5 page du navigateur toorefresh hello. Vous devez maintenant voir que hello image a été restaurée.
18. Sur votre ordinateur local, revenir en arrière toohello onglet du navigateur pour hello portail Azure et dans **étape 3 : démontage de disques de hello après la récupération** cliquez sur hello **démontage de disques** bouton. Si vous oubliez toodo cette étape, point de montage toohello hello connexion est automatiquement fermée après 12 heures. Après les 12 heures, vous devez toodownload une nouvelle toocreate de script un nouveau point de montage.


## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Créer une sauvegarde de machine virtuelle
> * Planifier une sauvegarde quotidienne
> * Restaurer un fichier à partir d’une sauvegarde

Avance toohello toolearn de didacticiel suivant sur l’analyse des ordinateurs virtuels.

> [!div class="nextstepaction"]
> [Surveiller les machines virtuelles](tutorial-monitoring.md)









