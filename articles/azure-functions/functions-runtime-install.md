---
title: aaaAzure fonctions Runtime Installation | Documents Microsoft
description: Comment tooInstall hello Azure fonctions Runtime
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a>Installer hello Azure en version préliminaire fonctions Runtime

Si vous souhaitez que la version préliminaire de Azure fonctions Runtime tooinstall hello, procédez comme suit :

1. Vérifiez que votre ordinateur passe requise hello
1. Télécharger hello [le programme d’installation de Azure fonctions Runtime Preview](https://aka.ms/azafr). 
1. Installez hello Azure fonctions Runtime preview
1. Configuration de hello complète de l’aperçu du Runtime de fonctions Azure hello

## <a name="prerequisites"></a>Composants requis

Avant d’installer de version préliminaire du Runtime de fonctions Azure hello, vous devez disposer de hello :

1. Un ordinateur exécutant Microsoft Windows Server 2016 ou Windows 10 Creators Update (édition Professionnelle ou Entreprise).
1. Une instance SQL Server en cours d’exécution au sein de votre réseau.  La version minimale requise est SQL Server Express.

## <a name="install-hello-azure-functions-runtime-preview"></a>Installer hello Azure en version préliminaire fonctions Runtime

le programme d’installation de Hello Azure fonctions Runtime preview vous guide tout au long des installation hello d’aperçu du Runtime de fonctions Azure hello Management et les rôles de travail.  Il est possible tooinstall hello gestion et le rôle de travail sur hello même ordinateur.  Toutefois, lorsque vous ajoutez des fonctions, vous devez déployer plusieurs rôles de travail sur tooscale en mesure de machines supplémentaires toobe vos fonctions sur plusieurs threads de travail.

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a>Installer hello gestion et le rôle de travail sur hello même ordinateur

1. Exécutez hello le programme d’installation de Azure fonctions Runtime Preview.

    ![Programme d’installation de la version préliminaire du runtime d’Azure Functions][1]

1. **Cliquez sur Suivant** avance au-delà de hello première étape du programme d’installation Bonjour
1. Une fois que vous avez lu les termes du contrat de hello Hello **CLUF**, **hello case à cocher** termes de hello tooaccept et **cliquez sur Suivant** tooadvance.
1. À présent, sélectionnez hello rôles lequel tooinstall sur cet ordinateur **rôle de fonctions de gestion** et/ou **rôle de travail des fonctions** et **cliquez sur Suivant**

    ![Programme d’installation de la version préliminaire du runtime d’Azure Functions - Sélection du rôle][3]

    > [!NOTE]
    > Vous pouvez installer hello **rôle de travail des fonctions** sur nombreux autres toodo machines, suivez ces instructions, puis sélectionnez uniquement **rôle de travail des fonctions** dans le programme d’installation hello.

1. **Cliquez sur Suivant** toohave hello **le programme d’installation de Azure fonctions Runtime** installer sur votre ordinateur.
1. Une fois que le programme d’installation complète hello lancera hello **outil de Configuration d’exécution Azure fonctions**.

    ![Programme d’installation de la version préliminaire du runtime d’Azure Functions terminé][5]

    > [!NOTE]
    > Si vous installez sur **Windows 10** et hello **conteneur** fonctionnalité a été précédemment désactivée, hello **Azure fonctions Runtime** programme d’installation vous invite tooreboot installation de votre hello toocomplete de machine.

## <a name="configure-hello-azure-functions-runtime"></a>Configurer hello Azure fonctions Runtime

hello toocomplete installation Azure fonctions Runtime vous devez effectuer la configuration de hello.

1. Hello **outil de Configuration du Runtime Azure fonctions** montre les rôles installés sur votre ordinateur.

    ![Outil de configuration de la version préliminaire du runtime d’Azure Functions terminé][6]

1. Cliquez sur hello **base de données** , entrez hello **détails de connexion pour votre Instance de SQL Server** et **cliquez sur Appliquer**.  Cela est nécessaire dans l’ordre toohello Azure fonctions Runtime toocreate un Bonjour de toosupport Runtime de base de données.
    
    ![Configuration de la base de données de la version préliminaire du runtime d’Azure Functions][7]

1. Cliquez sur hello **informations d’identification** onglet.  Dans cet écran, vous devez créer deux nouveaux jeux d’informations d’identification à utiliser avec un partage de fichiers pour l’hébergement de toutes vos Azure Functions.  **Spécifiez le nom d’utilisateur et mot de passe** combinaisons pour hello **propriétaire du partage de fichiers** et pourquoi **utilisateur du partage de fichiers** et cliquez sur **appliquer**.

    ![Informations d’identification de la version préliminaire du runtime d’Azure Functions][8]

1. Cliquez sur hello **partage de fichiers** onglet.  Dans cet écran, vous devez spécifier les détails de hello Hello **emplacement du partage de fichiers**.  Celui-ci peut être créé pour vous ou vous pouvez utiliser un partage de fichier existant, puis cliquez sur **Appliquer**.  Si vous sélectionnez un nouvel emplacement de partage de fichiers, vous devez spécifier un répertoire pour une utilisation par hello Azure fonctions Runtime.
    
    ![Partage de fichiers de la version préliminaire du runtime d’Azure Functions][9]

1. Cliquez sur hello **IIS** onglet.  Cet onglet affiche les détails de hello de hello des sites Web dans IIS qui hello Azure fonctions Runtime Installation va créer.  **Cliquez sur Appliquer** toocomplete.

    ![IIS de la version préliminaire du runtime d’Azure Functions][10]

1. Cliquez sur hello **Services** onglet.  Cet onglet affiche l’état hello de services de hello dans votre installation de l’exécution de fonctions d’Azure.  Si, après avoir hello de la configuration initiale **Service d’Activation de Azure fonctions hôte** ne fonctionne pas cliquez **démarrer le Service**

    ![Configuration de la version préliminaire du runtime d’Azure Functions terminée][11]

1. Enfin Parcourir toohello **Azure fonctions Runtime portail** en tant que`https://<machinename>/`

    ![Portail du runtime d’Azure Functions en version préliminaire][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png