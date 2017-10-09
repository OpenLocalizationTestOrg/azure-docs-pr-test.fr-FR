---
title: "Démarrer aaaAzure application Proxy AD - installer le connecteur | Documents Microsoft"
description: "Activer le Proxy d’Application Bonjour portail Azure et installer des connecteurs de proxy inverse de hello hello."
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
ms.date: 08/02/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ea79ffa92fa223584be04f49019fd31a0bfd8358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-proxy-and-install-hello-connector"></a>Prise en main le Proxy d’Application et d’installer le connecteur de hello
Cet article vous assiste hello étapes tooenable Proxy d’Application Microsoft Azure AD pour votre annuaire cloud dans Azure AD.

Si vous n’êtes pas encore prenant en charge des avantages de sécurité et de productivité hello tooyour organisation met de Proxy d’Application, en savoir plus sur [comment tooprovide sécuriser l’accès à distance, applications locales tooon](active-directory-application-proxy-get-started.md).

## <a name="application-proxy-prerequisites"></a>Conditions préalables pour le proxy d’application
Avant que vous pouvez activer et utiliser les services de Proxy d’Application, vous devez toohave :

* Un [abonnement Microsoft Azure AD de base ou Premium](active-directory-editions.md) et un annuaire Azure AD sur lequel vous êtes administrateur général.
* Un serveur exécutant Windows Server 2012 R2 ou 2016, sur lequel vous pouvez installer hello connecteur Proxy d’Application. Hello a besoin que les services de Proxy d’Application du toohello toobe tooconnect en mesure de dans le cloud de hello et hello des applications que vous publiez sur site.
  * Tooyour de l’authentification unique pour les applications publiées à l’aide de la délégation contrainte Kerberos, cet ordinateur doit être appartenant au domaine dans le domaine de hello même AD en tant qu’applications hello que vous publiez. Pour plus d’informations, consultez [KCD pour authentification unique avec le proxy d’application](active-directory-application-proxy-sso-using-kcd.md).

Si votre organisation utilise le proxy internet, de serveurs tooconnect toohello lecture [travail avec existant local serveurs proxy](application-proxy-working-with-proxy-servers.md) pour plus d’informations sur comment tooconfigure les avant d’obtiennent en main de Proxy d’Application.

## <a name="open-your-ports"></a>Ouvrir vos ports

tooprepare votre environnement pour le Proxy d’Application Azure AD, vous devez d’abord tooenable communication tooAzure des centres de données. S’il existe un pare-feu dans le chemin d’accès de hello, assurez-vous qu’il est ouvert afin que hello que connecteur peut rendre HTTPS (TCP) demande toohello le Proxy d’Application.

1. Ports de suivants de hello ouverte trop**sortant** le trafic :

   | Numéro de port | Utilisation |
   | --- | --- |
   | 80 | Téléchargement de la révocation de certificats de listes (CRL) lors de la validation du certificat SSL de hello |
   | 443 | Toutes les communications sortantes par hello service Proxy d’Application |

   Si votre pare-feu gère le trafic en fonction des utilisateurs de toooriginating, ouvrir ces ports pour le trafic à partir des services Windows qui s’exécutent comme un Service réseau.

   > [!IMPORTANT]
   > table de Hello reflète les exigences du port hello pour les versions de connecteur 1.5.132.0 et les versions ultérieures. Si vous disposez toujours d’une ancienne version de connecteur, vous devez également hello tooenable suivant ports dans Ajout too80 et 443:5671, 8080, 9090-9091, 9350, 9352, 10100 – 10120.
   >
   >Pour plus d’informations sur la mise à jour de votre version la plus récente toohello connecteurs, consultez [connecteurs de Proxy d’Application Azure de comprendre AD](application-proxy-understand-connectors.md#automatic-updates).

2. Si votre pare-feu ou un proxy autorise liste approuvées DNS, vous pouvez servicebus.windows.net et toomsappproxy.net de connexions de liste blanche. Si non, vous devez tooallow accès toohello [plages d’adresses IP du centre de données Azure](https://www.microsoft.com/download/details.aspx?id=41653), qui sont mis à jour chaque semaine.

3. Microsoft utilise des certificats de tooverify quatre adresses. Autoriser toohello accès aux URL suivantes si vous n’avez pas encore fait pour d’autres produits :
   * mscrl.microsoft.com:80
   * crl.microsoft.com:80
   * ocsp.msocsp.com:80
   * www.microsoft.com:80

4. Votre connecteur doit accès toologin.windows.net et login.microsoftonline.net pour le processus d’inscription de hello.

5. Hello d’utilisation [Azure AD Application Proxy Connector Ports Test outil](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify que votre connecteur pouvez contacter le service de Proxy d’Application hello. Au minimum, assurez-vous que toutes les coches vertes la région du centre des États-Unis hello et tooyou le plus proche de la région de hello. En outre, un nombre plus élevé de coches vertes signifie une résilience accrue.

## <a name="install-and-register-a-connector"></a>Installer et inscrire un connecteur
1. Connectez-vous en tant qu’administrateur Bonjour [portail Azure](https://portal.azure.com/).
2. Votre annuaire actuel s’affiche sous votre nom d’utilisateur dans le coin supérieur droit de hello. Si vous devez les répertoires toochange, sélectionnez cette icône.
3. Accédez trop**Azure Active Directory** > **le Proxy d’Application**.

   ![Accédez tooApplication Proxy](./media/active-directory-application-proxy-enable/app_proxy_navigate.png)

4. Sélectionnez **Télécharger le connecteur**.

   ![Télécharger le connecteur](./media/active-directory-application-proxy-enable/download_connector.png)

5. Exécutez **AADApplicationProxyConnectorInstaller.exe** sur le serveur de hello vous préparé conséquente toohello prerequisites.
6. Suivez les instructions de hello de hello Assistant tooinstall. Pendant l’installation, vous êtes tooregister demandées hello connecteur hello Proxy d’Application de votre client Azure AD.

   * Fournissez vos informations d’identification d’administrateur général d’Azure AD. Votre client d’administrateur global peut être différent de vos informations d’identification Microsoft Azure.
   * Assurez-vous que l’administrateur de hello hello connecteur se trouve dans des registres hello même répertoire où vous avez activé hello service Proxy d’Application. Par exemple, si le domaine du locataire hello est contoso.com, hello admin doit être admin@contoso.com ou tout autre alias sur ce domaine.
   * Si **la Configuration de sécurité renforcée d’Internet Explorer** est défini trop**sur** sur serveur hello où vous installez le connecteur de hello, vous ne voyiez pas l’écran d’enregistrement hello. accès tooget, suivez les instructions dans le message d’erreur hello hello. Vérifiez que la configuration de sécurité renforcée d’Internet Explore est désactivée.

Pour bénéficier d’une haute disponibilité, vous devez déployer au moins deux connecteurs. Chaque connecteur doit être inscrit séparément.

## <a name="test-that-hello-connector-installed-correctly"></a>Tester ce connecteur hello installé correctement

Vous pouvez vérifier qu’un nouveau connecteur installé correctement en vérifiant qu’il soit Bonjour portail Azure ou sur votre serveur. 

Hello portail Azure, se connecter à tooyour locataire et accédez trop**Azure Active Directory** > **le Proxy d’Application**. Tous les connecteurs et les groupes de connecteurs apparaissent sur cette page. Sélectionnez un toosee connecteur ses détails ou déplacez-le dans un groupe de connecteurs différents. 

Sur votre serveur, vérifiez la liste hello des services actifs pour le connecteur de hello et mise à jour du connecteur hello. deux services de Hello doivent démarrer immédiatement, mais dans le cas contraire, les activer : 

   * **connecteur de proxy d’application Microsoft AAD** active la connectivité.

   * **Le programme de mise à jour du connecteur de proxy d’application Microsoft AAD** est un service de mise à jour automatique. mise à jour Hello vérifie les nouvelles versions de connecteur de hello et mises à jour hello connecteur en fonction des besoins.

   ![Services de connecteur de proxy d’application - capture d’écran](./media/active-directory-application-proxy-enable/app_proxy_services.png)

Pour plus d’informations sur les connecteurs et comment ils restent des toodate, consultez [connecteurs de Proxy d’Application Azure de comprendre AD](application-proxy-understand-connectors.md).


## <a name="next-steps"></a>Étapes suivantes
Vous êtes maintenant prêt trop[publier des applications avec Proxy d’Application](application-proxy-publish-azure-portal.md).

Si vous avez des applications qui se trouvent sur des réseaux distincts ou des emplacements différents, utilisez plusieurs connecteurs connecteur groupes tooorganize hello dans des unités logiques. Apprenez-en davantage sur [l’utilisation de connecteurs de proxy d’application](active-directory-application-proxy-connectors-azure-portal.md).
