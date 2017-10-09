---
title: "aaaEnabling l’accès à distance pour les déploiements Azure dans Eclipse"
description: "Découvrez comment l’accès à distance de tooenable pour les déploiements Azure à l’aide de hello boîte à outils Azure pour Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a>Activation de l’accès à distance pour les déploiements Azure dans Eclipse
toohelp dépannage de vos déploiements, vous pouvez activer et utiliser l’accès à distance tooconnect toohello virtual machine hébergeant votre déploiement. Hello fonctionnalité accès à distance s’appuie sur hello protocole RDP (Remote Desktop). Après avoir publié tooAzure, ou si vous utilisez Eclipse avec un système d’exploitation de Windows, vous pouvez configurer l’accès à distance avant de publier tooAzure, vous pouvez configurer l’accès à distance pour votre déploiement. Notez que vous avez besoin d’un client Bureau à distance qui est compatible avec votre système d’exploitation dans une machine virtuelle dans Azure, de déploiement de l’ordre tooconnect tooyour.

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a>Comment tooenable l’accès à distance avant de déployer tooAzure
> [!NOTE]
> tooenable l’accès à distance avant de déployer votre tooAzure d’application, vous devez toobe exécuter Eclipse sur Windows.
> 
> 

Hello image suivante montre hello **l’accès à distance** boîte de dialogue de propriétés utilisée tooenable l’accès à distance.

![][ic719494]

Il existe deux hello toodisplay de façons **l’accès à distance** boîte de dialogue Propriétés :

* Cliquez sur hello **avancé** lien Bonjour **l’accès à distance** section Hello **publier tooAzure** boîte de dialogue.

* Ouvrez hello **propriétés** boîte de dialogue de votre projet Windows Azure.

Lorsque vous créez un nouveau projet de déploiement d’Azure, projet de hello n’aura pas accès à distance activée par défaut. Toutefois, vous pouvez facilement activer l’accès à distance en spécifiant le nom d’utilisateur hello et le mot de passe Bonjour **publier tooAzure** boîte de dialogue. mot de passe de l’accès à distance Hello est chiffré à l’aide de certificats X.509. Si vous n’utilisez pas fournir votre propre certificat, le chiffrement hello s’appuie sur un certificat auto-signé fourni avec hello plug-in Azure pour Eclipse. Ce certificat auto-signé est Bonjour **cert** dossier de votre projet Windows Azure, stocké à la fois en tant que fichier de certificat public (SampleRemoteAccessPublic.cer) et comme un Exchange informations personnelles (PFX) (fichier de certificat SampleRemoteAccessPrivate.pfx). Hello ce dernier contient hello clé privée hello, et a un mot de passe par défaut, **Password1**. Toutefois, ce mot de passe étant publiquement connu, certificat par défaut de hello doit être utilisé uniquement pour l’apprentissage, pas pour un déploiement de production. Par conséquent, autre qu’à des fins pédagogiques, lorsque vous souhaitez tooenabled les sessions à distance pour vos déploiements, vous devez cliquer sur hello **avancé** lien Bonjour **publier tooAzure** toospecify de la boîte de dialogue votre propre certificat. Notez que vous devez avoir la version PFX hello tooupload hello tooyour hébergé du service de certificats dans hello portail de gestion Azure afin qu’Azure puisse déchiffrer le mot de passe utilisateur hello.

reste Hello du didacticiel de hello vous montre comment l’accès à distance de tooenable d’un projet de déploiement d’Azure qui a été initialement créé avec l’accès à distance est désactivé. Pour les besoins de ce didacticiel, nous allons créer un certificat auto-signé, dont le fichier .pfx aura le mot de passe de votre choix. Vous avez également option hello d’à l’aide d’un certificat émis par une autorité de certification.

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a>Comment tooenable l’accès à distance après l’avoir déployé tooAzure
accès à distance tooenable après avoir déployé tooAzure, hello utilisation comme suit :

1. Connectez-vous au portail de gestion Azure hello à l’aide de votre compte Azure

2. Dans la liste **Cloud Services**, sélectionnez votre service cloud déployé.

3. Dans la page web de hello cloud service, cliquez sur hello **configurer** lien

4. Hello le bas de la page de configuration hello, cliquez sur hello **distant** lien

5. Lorsque la boîte de dialogue contextuelle hello s’affiche :
   
   * Spécifiez hello rôle pour lequel que vous voulez tooenable l’accès à distance

   * Cliquez sur tooselect hello **activer le Bureau à distance** case à cocher
   
   * Spécifiez un nom d’utilisateur et un mot de passe toouse pour l’accès à distance
   
   * Sélectionnez hello certificat toouse

6. Cliquez sur **OK** 

Vous verrez un message indiquant que la modification de votre configuration est en cours d’exécution, ce qui peut prendre quelques minutes toocomplete. Une fois la modification de configuration hello terminée, suivez les étapes de hello Bonjour **toolog dans à distance** section plus loin dans cet article.

## <a name="how-tooenable-remote-access-in-your-package"></a>Comment tooenable l’accès à distance dans votre package.
1. Dans le volet de l’Explorateur de projets d’Eclipse, cliquez avec le bouton droit sur votre projet Azure, puis sur **Propriétés**.

2. Bonjour **propriétés** boîte de dialogue, développez **Azure** dans le volet gauche de hello et cliquez sur **l’accès à distance**.

3. Bonjour **l’accès à distance** boîte de dialogue, vérifiez **activer tous les rôles tooaccept les connexions Bureau à distance avec ces informations d’identification de connexion** est activée.

4. Spécifiez un nom d’utilisateur pour hello connexion Bureau à distance.

5. Spécifiez et confirmez le mot de passe hello pour hello. vous servira Hello utilisateur nom et mot de passe valeurs définies dans cette boîte de dialogue lorsque vous établissez une connexion Bureau à distance. (Notez qu’il s’agit d’un mot de passe distinct de celui de votre fichier PFX.)

6. Spécifiez la date d’expiration de hello hello compte d’utilisateur.

7. Cliquez sur **nouveau** toocreate un nouveau certificat auto-signé. (Ou bien, vous pouvez sélectionner un certificat à partir de votre système de fichiers ou d’espace de travail via hello **espace de travail** ou **FileSystem** des boutons, respectivement, mais pour les besoins de ce didacticiel, nous allons créer un nouveau certificat.)

   * Bonjour **nouveau certificat** boîte de dialogue, spécifiez et confirmez le mot de passe hello vous utiliserez pour votre fichier PFX.

   * Acceptez la valeur hello fournie pour **nom (CN)**, ou utilisez un nom personnalisé.

   * Spécifiez hello chemin d’accès et nom de fichier dans lequel hello nouveau certificat, au format .cer doit être enregistré. Pour cette étape et hello suivante, vous pouvez utiliser hello **cert** dossier de votre projet Windows Azure, mais vous êtes libre toochoose un autre emplacement. Dans le cadre de ce didacticiel, nous utiliserons **c:\mycert\mycert.cer**. (Créer hello **c:\mycert** tooproceeding préalable du dossier, ou choisissez un dossier existant si vous le souhaitez.)

   * Spécifiez hello chemin d’accès et nom de fichier où seront enregistrées hello nouveau certificat et sa clé privée, au format .pfx. Dans le cadre de ce didacticiel, nous utiliserons **c:\mycert\mycert.pfx**. Votre **nouveau certificat** boîte de dialogue doit se présenter comme toohello suivant (mettre à jour les chemins d’accès du dossier hello si vous n’utilisez pas **c:\mycert**) :
     
      ![][ic712275]

   * Cliquez sur **OK** tooclose hello **nouveau certificat** boîte de dialogue.

8. Votre **l’accès à distance** boîte de dialogue doit se présenter comme toohello suivantes :</p>
   
   ![][ic719495]

9. Cliquez sur **OK** tooclose hello **l’accès à distance** boîte de dialogue.

Régénérez votre application, avec hello générer ensemble pour toocloud de déploiement.

## <a name="toolog-in-remotely"></a>toolog dans à distance
Une fois que votre instance de rôle est prêt, vous pouvez vous connecter à distance dans la machine virtuelle toohello qui héberge votre application.

* Si vous utilisez Eclipse sur Windows et vous hello sélectionné **démarrer le Bureau à distance sur déploiement** option lors de votre déploiement tooAzure, s’affiche avec un écran d’ouverture de session de connexion Bureau à distance au démarrage de votre déploiement. Lorsque vous êtes invité hello nom d’utilisateur et mot de passe, entrez les valeurs hello que vous avez spécifié pour l’utilisateur distant de hello et sera en mesure de toolog dans.

* Un autre toolog moyen dans est à distance via hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">portail de gestion Azure</a>:
  
  * Au sein de hello **Services de cloud computing** vue Hello portail de gestion Azure, cliquez sur votre service cloud, cliquez sur **Instances**et cliquez sur une instance spécifique, puis cliquez sur hello **Connect**bouton. Hello **Connect** bouton s’affiche comme suit hello dans la barre de commandes hello :
    
      ![][ic659273]

  * Après avoir cliqué sur hello **Connect** bouton, vous serez invité à tooopen un fichier RDP. Ouvrir le fichier de hello et suivez les invites hello. (Votre peut également enregistrer cet ordinateur local tooyour de fichier, puis exécutez hello fichier en double-cliquant dessus tooremote journal dans tooyour machine virtuelle sans avoir besoin de toofirst atteindre le portail de gestion hello.)

  * Lorsque vous êtes invité hello nom d’utilisateur et mot de passe, entrez les valeurs hello que vous avez spécifié pour l’utilisateur distant de hello et sera en mesure de toolog dans.

> [!NOTE]
> Si vous êtes sur un système d’exploitation non-Windows, vous devez toouse un client Bureau à distance qui est compatible avec votre système d’exploitation et suivez hello étapes tooconfigure que le client avec les paramètres de hello dans le fichier RDP hello que vous avez téléchargé.
> 
> 

## <a name="see-also"></a>Voir aussi
[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]

[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Lors de l’installation hello boîte à outils Azure pour Eclipse][Installing hello Azure Toolkit for Eclipse] 

Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
