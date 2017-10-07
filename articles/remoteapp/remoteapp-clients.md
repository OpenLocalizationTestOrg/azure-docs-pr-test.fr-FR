---
title: "aaaAccessing vos applications à partir de n’importe quel appareil | Documents Microsoft"
description: "Découvrez quels clients sont pris en charge pour Azure RemoteApp et comment tooaccess vos applications."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: fb7bd17d-7aa8-43fd-9278-f96e0e9308e4
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 15985b40d870e3155d4132063bf5b9677ff9afed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a>Accès à vos applications dans Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Une des beautés hello d’Azure RemoteApp est que vous pouvez accéder à des applications à partir d’un de vos périphériques. Mieux encore, vous pouvez commencer à travailler sur un appareil et ensuite une transition transparente tooa deuxième appareil et reprendre là où vous l’avez laissé. tooget a démarré, vous devez client de toodownload hello approprié pour votre appareil et connectez-vous au service de toohello.

Dans cette rubrique, nous verrons clients hello actuellement pris en charge et comment toodownload les avant de voir comment toosign dans tooRemoteApp de chacun des clients de hello.

## <a name="supported-clients"></a>Clients pris en charge
Vous pouvez accéder à l’aide des étapes hello ci-dessous si votre appareil est en cours d’exécution un de ces systèmes d’exploitation de RemoteApp :

* Windows 10 
* Windows 8.1
* Windows 8
* Windows 7 Service Pack 1
* Windows Phone 8.1
* iOS
* Mac OS X
* Android

 Que se passe-t-il pour les clients légers ? Hello suivant clients légers Windows Embedded est prises en charge :

* Windows Embedded Standard 7
* Windows Embedded 8 Standard
* Windows Embedded 8.1 Industry Pro
* Windows 10 IoT Entreprise

## <a name="downloading-hello-client"></a>Téléchargement du client de hello
Quelle que soit la plate-forme que vous utilisez, le client hello vous devez tooaccess RemoteApp se trouvent sur hello [téléchargement du client Bureau à distance](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.

Cliquez sur liens différents hello soit directement commencent le téléchargement de client de hello ou vous enverra toohello page de téléchargement du client dans le magasin d’applications hello pour cette plateforme. Installer le client de hello en suivant les instructions de hello sur l’écran hello.

Une fois que vous avez installé le client de hello sur votre appareil et a lancé, passer toohello la section correspondante ci-dessous toolearn comment toosign dans tooRemoteApp à partir de ce client.

## <a name="android"></a>Android
Une fois que vous avez installé l’application de bureau à distance Microsoft hello de hello Google Play store, vous pouvez le trouver dans votre liste d’applications sous **Bureau à distance**.

1. Lors du lancement du application hello met tooan centre de connexion vide, sauf si vous avez déjà l’application hello. tooget main d’Azure RemoteApp, tap hello ajouter bouton **« « + » »** , puis appuyez sur **Azure RemoteApp**.    
   
     ![Centre de connexion vide](./media/remoteapp-clients/Android1.png)
2. Vous devez toosign avec votre service de messagerie adresse tooaccess hello. Appuyez sur **Prise en main**.
   
    ![Invite de connexion](./media/remoteapp-clients/Android2.png)
3. Sur la page suivante de hello, tapez dans votre **adresse de messagerie** , puis appuyez sur **continuer**. Cela lance hello processus de connexion à l’aide d’Azure Active Directory.
   
    ![Première page Azure Active Directory](./media/remoteapp-clients/Android3.png)
4. Suivez les instructions de hello à toosign d’écran hello avec votre compte Microsoft (précédemment appelé « LiveID ») ou l’ID d’organisation. Une fois connecté, peuvent s’afficher une page qui répertorie toutes les invitations hello que vous avez reçu. Si vous êtes, sélectionnez les invitations hello vous faites confiance, puis appuyez sur **fait**.    
   
    ![Page des invitations](./media/remoteapp-clients/Android4.png)
5. Après avoir accepté votre invitation, d’une liste de hello des applications d’avoir accès toowill être téléchargé tooyour appareil et mis à disposition dans hello centre de connexion. Cliquez sur un des toostart d’applications hello à l’utiliser.
   
    ![Centre de connexion avec un flux](./media/remoteapp-clients/Android5.png)
6. Si vous n’avez pas encore une invitation, vous pouvez toujours essayer service de hello. est par conséquent, appuyez sur toodo **atteindre la version d’évaluation toofree** lorsque vous y êtes invité.
   
    ![Invite de démonstration de flux](./media/remoteapp-clients/Android6.png)
7. Vous obtenez ainsi accéder à tooa base tooget applications main de RemoteApp.
   
    ![Démonstration de flux pour Azure RemoteApp](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a>iOS
Une fois que vous avez installé l’application de bureau à distance Microsoft hello à partir du magasin d’applications hello, vous pouvez le trouver dans votre liste d’applications sous **Client Bureau à distance**.

1. Lors du lancement du application hello met tooan centre de connexion vide, sauf si vous avez déjà l’application hello. tooget main d’Azure RemoteApp, tap hello ajouter bouton **« « + » »** , puis appuyez sur **ajouter Azure RemoteApp**.
   
    ![Centre de connexion vide](./media/remoteapp-clients/IOS1.png)
2. Vous devez toosign avec votre service de hello de messagerie adresse tooaccess, toostart ce processus, le type dans votre **adresse de messagerie** , puis appuyez sur **continuer**.
   
    ![Invite de connexion](./media/remoteapp-clients/picture1.png)
3. Suivez les instructions de hello à toosign d’écran hello avec votre compte de Microsoft (LiveID) ou votre organisation. Une fois connecté, peuvent s’afficher une page qui répertorie toutes les invitations hello que vous avez reçu. Si vous êtes, sélectionnez les invitations hello vous faites confiance, puis appuyez sur **fait**.
   
    ![Page des invitations](./media/remoteapp-clients/IOS3.png)
4. Après avoir accepté votre invitation, d’une liste de hello des applications d’avoir accès toowill être téléchargé tooyour appareil et mis à disposition dans hello centre de connexion. Cliquez sur un des hello applications toolaunch et recommencez à l’utiliser.
   
    ![Centre de connexion avec un flux](./media/remoteapp-clients/IOS4.png)
5. Si vous n’avez pas encore une invitation, vous pouvez toujours essayer service de hello. est par conséquent, appuyez sur toodo **atteindre la version d’évaluation toofree** lorsque vous y êtes invité.
   
    ![Invite de démonstration de flux](./media/remoteapp-clients/IOS5.png)
6. Vous obtenez ainsi accéder à tooa base tooget applications main de RemoteApp.
   
    ![Démonstration de flux pour Azure RemoteApp](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a>Mac OS X
Une fois que vous avez installé l’application de bureau à distance Microsoft hello à partir du magasin d’applications hello, vous pouvez le trouver dans votre liste d’applications sous **Bureau à distance Microsoft**.

1. Lors du lancement du application hello met tooan centre de connexion vide, sauf si vous avez déjà l’application hello. tooget main d’Azure RemoteApp, cliquez sur hello **Azure RemoteApp** bouton.
   
    ![Centre de connexion vide](./media/remoteapp-clients/Mac1.png)
2. Vous devez toosign avec votre service de hello de messagerie adresse tooaccess, toostart traiter, appuyez sur **prise en main**.
   
    ![Invite de connexion](./media/remoteapp-clients/Mac2.png)
3. Sur la page suivante de hello, tapez dans votre **adresse de messagerie** , puis appuyez sur **continuer**. Cela lance hello se connecte à l’aide d’Azure Active Directory.
   
    ![Première page Azure Active Directory](./media/remoteapp-clients/picture2.png)
4. Suivez les instructions de hello à toosign d’écran hello avec votre compte de Microsoft (LiveID) ou votre organisation. Une fois connecté, peuvent s’afficher une page qui répertorie toutes les invitations hello que vous avez reçu. Si vous êtes, sélectionnez les invitations hello vous faites confiance et fermez la boîte de dialogue hello.
   
    ![Page des invitations](./media/remoteapp-clients/Mac4.png)
5. Après avoir accepté votre invitation, d’une liste de hello des applications d’avoir accès toowill être téléchargé tooyour appareil et mis à disposition dans hello centre de connexion. Double-cliquez sur un des hello applications toolaunch et recommencez à l’utiliser.
   
    ![Centre de connexion avec un flux](./media/remoteapp-clients/Mac5.png)
6. Si vous n’avez pas encore une invitation, vous pouvez toujours essayer service de hello. toodo, cliquez sur **atteindre la version d’évaluation toofree** lorsque vous y êtes invité.
   
    ![Invite de démonstration de flux](./media/remoteapp-clients/Mac6.png)
7. Vous obtenez ainsi accéder à tooa base tooget applications main de RemoteApp.
   
    ![Démonstration de flux pour Azure RemoteApp](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a>Windows (Toutes les versions prises en charge sauf Windows Phone)
Hello client lance automatiquement une fois l’installation, toutefois lorsque vous avez besoin tooaccess il plus tard il sont accessibles dans votre liste d’applications sous le nom de hello **Azure RemoteApp**.

1. Lus tard du lancement hello client, hello première page qui apparaît vous souhaite la bienvenue tooAzure RemoteApp. tooproceed, cliquez sur **prise en main**.
   
    ![Page d’accueil du client d’Azure RemoteApp hello](./media/remoteapp-clients/Windows1.png)
2. page suivante de Hello démarre hello signe dans le processus d’Azure RemoteApp à l’aide d’Azure Active Directory. Ce processus doivent sembler familière si vous avez utilisé les services Microsoft Bonjour passées. Commencez par taper votre **adresse de messagerie**, puis cliquez sur **Continuer**.
   
    ![Invite de la première page Azure Active Directory](./media/remoteapp-clients/Windows2.png)
3. Suivez les instructions de hello à toosign d’écran hello avec votre compte de Microsoft (LiveID) ou votre organisation. Une fois connecté, peuvent s’afficher une page qui répertorie toutes les invitations hello que vous avez reçu. Si vous êtes, sélectionnez les invitations hello vous faites confiance, cliquez sur **fait**.
   
    ![Page invitations à participer à des clients d’Azure RemoteApp hello](./media/remoteapp-clients/Windows3.png)
4. Après avoir accepté votre invitation, d’une liste de hello des applications d’avoir accès toowill être téléchargé tooyour appareil et mis à disposition dans hello centre de connexion. Double-cliquez sur un des hello applications toolaunch et recommencez à l’utiliser.
   
    ![Centre de connexion du client d’Azure RemoteApp hello](./media/remoteapp-clients/Windows4.png)
5. Si personne ne vous a encore envoyé d'invitation, ne vous inquiétez pas : nous avons paré à cette éventualité ! Vous aurez toujours accès tooa démonstration collection afin de tester les service hello.
   
    ![Démonstration de flux pour Azure RemoteApp](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a>Windows Phone 8.1
Une fois que vous avez installé l’application de bureau à distance Microsoft hello à partir du magasin de hello Windows Phone 8.1, vous pouvez le trouver dans votre liste d’applications sous **Bureau à distance**.

1. Lors du lancement du application hello vous procure directement tooan centre de connexion vide, sauf si vous avez déjà l’application hello. tooget main d’Azure RemoteApp, tap hello ajouter bouton **« « + » »** bas hello écran hello.
   
    ![Centre de connexion vide](./media/remoteapp-clients/WinPhone1.png)
2. Appuyez ensuite sur **Azure RemoteApp**.
   
    ![Page Ajouter des éléments](./media/remoteapp-clients/WinPhone2.png)
3. Vous devez toosign avec votre service de hello de messagerie adresse tooaccess, toostart traiter, appuyez sur **connecter**.
   
    ![Invite de connexion](./media/remoteapp-clients/WinPhone3.png)
4. Sur la page suivante de hello, tapez dans votre **adresse de messagerie** , puis appuyez sur **continuer**. Cela lance hello se connecte à l’aide d’Azure Active Directory.
   
    ![Première page Azure Active Directory](./media/remoteapp-clients/WinPhone4.png)
5. Suivez les instructions de hello à toosign d’écran hello avec votre compte de Microsoft (LiveID) ou votre organisation. Une fois connecté, peuvent s’afficher une page qui répertorie toutes les invitations hello que vous avez reçu. Si vous êtes, sélectionnez les invitations hello vous faites confiance, puis appuyez sur **enregistrer**.
   
    ![Page des invitations](./media/remoteapp-clients/WinPhone5.png)
6. Après avoir accepté votre invitation, d’une liste de hello des applications d’avoir accès toowill être téléchargé tooyour appareil et mis à disposition dans hello centre de connexion. Cliquez sur un des hello applications toolaunch et recommencez à l’utiliser.
   
    ![Centre de connexion avec un flux](./media/remoteapp-clients/WinPhone6.png)
7. Si vous n’avez pas encore une invitation, vous pouvez toujours essayer service de hello. est par conséquent, appuyez sur toodo **Oui** lorsque vous y êtes invité.
   
    ![Invite de démonstration de flux](./media/remoteapp-clients/WinPhone7.png)
8. Vous obtenez ainsi accéder à tooa base tooget applications main de RemoteApp.
   
    ![Démonstration de flux pour Azure RemoteApp](./media/remoteapp-clients/WinPhone8.png)

