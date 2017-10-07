---
title: "tooSharePoint d’accès à distance aaaEnable avec Proxy d’Application Azure AD | Documents Microsoft"
description: "Traite des concepts de base hello sur la façon toointegrate un serveur de SharePoint sur site avec le Proxy d’Application Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 6ab413462fcaf387e150449df9c97505c4108bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-access-toosharepoint-with-azure-ad-application-proxy"></a>Activer tooSharePoint l’accès à distance avec le Proxy d’Application Azure AD

Cet article explique comment toointegrate un serveur de SharePoint sur site avec le Proxy d’Application Azure Active Directory (Azure AD).

tooSharePoint d’accès à distance tooenable avec Proxy d’Application Azure AD, suivez les sections hello dans cet article étape par étape.

## <a name="prerequisites"></a>Composants requis

Cet article suppose que vous avez déjà SharePoint 2013 ou une version plus récente dans votre environnement. En outre, tenez compte des hello suivant des conditions préalables :

* SharePoint comprend la prise en charge native de Kerberos. Par conséquent, les utilisateurs qui accèdent à des sites internes à distance via le Proxy d’Application Azure AD peuvent supposer toohave une-session unique (SSO de) l’expérience.

* Vous avez besoin toomake quelques configuration modifications tooyour SharePoint serveur. Nous vous recommandons d’utiliser un environnement intermédiaire. De cette manière, vous pouvez rendre tooyour mises à jour tout d’abord de serveur de test et puis faciliter un cycle de test avant de passer en production.

* Nous supposons que vous avez déjà configuré SSL pour SharePoint, car nous avons besoin de que SSL sur hello publié URL. Vous devez toohave que SSL est activé sur votre site interne, tooensure que des liens sont envoyés/correctement mappés. Si vous n’avez pas configuré SSL, consultez le blog [Configure SSL for SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) pour obtenir des instructions. En outre, assurez-vous que hello connecteur approbations hello certificat d’ordinateur que vous émettez. (les certificats hello n’est pas nécessaire à toobe publiquement émis.)

## <a name="step-1-set-up-single-sign-on-toosharepoint"></a>Étape 1 : Configurer tooSharePoint de l’authentification unique

Nos clients souhaitent hello expérience d’authentification meilleures pour leurs applications principales, SharePoint server dans ce cas. Dans ce scénario courant d’Azure AD, utilisateur de hello est authentifié qu’une seule fois, car ils ne seront pas demandées pour l’authentification à nouveau.

Pour les applications sur site ou utilisent l’authentification Windows, vous pouvez obtenir l’authentification unique à l’aide de protocole d’authentification Kerberos hello et une fonctionnalité appelée la délégation Kerberos contrainte (KCD). KCD, lors de la configuration, permet à un windows tooobtain de connecteur de Proxy d’Application hello ticket et le jeton pour un utilisateur, même si l’utilisateur de hello n’est pas connecté directement tooWindows. toolearn en savoir plus sur KCD, consultez [présentation de délégation contrainte Kerberos](https://technet.microsoft.com/library/jj553400.aspx).

tooset de KCD pour un serveur SharePoint, et utiliser des procédures hello Bonjour les sections séquentielles suivantes :

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a>Vérifier que SharePoint s’exécute sous un compte de service

Tout d’abord, vérifiez que SharePoint s’exécute sous un compte de service défini, et non sous le système local, le service local ou le service réseau. Cela afin que vous pouvez attacher le compte de service (SPN) de noms principal tooa valide. Noms principaux de service sont comment hello protocole Kerberos identifie les différents services. Et vous devez serez hello compte ultérieure tooconfigure hello KCD.

tooensure vos sites sont en cours d’exécution sous un compte de service définis, effectuez hello comme suit :

1. Ouvrez hello **Administration centrale de SharePoint 2013** site.
2. Accédez trop**sécurité** et sélectionnez **configurer des comptes de service**.
3. Sélectionnez **Pool d’applications web - SharePoint - 80**. options de Hello peuvent être légèrement différentes selon le nom de hello de votre pool de web, ou si hello pool web utilise SSL par défaut.

  ![Choix disponibles pour configurer un compte de service](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. Si **sélectionner un compte pour ce composant** est **Service Local** ou **Service réseau**, vous devez toocreate un compte. Si ce n’est pas le cas, vous avez terminé et que vous pouvez déplacer toohello la prochaine section.
5. Choisissez **Enregistrer le nouveau compte géré**. Une fois votre compte est créé, vous devez définir **Pool d’applications Web** avant de pouvoir utiliser le compte de hello.

> [!NOTE]
Vous devez toohave a déjà créé le compte Azure AD pour le service de hello. Nous vous suggérons d’autoriser une modification de mot de passe automatique. Pour plus d’informations sur l’ensemble complet de hello d’étapes et de résolution des problèmes, consultez [configurer des modifications de mot de passe automatique dans SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).

### <a name="configure-sharepoint-for-kerberos"></a>Configurer SharePoint pour Kerberos

Vous utilisez KCD tooperform unique authentification toohello SharePoint server, et cela fonctionne uniquement avec Kerberos.

tooconfigure de site SharePoint pour l’authentification Kerberos :

1. Ouvrez hello **Administration centrale de SharePoint 2013** site.
2. Accédez trop**gestion des applications**, sélectionnez **gérer les applications web**et sélectionnez votre site SharePoint. Dans cet exemple, il s’agit de **SharePoint - 80**.

  ![Sélection d’un site SharePoint hello](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. Cliquez sur **fournisseurs d’authentification** sur la barre d’outils hello.
4. Bonjour **fournisseurs d’authentification** , cliquez sur **Zone par défaut** tooview les paramètres hello.
5. Bonjour **modifier l’authentification** boîte de dialogue zone, faites défiler vers le bas jusqu'à ce que vous voyiez **Types de revendications d’authentification** et vérifiez que les deux **activer l’authentification Windows** et  **L’authentification intégrée Windows** sont sélectionnés.
6. Dans la zone de liste déroulante hello, assurez-vous que **négocier (Kerberos)** est sélectionnée.

  ![Boîte de dialogue Modifier l’authentification](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. En bas de hello Hello **modifier l’authentification** boîte de dialogue, cliquez sur **enregistrer**.

### <a name="set-a-service-principal-name-for-hello-sharepoint-service-account"></a>Définir un nom principal de service pour le compte de service SharePoint de hello

Avant de configurer hello KCD, vous devez le service SharePoint de tooidentify hello en cours d’exécution en tant que compte de service hello que vous avez configurée. Pour cela, définissez un nom de principal de service. Pour plus d'informations, consultez la page [Noms de principal de service](https://technet.microsoft.com/library/cc961723.aspx).

format des SPN Hello est la suivante :

```
<service class>/<host>:<port>
```

Dans le format des SPN hello :

* _classe de service_ est un nom unique pour le service de hello. Pour SharePoint, vous utilisez **HTTP**.

* _hôte_ est hello nom de domaine complet ou le nom NetBIOS de l’ordinateur hôte hello hello service est en cours d’exécution. Pour un site SharePoint, ce texte peut-être toobe des URL de hello du site hello, selon la version de hello d’IIS que vous utilisez.

* _port_ est facultatif.

Si hello FQDN du serveur SharePoint de hello est :

```
sharepoint.demo.o365identity.us
```

Puis hello SPN est la suivante :

```
HTTP/ sharepoint.demo.o365identity.us demo
```

Vous devrez peut-être également tooset SPN pour des sites spécifiques sur votre serveur. Pour plus d’informations, consultez [Configurer l’authentification Kerberos](https://technet.microsoft.com/library/cc263449(v=office.12).aspx). Payer attentif toohello section « Créer des noms principaux de Service pour vos applications Web à l’aide de l’authentification Kerberos ».

Hello plus simple pour tooset SPN est toofollow les formats de SPN hello qui peuvent déjà être présents pour vos sites. Copiez ces tooregister SPN sur le compte de service hello. toodo cela :

1. Parcourir le site toohello avec hello SPN à partir d’un autre ordinateur.
 Lorsque vous, hello ensemble approprié des tickets Kerberos est mis en cache sur l’ordinateur de hello. Ces tickets contiennent hello SPN du site hello cible que vous avez accédé à.

2. Vous pouvez extraire hello SPN pour le site à l’aide d’un outil appelé [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html). Dans une fenêtre de commande qui s’exécute dans hello même contexte en tant qu’utilisateur hello qui exécutera le site d’accès hello dans le navigateur de hello, hello la commande suivante :
```
Klist
```
Klist retourne ensuite un jeu hello de cible de noms principaux de service. Dans cet exemple, valeur de hello mis en surbrillance est hello SPN que nécessaire :

  ![Exemples de résultats de l’outil Klist](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. Maintenant que vous avez hello SPN, vous devez toomake Vérifiez qu’il est correctement configuré sur le compte de service hello que vous avez configurée pour l’application web de hello précédemment. Exécutez hello de commande suivante à partir de l’invite de commandes hello en tant qu’administrateur de domaine de hello :

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 Cette commande définit hello SPN pour le service SharePoint de hello compte en cours d’exécution en tant que _demo\sp_svc_.

 Remplacez _http/sharepoint.demo.o365identity.us_ avec hello nom principal de service pour votre serveur et _demo\sp_svc_ avec le compte de service hello dans votre environnement. commande de Setspn Hello recherche hello SPN avant qu’il l’ajoute. Dans le cas présent, l’erreur **Valeur de SPN dupliquée** peut s’afficher. Si vous voyez cette erreur, assurez-vous que la valeur de hello est associé au compte de service hello.

Vous pouvez vérifier que hello que SPN a été ajouté en exécutant la commande de Setspn hello avec hello -l, option. toolearn en savoir plus sur cette commande, consultez [Setspn](https://technet.microsoft.com/library/cc731241.aspx).

### <a name="ensure-that-hello-connector-is-set-as-a-trusted-delegate-toosharepoint"></a>Vérifiez que le connecteur hello est défini comme un tooSharePoint délégué approuvé

Configurer hello KCD afin que le service de Proxy d’Application Azure AD hello peut déléguer le service de SharePoint toohello utilisateur identités. Cela en activant le connecteur de Proxy d’Application hello tooretrieve les tickets Kerberos pour les utilisateurs qui ont été authentifiés dans Azure AD. Ce serveur transmet ensuite hello contexte toohello cible application ou SharePoint dans ce cas.

tooconfigure hello KCD, hello Répétez ces étapes pour chaque ordinateur de connecteur comme suit :

1. Connectez-vous en tant qu’un tooa d’administrateur de domaine contrôleur de domaine, puis ouvrez **Active Directory Users and Computers**.
2. Trouver l’ordinateur hello hello connecteur est en cours d’exécution. Dans cet exemple, il a hello même serveur SharePoint.
3. Double-cliquez sur hello ordinateur, puis cliquez sur hello **délégation** onglet.
4. Vérifiez que les paramètres de délégation hello sont définies trop**n’approuver cet ordinateur pour toohello délégation spécifié services uniquement**, puis sélectionnez **utiliser tout protocole d’authentification**.

  ![Paramètres de délégation](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. Cliquez sur hello **ajouter** et sur **utilisateurs ou ordinateurs**et recherchez le compte de service hello.

  ![Ajout hello SPN pour le compte de service hello](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. Dans liste hello de SPN, sélectionnez hello une que vous avez créé précédemment pour le compte de service hello.
7. Cliquez sur **OK**. Cliquez sur **OK** à nouveau les modifications toosave hello.

## <a name="step-2-enable-remote-access-toosharepoint"></a>Étape 2 : Activer l’accès à distance tooSharePoint

Maintenant que vous avez activée SharePoint pour Kerberos et configuré KCD, vous êtes prêt tooset des tooSharePoint de l’authentification unique. Connecteur de hello, vous pouvez ensuite publier batterie de serveurs SharePoint hello pour l’accès à distance via le Proxy d’Application Azure AD.

tooperform hello comme suit, vous devez toobe un membre du rôle Administrateur général de hello dans un compte Azure Active Directory de votre organisation.

1. Connectez-vous à toohello [portail Azure](https://manage.windowsazure.com) et recherchez votre locataire Azure AD.
2. Cliquez sur **Applications**, puis sur **Ajouter**.
3. Sélectionnez **Publier une application qui sera accessible depuis l’extérieur de votre réseau**. Si vous ne voyez pas cette option, assurez-vous que vous avez Azure AD Basic ou Premium configuré dans le locataire de hello.
4. Chacune des options de hello procédez comme suit :
 * **Nom** : utilisez la valeur de votre choix, par exemple **SharePoint**.
 * **URL interne**: hello les URL du site SharePoint de hello en interne, telles que **https://SharePoint/**. Dans cet exemple, assurez-vous que toouse **https**.
 * **Méthode de préauthentification** : sélectionnez **Azure Active Directory**.

  ![Options d’ajout d’une application](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. Une fois l’application hello est publiée, cliquez sur hello **configurer** onglet.
6. Faites défiler vers le bas toohello option **traduire les URL dans les en-têtes**. la valeur par défaut Hello est **Oui**. Modifier trop**non**.

 SharePoint utilise hello _en-tête d’hôte_ toolook valeur site de hello. Il génère également des liens en fonction de cette valeur. effet net de Hello est toomake assurer que les liens qui génère de SharePoint sont une URL publiée est correctement définie l’URL externe de toouse hello. Valeur hello trop**Oui** également Active hello connecteur tooforward hello demande toohello application d’arrière-plan. Toutefois, valeur hello trop**non** signifie que le connecteur de hello n’envoie pas de nom d’hôte interne hello. Au lieu de cela, connecteur de hello envoie des en-tête d’hôte hello hello publié l’application principale de toohello URL.

 En outre, tooensure que SharePoint accepte cette URL, vous devez toocomplete davantage de configuration sur le serveur SharePoint de hello. Vous devez le faire dans la section suivante de hello.

7. Modification **méthode d’authentification interne** trop**l’authentification Windows intégrée**. Si votre client Azure AD utilise un nom UPN dans le cloud de hello est différente de hello UPN local, n’oubliez pas tooupdate **identité déléguée** également.
8. Définissez **SPN d’Application interne** toohello valeur que vous avez définis précédemment. Par exemple, utilisez **http/sharepoint.demo.o365identity.us**.
9. Affecter des utilisateurs cibles hello application tooyour.

Votre application doit se présenter comme toohello l’exemple suivant :

  ![Application achevée](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-hello-external-url"></a>Étape 3 : Vérifier que SharePoint connaît hello des URL externe

Votre dernière tooensure étape que SharePoint peut trouver site hello basé sur l’URL externe de hello, afin qu’il doit rendre les liens en fonction de cette URL externe. Pour cela, en configurant des mappages des accès de substitution pour un site SharePoint hello.

1. Ouvrez hello **Administration centrale de SharePoint 2013** site.
2. Sous **Paramètres système**, sélectionnez **Configurer des mappages d’accès alternatifs**.

 Cette opération ouvre hello **mappages des accès de substitution** boîte.

  ![Zone Mappages des accès de substitution](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. Dans hello liste déroulante, en regard de **autre Collection de mappages des accès**, sélectionnez **modifier la Collection de mappages des accès de substitution**.
4. Sélectionnez votre site, par exemple **SharePoint - 80**.

  ![Sélection d’un site](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. Vous pouvez choisir de tooadd hello publié URL comme une URL interne ou une URL publique. Cet exemple utilise une URL publique comme hello extranet.
6. Cliquez sur **modifier les URL publiques** Bonjour **Extranet** chemin d’accès, puis entrez chemin hello pour hello publié l’application, comme à l’étape précédente de hello. Par exemple, entrez **https://sharepoint-iddemo.msappproxy.net**.

  ![Entrez le chemin d’accès de hello](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. Cliquez sur **Enregistrer**.

 Vous pouvez désormais accéder à un site SharePoint hello en externe via le Proxy d’Application Azure AD.

## <a name="next-steps"></a>Étapes suivantes

- [Comment tooprovide sécuriser l’accès à distance des applications tooon-site](active-directory-application-proxy-get-started.md)
- [Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md)
- [Publication de SharePoint 2016 et d’Office Online Server avec le proxy d’application Azure AD](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
