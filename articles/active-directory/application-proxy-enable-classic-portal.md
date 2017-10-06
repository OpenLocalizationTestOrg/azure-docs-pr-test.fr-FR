---
title: "aaaEnable Proxy d’Application Azure AD dans le portail classique de hello | Documents Microsoft"
description: "Activer le Proxy d’Application Bonjour portail Azure classic et installer des connecteurs de proxy inverse de hello hello."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: c7186f98-dd80-4910-92a4-a7b8ff6272b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro; oldportal
ms.openlocfilehash: 8be9416a61993e1b46a20152e172c5133e54c0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-application-proxy-in-hello-classic-portal-and-download-connectors"></a>Activer le Proxy d’Application dans le portail classique de hello et télécharger des connecteurs
Cet article vous assiste hello étapes tooenable Proxy d’Application Microsoft Azure AD pour votre annuaire cloud dans Azure AD.

Si vous n’êtes pas familiarisé avec ce que le Proxy d’Application peuvent vous aider à effectuer, en savoir plus sur [comment tooprovide sécuriser l’accès à distance, applications locales tooon](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Conditions préalables pour le proxy d’application
Avant que vous pouvez activer et utiliser les services de Proxy d’Application, vous devez toohave :

* Un [abonnement Microsoft Azure AD de base ou Premium](active-directory-editions.md) et un annuaire Azure AD sur lequel vous êtes administrateur général.
* Un serveur exécutant Windows Server 2012 R2 ou 2016, sur lequel vous pouvez installer hello connecteur Proxy d’Application. serveur de Hello envoie des demandes toohello les services de Proxy d’Application dans le cloud de hello, et il doit une applications toohello connexion HTTP ou HTTPS que vous publiez.
  * Tooyour de l’authentification unique pour les applications publiées cet ordinateur doit être joint au domaine dans le domaine de hello même AD en tant qu’applications hello que vous publiez. Pour plus d’informations, consultez [Authentification unique avec le proxy d’application](active-directory-application-proxy-sso-using-kcd.md).
* Si votre organisation utilise le proxy internet, de serveurs tooconnect toohello lecture [travail avec existant local serveurs proxy](application-proxy-working-with-proxy-servers.md) pour plus d’informations sur la façon de tooconfigure les.

## <a name="open-your-ports"></a>Ouvrir vos ports

tooprepare votre environnement pour le Proxy d’Application Azure AD, vous devez d’abord tooenable communication tooAzure des centres de données. S’il existe un pare-feu dans le chemin d’accès de hello, assurez-vous qu’il est ouvert afin que hello que connecteur peut rendre HTTPS (TCP) demande toohello le Proxy d’Application.

1. Ports de suivants de hello ouverte trop**sortant** le trafic :

   | Numéro de port | Utilisation |
   | --- | --- |
   | 80 | Téléchargement de la révocation de certificats de listes (CRL) lors de la validation du certificat SSL de hello |
   | 443 | Toutes les communications sortantes par hello service Proxy d’Application |

   Si votre pare-feu gère le trafic en fonction des utilisateurs de toooriginating, ouvrir ces ports pour le trafic en provenance des services Windows exécutés comme Service réseau.

   > [!IMPORTANT]
   > table de Hello reflète les exigences du port hello pour les versions de connecteur 1.5.132.0 et les versions ultérieures. Si vous disposez toujours d’une ancienne version de connecteur, vous devez également hello tooenable suivant des ports : 5671, 8080, 9090, 9091, 9350, 9352 et 10100 – 10120.
   >
   >Pour plus d’informations sur la mise à jour de votre version la plus récente toohello connecteurs, consultez [connecteurs de Proxy d’Application Azure de comprendre AD](application-proxy-understand-connectors.md#automatic-updates).

2. Si votre pare-feu ou un proxy autorise liste approuvées DNS, vous pouvez servicebus.windows.net et toomsappproxy.net de connexions de liste blanche. Si non, vous devez tooallow accès toohello [plages d’adresses IP du centre de données Azure](https://www.microsoft.com/download/details.aspx?id=41653), qui sont mis à jour chaque semaine.

3. Hello d’utilisation [Azure AD Application Proxy Connector Ports Test outil](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify que votre connecteur pouvez contacter le service de Proxy d’Application hello. Au minimum, assurez-vous que toutes les coches vertes la région du centre des États-Unis hello et tooyou le plus proche de la région de hello. En outre, un nombre plus élevé de coches vertes signifie une résilience accrue.

## <a name="enable-application-proxy-in-azure-ad"></a>Activer le proxy d’application dans Azure AD
1. Connectez-vous en tant qu’administrateur Bonjour [portail Azure classic](https://manage.windowsazure.com/).
2. TooActive active, sélectionnez le répertoire hello dans lequel vous souhaitez tooenable Proxy d’Application.

    ![Active Directory - icône](./media/active-directory-application-proxy-enable/ad_icon.png)
3. Sélectionnez **configurer** la page annuaire hello et faites défiler trop**le Proxy d’Application**.
4. Activer/désactiver **activer les Services de Proxy d’Application pour ce répertoire** trop**activé**.

    ![Activer le proxy d’application](./media/active-directory-application-proxy-enable/app_proxy_enable.png)
5. Sélectionnez **Télécharger maintenant**. Hello **Azure AD Application Proxy Connector Télécharger** s’ouvre. Lisez et acceptez les termes du contrat de licence hello et cliquez sur **télécharger** toosave hello fichier Windows Installer (.exe) de connecteur de hello.

## <a name="install-and-register-hello-connector"></a>Installer et inscrire hello connecteur
1. Exécutez **AADApplicationProxyConnectorInstaller.exe** sur le serveur de hello vous préparé conséquente toohello prerequisites.
2. Suivez les instructions de hello de hello Assistant tooinstall.
3. Pendant l’installation, vous êtes tooregister demandées hello connecteur hello Proxy d’Application de votre client Azure AD.

   * Fournissez vos informations d’identification d’administrateur général d’Azure AD. Votre client d’administrateur global peut être différent de vos informations d’identification Microsoft Azure.
   * Assurez-vous que l’administrateur de hello hello connecteur se trouve dans des registres hello même répertoire où vous avez activé hello service Proxy d’Application. Par exemple, si le domaine du locataire hello est contoso.com, hello admin doit être admin@contoso.com ou tout autre alias sur ce domaine.
   * Si **la Configuration de sécurité renforcée d’Internet Explorer** est défini trop**sur** sur le serveur de hello, l’écran d’enregistrement hello risque d’être bloqué. accès tooallow, suivez les instructions dans le message d’erreur hello hello. Vérifiez que la configuration de sécurité renforcée d’Internet Explore est désactivée.
   * Si l’inscription du connecteur n’aboutit pas, voir [Résoudre les problèmes du proxy d’application](active-directory-application-proxy-troubleshoot.md).  
4. Lors de l’installation de hello terminée, deux nouveaux services sont ajoutés tooyour server :

   * **connecteur de proxy d’application Microsoft AAD** active la connectivité.

     * **Le programme de mise à jour du connecteur de proxy d’application Microsoft AAD** est un service de mise à jour automatique. Il vérifie les nouvelles versions de connecteur de hello périodiquement et met à jour de connecteur de hello en fonction des besoins.

     ![Services de connecteur de proxy d’application - capture d’écran](./media/active-directory-application-proxy-enable/app_proxy_services.png)
5. Cliquez sur **Terminer** dans la fenêtre d’installation hello.

Pour plus d’informations sur les connecteurs, consultez [Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md).

Pour bénéficier d’une haute disponibilité, vous devez déployer au moins deux connecteurs. toodeploy plusieurs connecteurs, répétez les étapes 2 et 3. Chaque connecteur doit être inscrit séparément.

Si vous souhaitez toouninstall hello connecteur, désinstallez les services de connecteur hello et hello mise à jour. Redémarrez votre ordinateur toofully supprimer hello service.

## <a name="next-steps"></a>Étapes suivantes
Vous êtes maintenant prêt trop[publier des applications avec Proxy d’Application](active-directory-application-proxy-publish.md).

Si vous avez des applications qui se trouvent sur des réseaux distincts ou des emplacements différents, vous pouvez utiliser plusieurs connecteurs connecteur groupes tooorganize hello dans des unités logiques. Apprenez-en davantage sur [l’utilisation de connecteurs de proxy d’application](active-directory-application-proxy-connectors.md).
