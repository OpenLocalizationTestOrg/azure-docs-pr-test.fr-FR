---
title: "mise à niveau du serveur MFA aaaAzure | Documents Microsoft"
description: "Les étapes et des conseils tooupgrade hello version plus récente de tooa serveur Azure multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 50bb8ac3-5559-4d8b-a96a-799a74978b14
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: aaa8d400e0e5f1c6be3a6d22cde6dd893ef4d546
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-toohello-latest-azure-multi-factor-authentication-server"></a>Mise à niveau toohello dernière serveur Azure multi-Factor Authentication

Cet article vous guide tout au long des hello processus de mise à niveau du serveur Azure multi-Factor Authentication (MFA) 6.0 ou version ultérieure. Si vous avez besoin de tooupgrade une ancienne version de le PhoneFactor Agent de hello, consultez trop[hello mise à niveau le PhoneFactor Agent tooAzure serveur multi-Factor](multi-factor-authentication-get-started-server-upgrade.md).

Si vous utilisez la mise à niveau à partir de v6.x ou toov7.x plus anciens ou plus récent, tous les composants de modifier à partir de .NET 2.0 too.NET 4.5. Tous les composants requièrent également Redistribuable Microsoft Visual C++ 2015 Update 1 ou une version ultérieure. programme d’installation du serveur MFA Hello installe les deux versions hello x86 et x64 de ces composants s’ils ne sont pas déjà installés. Si hello portail de l’utilisateur et Service Web d’application Mobile s’exécutent sur des serveurs distincts, vous devez tooinstall ces packages avant la mise à niveau ces composants. Vous pouvez rechercher des hello redistribuable Microsoft Visual C++ 2015 mise à jour sur hello [Microsoft Download Center](https://www.microsoft.com/en-us/download/). 

## <a name="install-hello-latest-version-of-azure-mfa-server"></a>Installer la version la plus récente du serveur de l’authentification Multifacteur Azure hello

1. Utilisez les instructions hello dans [téléchargement hello serveur Azure multi-Factor Authentication](multi-factor-authentication-get-started-server.md#download-the-azure-multi-factor-authentication-server) tooget hello dernière version de hello serveur Azure MFA.
2. Effectuez une sauvegarde du fichier de données de serveur MFA hello situé dans C:\Program Files\Multi-Factor Authentication Server\Data\PhoneFactor.pfdata (en supposant que hello par défaut emplacement d’installation) sur votre serveur principal de l’authentification Multifacteur.
3. Si vous exécutez plusieurs serveurs pour la haute disponibilité, modifiez les systèmes clients hello qui s’authentifient toohello serveur MFA de sorte qu’ils arrêtent l’envoi du trafic toohello les serveurs qui sont la mise à niveau. Si vous utilisez un équilibrage de charge, supprimer un serveur de l’authentification Multifacteur d’équilibrage de charge hello, procédez comme hello mise à niveau, puis ajoutez le serveur de hello dans la batterie de serveurs hello.
4. Exécutez le programme d’installation de la nouvelle hello sur chaque serveur de l’authentification Multifacteur. Mettre à niveau les serveurs subordonnés premier, car ils peuvent lire l’ancien fichier de données hello en cours de réplication par le maître de hello. 

  Il est inutile toouninstall votre serveur en cours de l’authentification Multifacteur avant le programme d’installation de hello en cours d’exécution. programme d’installation Hello effectue une mise à niveau sur place. Hello chemin d’installation est récupéré à partir du Registre hello à partir de l’installation précédente de hello, afin que celui-ci soit Bonjour même emplacement (par exemple, C:\Program Files\Multi-Factor Authentication Server). 
  
5. Si vous êtes tooinstall demandées Microsoft Visual C++ 2015 la mise à jour Redistributable package, acceptez hello. Les deux versions hello x86 et x64 du package de hello sont installées.
5. Si vous utilisez hello SDK du Service Web, vous êtes invité tooinstall hello nouveau SDK du Service Web. Lorsque vous installez hello nouveau SDK du Service Web, assurez-vous que ce nom de répertoire virtuel hello correspond au répertoire virtuel de hello précédemment installé (par exemple, MultiFactorAuthWebServiceSdk).
6. Répétez les étapes hello sur tous les serveurs subordonnés. Promouvoir l’un des hello subordonnés toobe hello nouveau maître, puis mise à niveau hello ancien serveur maître. 

## <a name="upgrade-hello-user-portal"></a>Mise à niveau hello portail de l’utilisateur

1. Effectuez une sauvegarde du fichier web.config hello qui se trouve dans le répertoire virtuel de hello Hello emplacement d’installation (par exemple, C:\inetpub\wwwroot\MultiFactorAuth) du portail de l’utilisateur. Si des modifications ont été apportées toohello le thème par défaut, effectuez une sauvegarde du dossier de App_Themes\Default hello également. Il est mieux toocreate une copie du dossier par défaut de hello et créer un nouveau thème à thème par défaut de hello toochange.
2. Si hello portail de l’utilisateur s’exécute sur le même serveur que hello d’autres composants serveur MFA, hello de hello installation du serveur de l’authentification Multifacteur vous invite tooupdate hello portail de l’utilisateur. Acceptez l’invite de hello et installer la mise à jour du portail de l’utilisateur hello. Vérifiez que ce nom de répertoire virtuel hello correspond au répertoire virtuel de hello précédemment installé (par exemple, MultiFactorAuth).
3. En cas de hello portail de l’utilisateur sur son propre serveur, copiez le fichier MultiFactorAuthenticationUserPortalSetup64.msi hello de hello emplacement d’installation d’un des hello serveurs MFA et le placer sur le serveur web du portail utilisateur hello. Exécutez le programme d’installation hello. 

  Si une erreur se produit indiquant, « Microsoft Visual C++ 2015 Redistributable mise à jour 1 ou version ultérieure est requis, » télécharger et installer le dernier package de mise à jour hello de hello [Microsoft Download Center](https://www.microsoft.com/download/). Installez les deux versions de x86 et x64 hello.

4. Une fois hello mis à jour le portail de l’utilisateur le logiciel est installé, comparer sauvegarde de web.config hello réalisée à l’étape 1 avec un nouveau fichier web.config de hello. Si aucun attribut n’existe dans le fichier web.config de nouveau hello, copiez votre fichier web.config sauvegarde hello toooverwrite de répertoire virtuel hello nouveau. Une autre option consiste à toocopy/coller des valeurs d’appSettings hello et hello URL du SDK du Service Web à partir du fichier de sauvegarde hello dans web.config de nouveau hello.

Si vous avez hello portail de l’utilisateur sur plusieurs serveurs, répétez l’installation hello sur chacun d'entre eux. 


## <a name="upgrade-hello-mobile-app-web-service"></a>Mise à niveau hello Service Web d’application Mobile

1. Effectuez une sauvegarde du fichier web.config hello qui est dans le répertoire virtuel de hello Hello emplacement d’installation de Service Web d’application Mobile (par exemple, C:\inetpub\wwwroot\app ou C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService).
2. Copiez le fichier MultiFactorAuthenticationMobileAppWebServiceSetup64.msi hello de hello emplacement d’installation de salutation serveurs MFA et placez-le sur serveur web de hello application Mobile d’enregistrement.
3. Exécutez le programme d’installation hello. 

  Si une erreur se produit indiquant que Microsoft Visual C++ 2015 Redistributable mise à jour 1 ou version ultérieure est requis, téléchargez et installez hello dernière mise à jour à partir de hello [Microsoft Download Center](https://www.microsoft.com/download/). Installez les deux versions de x86 et x64 hello.

4. Après installation du logiciel de Service Web d’application Mobile hello mis à jour, comparez le fichier web.config hello qui a été sauvegardée à l’étape 1 avec un nouveau fichier web.config de hello. Si aucun attribut n’existe dans le fichier web.config de nouveau hello, vous pouvez copier votre fichier web.config enregistré dans le répertoire virtuel de hello et remplacer hello nouveau. Une autre option consiste à toocopy/coller des valeurs d’appSettings hello et hello URL du SDK du Service Web à partir du fichier de sauvegarde hello dans web.config de nouveau hello.

Si vous avez hello Service Web d’application Mobile sur plusieurs serveurs, répétez l’installation hello sur chacun d'entre eux. 

## <a name="upgrade-hello-ad-fs-adapters"></a>Mise à niveau hello AD FS adaptateurs


### <a name="if-mfa-runs-on-different-servers-than-ad-fs"></a>Si MFA s’exécute sur d’autres serveurs qu’AD FS

Ces instructions s’appliquent uniquement si vous exécutez le serveur Multi-Factor Authentication indépendamment de vos serveurs AD FS. Si les deux services s’exécutent hello les mêmes serveurs, ignorez cette section et passez les étapes d’installation toohello. 

1. Enregistrer une copie du fichier MultiFactorAuthenticationAdfsAdapter.config hello qui a été inscrit dans AD FS ou exporter la configuration hello à l’aide de hello suivant de commande PowerShell : `Export-AdfsAuthenticationProviderConfigurationData -Name [adapter name] -FilePath [path tooconfig file]`. nom de l’adaptateur Hello est « WindowsAzureMultiFactorAuthentication » ou « AzureMfaServerAuthentication » en fonction de la version de hello précédemment installée.
2. Copiez hello fichiers suivants à partir de serveurs de hello serveur MFA installation emplacement toohello AD FS :

  - MultiFactorAuthenticationAdfsAdapterSetup64.msi
  - Register-MultiFactorAuthenticationAdfsAdapter.ps1
  - Unregister-MultiFactorAuthenticationAdfsAdapter.ps1
  - MultiFactorAuthenticationAdfsAdapter.config

3. Modifiez le script de hello Register-multifactorauthenticationadfsadapter.ps1 en ajoutant `-ConfigurationFilePath [path]` fin toohello Hello `Register-AdfsAuthenticationProvider` commande. Remplacez *[chemin]* avec le chemin d’accès complet de hello toohello MultiFactorAuthenticationAdfsAdapter.config fichier ou le fichier de configuration hello exporté à l’étape précédente de hello. 

  Vérifiez les attributs de hello dans hello nouvelle MultiFactorAuthenticationAdfsAdapter.config toosee s’ils correspondent l’ancien fichier de configuration hello. Si tous les attributs ont été ajoutés ou supprimés dans la nouvelle version de hello, copier les valeurs d’attribut hello toohello de fichier de configuration anciennes hello nouveau ou modifier toomatch du fichier hello ancienne configuration.

### <a name="install-new-ad-fs-adapters"></a>Installer de nouveaux adaptateurs AD FS

> [!IMPORTANT] 
> Vos utilisateurs ne seront pas de vérification en deux étapes de tooperform requis au cours des étapes 3 à 8 de cette section. Si vous avez configuré AD FS dans plusieurs clusters, vous pouvez supprimer, mise à niveau et la restauration de la batterie de serveurs chaque cluster Bonjour indépendamment de hello autres interruptions de service tooavoid clusters.

1. Supprimer des serveurs AD FS à partir de la batterie de serveurs hello. Mettre à jour de ces serveurs lors hello d’autres sont en cours d’exécution.
2. Installer l’adaptateur AD FS hello sur chaque serveur supprimé de la batterie de serveurs hello AD FS. Si hello MFA Server est installé sur chaque serveur AD FS, vous pouvez mettre à jour via l’administration du serveur MFA hello UX. Sinon, effectuez la mise à jour en exécutant MultiFactorAuthenticationAdfsAdapterSetup64.msi. 

  Si une erreur se produit indiquant, « Microsoft Visual C++ 2015 Redistributable mise à jour 1 ou version ultérieure est requis, » télécharger et installer le dernier package de mise à jour hello de hello [Microsoft Download Center](https://www.microsoft.com/download/). Installez les deux versions de x86 et x64 hello.

3. Accédez trop**AD FS** > **des stratégies d’authentification** > **modifier la stratégie d’authentification multifacteur Global**. Décochez la case **WindowsAzureMultiFactorAuthentication** ou **AzureMFAServerAuthentication** (selon la version actuelle de hello installée). 

  Une fois cette étape terminée, la vérification en deux étapes par le serveur MFA ne sera pas disponible dans ce cluster AD FS avant la fin de l’étape 8.

4. Unregister hello version antérieure de l’adaptateur hello AD FS en exécutant hello Unregister-multifactorauthenticationadfsadapter.ps1 de script PowerShell. Vérifiez que hello *-nom* paramètre (« WindowsAzureMultiFactorAuthentication » ou « AzureMFAServerAuthentication ») correspond au nom de hello qui a été affiché à l’étape 3. Cela s’applique tooall des serveurs dans un cluster de hello même AD FS dans la mesure où il existe une configuration centrale.
5. Inscrire l’adaptateur AD FS hello en exécutant le script de Registre-multifactorauthenticationadfsadapter.ps1 PowerShell hello. Cela s’applique tooall des serveurs dans un cluster de hello même AD FS dans la mesure où il existe une configuration centrale.
6. Hello de redémarrage du service AD FS sur chaque serveur supprimé hello batterie de serveurs AD FS.
7. Ajouter des serveurs de mise à jour de hello sauvegarder la batterie de serveurs toohello AD FS et remove hello autres serveurs à partir de la batterie de serveurs hello.
8. Accédez trop**AD FS** > **des stratégies d’authentification** > **modifier la stratégie d’authentification multifacteur Global**. Cochez **AzureMfaServerAuthentication**.
9. Répétez l’étape 2 : serveurs hello tooupdate maintenant supprimés de la batterie de serveurs hello AD FS et redémarrer hello AD FS sur ces serveurs.
10. Ajouter ces serveurs dans la batterie de serveurs hello AD FS.

## <a name="next-steps"></a>Étapes suivantes

- Consultez des exemples de [Scénarios avancés avec Azure Multi-Factor Authentication et des VPN tiers](multi-factor-authentication-advanced-vpn-configurations.md)

- [Synchronisez le serveur MFA avec Windows Server Active Directory](multi-factor-authentication-get-started-server-dirint.md)

- [Configurez l’authentification Windows](multi-factor-authentication-get-started-server-windows.md) pour vos applications
