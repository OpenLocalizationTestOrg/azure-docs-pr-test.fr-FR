---
title: aaaUpgrade PhoneFactor tooAzure serveur MFA | Documents Microsoft
description: "Prise en main le serveur Azure MFA lorsque vous mettez à niveau à partir de l’agent phonefactor plus ancienne de hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 42838ff7-bdf2-4d06-bacc-b3839a00cd76
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.openlocfilehash: 15b7b8517929c30f66e6a39cd44c69d12d25c6d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hello-phonefactor-agent-tooazure-multi-factor-authentication-server"></a>Hello mise à niveau le PhoneFactor Agent tooAzure serveur multi-Factor Authentication
tooupgrade hello PhoneFactor Agent v5.x ou antérieure tooAzure serveur multi-Factor Authentication, désinstaller hello PhoneFactor Agent et affilié tout d’abord les composants. Puis hello serveur multi-Factor Authentication et ses composants connexes peuvent être installés.

## <a name="uninstall-hello-phonefactor-agent"></a>Désinstaller le PhoneFactor Agent de hello

1. Sauvegarder tout d’abord, le fichier de données PhoneFactor hello. emplacement d’installation par défaut Hello est C:\Program Files\PhoneFactor\Data\Phonefactor.pfdata.

2. Si hello portail de l’utilisateur est installé :
  1. Accédez toohello du dossier d’installation et sauvegardez le fichier web.config de hello. emplacement d’installation Hello par défaut est C:\inetpub\wwwroot\PhoneFactor.

  2. Si vous avez ajouté le portail de toohello des thèmes personnalisés, sauvegardez votre dossier personnalisé sous le répertoire C:\inetpub\wwwroot\PhoneFactor\App_Themes de hello.

  3. Désinstaller hello portail de l’utilisateur via hello PhoneFactor Agent (disponible uniquement si installé sur hello PhoneFactor Agent hello par le même serveur que) ou via des programmes et fonctionnalités Windows.

3. Si hello Service Web d’application Mobile est installé :

  1. Accédez toohello du dossier d’installation et sauvegardez le fichier web.config de hello. emplacement d’installation Hello par défaut est C:\inetpub\wwwroot\PhoneFactorPhoneAppWebService.

  2. Désinstallez hello Service Web d’application Mobile via programmes et fonctionnalités Windows.

4. Si hello SDK du Service Web est installé, désinstallez-le via hello PhoneFactor Agent ou programmes et fonctionnalités Windows.

5. Désinstallez hello PhoneFactor Agent via programmes et fonctionnalités Windows.

## <a name="install-hello-multi-factor-authentication-server"></a>Installer hello serveur multi-Factor Authentication

Hello chemin d’installation est récupéré à partir du Registre hello à partir de l’installation de le PhoneFactor Agent précédente hello, par conséquent, il doit installer Bonjour même emplacement (par exemple, C:\Program Files\PhoneFactor). Les nouvelles installations présentent un chemin d’installation par défaut différent (par exemple, C:\Program Files\Multi-Factor Authentication Server). Hello en hello précédente de que phonefactor Agent doit être mis à niveau pendant l’installation, afin de vos utilisateurs et les paramètres doivent être encore qu'il hello nouveau serveur d’authentification multifacteur après l’installation fichier de données.

1. Si vous y êtes invité, activer hello serveur multi-Factor Authentication et assurez-vous qu’il est attribué le groupe de réplication approprié toohello.

2. Si hello SDK du Service Web a été précédemment installé, installez hello nouveau du SDK du Service Web via hello Interface utilisateur de multi-Factor Authentication Server.

  par défaut de nom de répertoire virtuel est maintenant de Hello **MultiFactorAuthWebServiceSdk** au lieu de **PhoneFactorWebServiceSdk**. Si vous souhaitez que le nom de toouse hello précédent, vous devez modifier le nom hello du répertoire virtuel de hello lors de l’installation. Dans le cas contraire, si vous autorisez hello installation toouse hello nouveau nom par défaut, vous avez toochange hello URL dans toutes les applications que hello référence SDK du Service Web (par exemple hello portail de l’utilisateur et le Service Web d’application Mobile) toopoint à l’emplacement correct de hello.

3. Si hello portail de l’utilisateur a été précédemment installé sur hello PhoneFactor Agent serveur, installez hello nouveau portail d’utilisateur d’authentification multifacteur via hello Interface utilisateur de multi-Factor Authentication Server.

  par défaut de nom de répertoire virtuel est maintenant de Hello **MultiFactorAuth** au lieu de **PhoneFactor**. Si vous souhaitez que le nom de toouse hello précédent, vous devez modifier le nom hello du répertoire virtuel de hello lors de l’installation. Dans le cas contraire, si vous autorisez hello installation toouse hello nouveau nom par défaut, vous cliquez sur l’icône portail utilisateur hello Bonjour serveur multi-Factor et mettre à jour hello URL du portail utilisateur sur l’onglet Paramètres de hello.

4. Si hello portail utilisateur et/ou le Service Web d’application Mobile a été précédemment installé sur un serveur différent de hello PhoneFactor Agent :

  1. Atteindre l’emplacement d’installation toohello (par exemple, C:\Program Files\PhoneFactor) et copiez toohello de programmes d’installation au moins un autre serveur. Il existe des programmes d’installation 32 bits et 64 bits pour hello portail de l’utilisateur et le Service application Web Mobile. Ils sont appelés MultiFactorAuthenticationUserPortalSetupXX.msi et MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi.

  2. tooinstall hello portail de l’utilisateur sur le serveur web de hello, ouvrez une invite de commandes en tant qu’administrateur et exécutez MultiFactorAuthenticationUserPortalSetupXX.msi.

    par défaut de nom de répertoire virtuel est maintenant de Hello **MultiFactorAuth** au lieu de **PhoneFactor**. Si vous souhaitez que le nom de toouse hello précédent, vous devez modifier le nom hello du répertoire virtuel de hello lors de l’installation. Dans le cas contraire, si vous autorisez hello installation toouse hello nouveau nom par défaut, vous cliquez sur l’icône portail utilisateur hello Bonjour serveur multi-Factor et mettre à jour hello URL du portail utilisateur sur l’onglet Paramètres de hello. Les utilisateurs existants doivent toobe informé de la nouvelle URL de hello.

  3. Atteindre l’emplacement d’installation toohello portail de l’utilisateur (par exemple, C:\inetpub\wwwroot\MultiFactorAuth) et modifier le fichier web.config de hello. Copiez les valeurs hello dans les sections appSettings et applicationSettings de hello à partir de votre fichier web.config d’origine qui a été sauvegardé avant la mise à niveau hello dans le fichier web.config hello. Si le nouveau nom de répertoire virtuel par défaut hello a été conservé lors de l’installation du SDK du Service Web de hello, modifiez les URL de hello hello applicationSettings section toopoint toohello bon emplacement. Si toutes les autres valeurs par défaut ont été modifiés dans le précédent fichier web.config de hello, appliquer ces mêmes modifications toohello nouveau fichier web.config.

  4. tooinstall hello Service Web d’application Mobile sur le serveur web de hello, ouvrez une invite de commandes en tant qu’administrateur et exécutez hello MultiFactorAuthenticationMobileAppWebServiceSetupXX.msi.

    par défaut de nom de répertoire virtuel est maintenant de Hello **MultiFactorAuthMobileAppWebService** au lieu de **PhoneFactorPhoneAppWebService**. Si vous souhaitez que le nom de toouse hello précédent, vous devez modifier le nom hello du répertoire virtuel de hello lors de l’installation. Vous souhaiterez peut-être toochoose un toomake nom plus court plus facile pour les utilisateurs finaux des tootype dans sur leurs appareils mobiles. Dans le cas contraire, si vous autorisez hello installation toouse hello nouveau nom par défaut, vous cliquez sur icône d’application Mobile hello Bonjour serveur multi-Factor et mettre à jour hello URL du Service Web application Mobile.

  5. Atteindre l’emplacement d’installation de Service Web d’application Mobile toohello (par exemple, C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService) et modifier le fichier web.config de hello. Copiez les valeurs hello dans les sections appSettings et applicationSettings de hello à partir de votre fichier web.config d’origine qui a été sauvegardé avant la mise à niveau hello dans le fichier web.config hello. Si le nouveau nom de répertoire virtuel par défaut hello a été conservé lors de l’installation du SDK du Service Web de hello, modifiez les URL de hello hello applicationSettings section toopoint toohello bon emplacement. Si toutes les autres valeurs par défaut ont été modifiés dans le précédent fichier web.config de hello, appliquer ces mêmes modifications toohello nouveau fichier web.config.

## <a name="next-steps"></a>Étapes suivantes

- [Installer le portail des utilisateurs hello](multi-factor-authentication-get-started-portal.md) pourquoi le serveur Azure multi-Factor Authentication.

- [Configurez l’authentification Windows](multi-factor-authentication-get-started-server-windows.md) pour vos applications. 
