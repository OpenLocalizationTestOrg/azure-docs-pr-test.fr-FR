---
title: "aaaConnect tooSQL de base de données à l’aide de SQL Server Management Studio dans Azure RemoteApp | Documents Microsoft"
description: "Utilisez ce didacticiel toolearn comment toouse SQL Server Management Studio dans Azure RemoteApp pour la sécurité et les performances lors de la connexion tooSQL de base de données"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a>Utilisez SQL Server Management Studio dans Azure RemoteApp tooconnect tooSQL base de données

> [!IMPORTANT]
> Azure RemoteApp n’est plus disponible. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
>

## <a name="introduction"></a>Introduction
Ce didacticiel vous montre comment toouse SQL Server Management Studio (SSMS) dans Azure RemoteApp tooconnect tooSQL base de données. Il vous guide tout au long des processus de hello de configuration SQL Server Management Studio dans Azure RemoteApp, explique les avantages de hello et montre les fonctionnalités de sécurité que vous pouvez utiliser dans Azure Active Directory.

**Estimation du temps toocomplete :** 45 minutes

## <a name="ssms-in-azure-remoteapp"></a>SSMS dans Azure RemoteApp
Azure RemoteApp est un service RDS d’Azure, qui fournit des applications. Vous pouvez obtenir plus d’informations sur ce service ici : [Qu’est-ce que RemoteApp ?](../remoteapp/remoteapp-whatis.md)

En cours d’exécution dans Azure RemoteApp donne SSMS vous hello même expérience en exécutant SSMS localement.

![Capture d’écran illustrant SSMS en cours d’exécution dans Azure RemoteApp][1]

## <a name="benefits"></a>Avantages
Il existe de nombreux avantages toousing SSMS dans Azure RemoteApp, y compris :

* Le port 1433 sur le serveur SQL Azure n’a pas de toobe exposé en externe (en dehors d’Azure).
* Aucun tookeep besoin, ajout et suppression d’adresses IP dans le pare-feu de serveur SQL Azure hello.
* Toutes les connexions Azure RemoteApp ont lieu via HTTPS sur le port 443 à l’aide du protocole RDP (Remote Desktop Protocol) chiffré.
* SSMS est multi-utilisateur et évolutif.
* Il existe un gain de performances de l’utilisation de SSMS Bonjour même région que hello de base de données SQL.
* Vous pouvez auditer l’utilisation d’Azure RemoteApp avec l’édition Premium d’Azure Active Directory qui a des rapports d’activité utilisateur hello.
* Vous pouvez activer l’authentification multifacteur (MFA).
* Accès SSMS n’importe où lorsque vous utilisez une de hello clients pris en charge Azure RemoteApp qui inclut iOS, Android, Mac, Windows Phone et les PC Windows.

## <a name="create-hello-azure-remoteapp-collection"></a>Créer la collection de hello Azure RemoteApp
Voici votre collection Azure RemoteApp avec SSMS hello étapes toocreate :

### <a name="1-create-a-new-windows-vm-from-image"></a>1. Créer une machine virtuelle Windows à partir d’une image
Utilisez hello Image « Windows Server à distance Bureau Session hôte Windows Server 2012 R2 » à partir de hello galerie toomake votre nouvelle machine virtuelle.

### <a name="2-install-ssms-from-sql-express"></a>2. Installer SSMS à partir de SQL Express
Accédez à hello nouvelle machine virtuelle et de parcourir la page de téléchargement toothis : [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)

Il existe un téléchargement de tooonly option SSMS. Après le téléchargement, allez dans le répertoire d’installation hello et exécuter le programme d’installation tooinstall SSMS.

Vous devez également tooinstall SQL Server 2014 Service Pack 1. Vous pouvez le télécharger ici : [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)

SQL Server 2014 Service Pack 1 inclut des fonctionnalités essentielles pour l’utilisation de la base de données SQL Azure.

### <a name="3-run-validate-script-and-sysprep"></a>3. Exécuter le script de validation et Sysprep
Sur hello bureau Hello machine virtuelle est un script PowerShell appelé Validate. Exécutez-le en double-cliquant dessus. Il vérifie que hello machine virtuelle est prête toobe utilisé pour l’hébergement à distance des applications. Lors de la vérification est terminée, il demande toorun sysprep - choisissez toorun il.

Quand sysprep se termine, il s’arrêtera hello machine virtuelle.

toolearn savoir plus sur la création d’une image Azure RemoteApp, consultez : [comment toocreate un modèle RemoteApp de l’image dans Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)

### <a name="4-capture-image"></a>4. Capturer l’image
Lorsque hello machine virtuelle est arrêtée, recherchez-le dans le portail actuel de hello et capturer.

toolearn savoir plus sur la capture d’une image, consultez [capturer une image d’une machine virtuelle de Microsoft Azure créée avec le modèle de déploiement classique de hello](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="5-add-tooazure-remoteapp-template-images"></a>5. Ajouter des images de modèle RemoteApp tooAzure
Bonjour section Azure RemoteApp du portail en cours de hello, onglet des Images de modèle toohello, cliquez sur Ajouter. Dans la boîte de hello, sélectionnez « Importer une image à partir de votre bibliothèque de Machines virtuelles », puis choisissez hello Image que vous venez de créer.

### <a name="6-create-cloud-collection"></a>6. Créer une collection cloud
Dans le portail actuel hello, créez une nouvelle Collection de Cloud de RemoteApp Azure. Choisissez hello Image de modèle que vous venez d’importer avec SSMS installé dessus.

![Créer une collection cloud][2]

### <a name="7-publish-ssms"></a>7. Publier SSMS
Sur la publication d’onglet de votre nouvelle collection cloud, cliquez sur Publier une application à partir de hello hello Menu Démarrer, puis choisissez SSMS à partir de la liste de hello.

![Publier une application][5]

### <a name="8-add-users"></a>8. Ajouter des utilisateurs
Sur l’onglet de l’accès utilisateur hello, vous pouvez sélectionner les utilisateurs de hello qui auront accès toothis Azure RemoteApp ensemble qui inclut uniquement les SSMS.

![Ajouter un utilisateur][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a>9. Installer l’application de client hello Azure RemoteApp
Vous pouvez télécharger et installer un client Azure RemoteApp ici : [Télécharger | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)

## <a name="configure-azure-sql-server"></a>Configuration d’Azure SQL Server
Hello uniquement de la configuration requise est tooensure Services Azure est activée pour le pare-feu hello. Si vous utilisez cette solution, puis il est inutile tooadd toutes les adresses IP tooopen le pare-feu hello. le trafic réseau Hello autorisé toohello SQL Server est à partir d’autres services Azure.

![Autoriser dans Azure][4]

## <a name="multi-factor-authentication-mfa"></a>Multi-Factor Authentication (MFA)
La MFA peut être activée spécifiquement pour cette application. Accédez à onglet d’Applications toohello d’Azure Active Directory. Vous trouverez une entrée correspondant à Microsoft Azure RemoteApp. Si vous cliquez sur cette application, puis configurez, vous verrez la page hello ci-dessous vous permet d’activer l’authentification Multifacteur pour cette application.

![Activer la MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a>Auditer l’activité utilisateur avec Azure Active Directory Premium
Si vous n’avez pas d’Azure AD Premium, vous devez tooturn il sur dans hello section des licences de votre annuaire. Premium est activé, vous pouvez assigner des utilisateurs au niveau du toohello Premium.

Lorsque vous passez tooa utilisateur dans Azure Active Directory, vous pouvez ensuite accéder toohello activité onglet toosee connexion informations tooAzure RemoteApp.

## <a name="next-steps"></a>Étapes suivantes
Après avoir effectué hello toutes les étapes ci-dessus, vous être en mesure de toorun hello Azure RemoteApp client et reconnectez-vous avec un utilisateur affecté. Vous n’aurez SSMS comme l’un de vos applications, et vous pouvez l’exécuter comme vous le feriez s’il était installé sur votre ordinateur avec tooAzure accéder à SQL server.

Pour plus d’informations sur la façon dont toomake hello tooSQL de connexion de base de données, consultez [connecter tooSQL de base de données avec SQL Server Management Studio et exécuter un exemple de requête T-SQL](sql-database-connect-query-ssms.md).

C’est tout pour le moment. Vous n’avez plus qu’à l’utiliser !

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png