---
title: aaaActive Directory Federation Services administration et personnalisation avec Azure AD Connect | Documents Microsoft
description: "Gestion d’AD FS avec Azure AD Connect et personnalisation de la connexion de l’utilisateur à AD FS avec Azure AD Connect et PowerShell."
keywords: "AD FS, ADFS, gestion AD FS, AAD Connect, Connect, connexion, personnalisation d’AD FS, réparer l’approbation, O365, fédération, partie de confiance"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a>Gérer et personnaliser Active Directory Federation Services à l’aide d’Azure AD Connect
Cet article décrit comment toomanage et personnaliser des Services de fédération Active Directory (AD FS) à l’aide de Connect de Azure Active Directory (Azure AD). Il inclut également d’autres tâches courantes de AD FS que vous devrez peut-être toodo pour terminer la configuration d’une batterie de serveurs AD FS.

| Rubrique | Sujet traité |
|:--- |:--- |
| **Gérer AD FS** | |
| [Réparation hello approbation](#repairthetrust) |Comment la fédération de hello toorepair faire confiance à Office 365. |
| [Fédérer avec Azure AD à l’aide d’un ID de connexion de substitution](#alternateid) | Configurer la fédération à l’aide d’un ID de connexion de substitution  |
| [Ajout d’un serveur AD FS](#addadfsserver) |Comment tooexpand un AD FS de batterie de serveurs avec un serveur AD FS supplémentaire. |
| [Ajouter un serveur de proxy d’application web AD FS](#addwapserver) |Comment tooexpand un AD FS de batterie de serveurs avec un autre serveur Web Application Proxy (WAP). |
| [Ajout d’un domaine fédéré](#addfeddomain) |Comment tooadd un domaine fédéré. |
| [Mettre à jour le certificat SSL de hello](active-directory-aadconnectfed-ssl-update.md)| Comment tooupdate hello SSL de certificats pour une batterie de serveurs AD FS. |
| **Personnaliser AD FS** | |
| [Ajout d’une illustration ou d’un logo de société personnalisé](#customlogo) |Comment toocustomize un AD FS sign-dans la page avec un logo de société et l’illustration. |
| [Ajout d’une description de connexion](#addsignindescription) |Comment tooadd une connexion dans la page description. |
| [Modification des règles de revendication AD FS](#modclaims) |Comment toomodify AD FS des revendications pour différents scénarios de fédération. |

## <a name="manage-ad-fs"></a>Gérer AD FS
Vous pouvez effectuer diverses tâches AD FS dans Azure AD Connect avec une intervention minime de l’utilisateur à l’aide d’Assistant de hello Azure AD Connect. Une fois que vous avez terminé l’installation d’Azure AD Connect à l’exécution de l’Assistant hello, vous pouvez exécuter les Assistant hello tooperform à nouveau des tâches supplémentaires.

## Réparation hello approbation<a name=repairthetrust></a>
Vous pouvez utiliser Azure AD Connect toocheck hello actuel d’intégrité de hello AD FS et de confiance Azure AD et prendre les mesures appropriées toorepair hello approbation. Suivez ces étapes toorepair votre Azure AD et AD FS de confiance.

1. Sélectionnez **AAD de réparation et de faire confiance à ADFS** à partir de la liste de hello des tâches supplémentaires.
   ![Réparer la confiance AAD et ADFS](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)

2. Sur hello **connecter tooAzure AD** page, fournissez vos informations d’identification d’administrateur global pour Azure AD, puis cliquez sur **suivant**.
   ![Se connecter tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)

3. Sur hello **informations d’identification de l’accès à distance** , entrez les informations d’identification hello pour l’administrateur de domaine hello.

   ![Informations d’identification d’accès à distance](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    Lorsque vous cliquez sur **Suivant**, Azure AD Connect vérifie l’intégrité du certificat et affiche les éventuels problèmes.

    ![État des certificats](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    Hello **tooconfigure prêt** page liste de hello affiche des actions qui seront effectuées approbation de hello toorepair.

    ![Tooconfigure prêt](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. Cliquez sur **installer** toorepair une confiance hello.

> [!NOTE]
> Azure AD Connect peut seulement réparer ou modifier les certificats auto-signés. Azure AD Connect ne permet pas de réparer les certificats tiers.

## Fédération avec Azure AD en utilisant AlternateID <a name=alternateid></a>
Il est recommandé que hello locaux d’utilisateur Principal Name(UPN) et cloud hello nom d’utilisateur Principal sont conservés hello identiques. Si hello UPN sur site utilise un domaine non routable (par ex. Contoso.local) ou ne peut pas être modifiée en raison des dépendances des applications toolocal, nous vous recommandons de configurer des ID de connexion de remplacement. ID de connexion de remplacement vous permet de tooconfigure un signe de rencontrer dans lequel les utilisateurs peuvent se connecter avec un attribut autre que leur UPN, comme le courrier électronique. choix de Hello pour le nom d’utilisateur Principal dans l’attribut de Azure AD Connect par défaut toohello userPrincipalName dans Active Directory. Si vous choisissez n’importe quel autre attribut pour le nom d’utilisateur principal et fédérez avec AD FS, Azure AD Connect configurera AD FS pour l’ID de connexion de substitution. Vous trouverez ci-dessous un exemple de choix d’un autre attribut pour le nom d’utilisateur principal :

![Sélection d’un attribut d’ID de substitution](media/active-directory-aadconnect-federation-management/attributeselection.png)

La configuration d’un ID de connexion de substitution pour AD FS comprend deux étapes principales :
1. **Configurer l’ensemble approprié de hello de revendications d’émission**: règles de revendication d’émission hello dans la partie de confiance hello Azure AD d’approbation sont modifiées toouse hello sélectionné UserPrincipalName attribut comme hello d’un autre ID d’utilisateur de hello.
2. **Activer l’ID de connexion de remplacement dans la configuration de hello AD FS**: configuration de hello AD FS est mis à jour afin que les services AD FS peut rechercher des utilisateurs dans les forêts approprié hello utilisait autre hello Cette configuration est prise en charge pour AD FS sur Windows Server 2012 R2 (avec KB2919355) ou version ultérieure. Si les serveurs hello AD FS sont 2012 R2, les vérifications de Azure AD Connect présence hello Hello requis Ko. Si hello Ko n’est pas détecté, un avertissement s’affiche après la fin de la configuration, comme indiqué ci-dessous :

    ![Avertissement d’absence de base de connaissances sur 2012 R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    configuration de hello toorectify en cas de Ko manquant, installez hello requis [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) , puis réparez à l’aide de confiance hello [AAD de réparer et de niveau de confiance AD FS](#repairthetrust).

> [!NOTE]
> Pour plus d’informations sur toomanually alternateID et les étapes de configuration, lire [configuration d’un autre ID de connexion](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)

## Ajout d’un serveur AD FS <a name=addadfsserver></a>

> [!NOTE]
> serveur de tooadd un AD FS, Azure AD Connect requiert un certificat PFX hello. Par conséquent, vous pouvez effectuer cette opération uniquement si vous avez configuré la batterie de serveurs hello AD FS à l’aide d’Azure AD Connect.

1. Sélectionnez **Déploiement d’un serveur de fédération supplémentaire**, puis cliquez sur **Suivant**.

   ![Serveur de fédération supplémentaire](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. Sur hello **connecter tooAzure AD** page, entrez vos informations d’identification d’administrateur global pour Azure AD, puis cliquez sur **suivant**.

   ![Se connecter tooAzure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. Fournissez les informations d’identification d’administrateur de domaine hello.

   ![Informations d’identification de l’administrateur de domaine](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. Azure AD Connect demande hello de mot de passe du fichier PFX hello que vous avez fourni lors de la configuration de votre nouvelle batterie AD FS avec Azure AD Connect. Cliquez sur **entrer le mot de passe** mot de passe tooprovide hello pour le fichier PFX hello.

   ![Mot de passe du certificat](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Spécifiez le certificat SSL](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. Sur hello **serveurs AD FS** , entrez le nom du serveur hello ou toobe d’adresse IP ajoutée batterie de serveurs toohello AD FS.

   ![Serveurs AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. Cliquez sur **suivant**et parcourez hello final **configurer** page. Une fois Azure AD Connect a fini d’ajouter de batterie de serveurs hello serveurs toohello AD FS, vous aurez connectivité de hello option tooverify hello.

   ![Tooconfigure prêt](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Installation terminée](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## Ajout d’un serveur de proxy d’application web AD FS <a name=addwapserver></a>

> [!NOTE]
> tooadd un serveur WAP, Azure AD Connect requiert un certificat PFX hello. Par conséquent, vous ne pouvez effectuer cette opération que si vous avez configuré la batterie de serveurs hello AD FS à l’aide d’Azure AD Connect.

1. Sélectionnez **déployer le Proxy d’Application Web** à partir de la liste de hello des tâches disponibles.

   ![Déployer le proxy d’application web](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. Fournir les informations d’identification d’administrateur général Azure de hello.

   ![Se connecter tooAzure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. Sur hello **certificat SSL de spécifier** , fournissez le mot de passe hello pour le fichier PFX hello que vous avez fourni lors de la configuration de la batterie de serveurs hello AD FS avec Azure AD Connect.
   ![Mot de passe du certificat](media/active-directory-aadconnect-federation-management/WapServer3.PNG)

    ![Spécifiez le certificat SSL](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. Ajoutez hello server toobe est ajouté comme un serveur WAP. Étant donné que le serveur WAP de hello n’est peut-être pas toohello joint à un domaine, hello dernier demande pour le serveur de toohello les informations d’identification d’administration à ajouter.

   ![Informations d’identification du serveur d’administration](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. Sur hello **informations d’identification de Proxy approbation** , fournissez proxy de hello tooconfigure les informations d’identification d’administration de confiance et accès serveur principal hello dans la batterie de serveurs hello AD FS.

   ![Informations d’identification de confiance du proxy](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. Sur hello **tooconfigure prêt** page, Assistant de hello affiche la liste de hello des actions qui seront effectuées.

   ![Tooconfigure prêt](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. Cliquez sur **installer** configuration de hello toofinish. Une fois la configuration de hello est terminée, Assistant vous propose hello vous hello option tooverify hello serveurs toohello de connectivité. Cliquez sur **Vérifiez** toocheck connectivité.

   ![Installation terminée](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## Ajout d’un domaine fédéré <a name=addfeddomain></a>

Il est facile tooadd un toobe domaine fédéré avec Azure AD à l’aide d’Azure AD Connect. Azure AD Connect ajoute le domaine hello pour la fédération et modifie la revendication hello règles toocorrectly reflètent l’émetteur de hello lorsque vous avez plusieurs domaines fédérés avec Azure AD.

1. tooadd un domaine fédéré, tâche hello sélectionnez **ajouter un domaine Azure AD**.

   ![Domaine Azure AD supplémentaire](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. Sur la page suivante de hello d’Assistant de hello, fournissent des informations d’identification d’administrateur global de hello pour Azure AD.

   ![Se connecter tooAzure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. Sur hello **informations d’identification de l’accès à distance** , fournissez les informations d’identification d’administrateur de domaine hello.

   ![Informations d’identification d’accès à distance](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. Sur la page suivante de hello, Assistant de hello fournit une liste de domaines Azure AD que vous pouvez fédérer votre annuaire local avec. Choisissez le domaine de hello à partir de la liste de hello.

   ![Domaine Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    Après avoir choisi le domaine de hello, Assistant de hello fournit des informations appropriées sur les autres actions hello Assistant prend et hello l’impact de la configuration de hello. Dans certains cas, si vous sélectionnez un domaine qui n’est pas encore vérifié dans Azure AD, Assistant de hello vous fournit des informations toohelp vous vérifiez le domaine de hello. Consultez [ajouter votre tooAzure de nom de domaine personnalisé Active Directory](../active-directory-add-domain.md) pour plus d’informations.

5. Cliquez sur **Suivant**. Hello **tooconfigure prêt** page affiche la liste de hello des actions qui effectue Azure AD Connect. Cliquez sur **installer** configuration de hello toofinish.

   ![Tooconfigure prêt](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> Ajouter des utilisateurs à partir de hello domaine fédéré doit être synchronisée qu’elles soient en mesure de toologin tooAzure AD.

## <a name="ad-fs-customization"></a>Personnalisation d’AD FS
Hello sections suivantes fournissent plus d’informations sur les tâches courantes de hello que vous pouvez avoir tooperform lorsque vous personnalisez votre page de connexion AD FS.

## Ajout d’une illustration ou d’un logo de société personnalisé <a name=customlogo></a>
logo de hello toochange de société hello qui s’affiche sur hello **connexion** page, utilisez hello suivant l’applet de commande Windows PowerShell et la syntaxe.

> [!NOTE]
> Hello recommandée pour le logo de hello sont 260 x 35 96 PPP avec une taille de fichier non supérieure à 10 Ko.

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> Hello *TargetName* paramètre est obligatoire. thème par défaut Hello fourni avec AD FS est nommé par défaut.

## Ajout d’une description de connexion <a name=addsignindescription></a>
tooadd un toohello de description de page de connexion **page de connexion**, utilisez hello suivant l’applet de commande Windows PowerShell et la syntaxe.

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## Modification des règles de revendication AD FS <a name=modclaims></a>
AD FS prend en charge un langage de revendication complet que vous pouvez utiliser les règles de revendication toocreate personnalisé. Pour plus d’informations, consultez [hello rôle Hello Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).

Hello sections suivantes décrivent comment vous pouvez écrire des règles personnalisées pour certains scénarios qui se rapportent tooAzure AD et fédération AD FS.

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a>ID non modifiable conditionnel sur une valeur qui est présent dans l’attribut de hello
Azure AD Connect vous permet de spécifier un toobe de l’attribut utilisé comme une ancre source lorsque les objets sont synchronisés tooAzure AD. Si la valeur hello dans l’attribut personnalisé de hello n’est pas vide, vous pourriez tooissue une revendication d’ID immuable.

Par exemple, vous pouvez sélectionner **ms-ds-consistencyguid** en tant qu’attribut hello pour ancre source de hello et problème **ImmutableID** en tant que **ms-ds-consistencyguid** cas Bonjour attribut a la valeur par rapport à elle. S’il n’existe aucune valeur par rapport à l’attribut de hello, émettre **objectGuid** comme hello immuable ID. Vous pouvez construire ensemble hello de règles de revendication personnalisée comme décrit dans hello suivant la section.

**Règle 1 : attributs de la requête**

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

Dans cette règle, vous interrogez les valeurs hello de **ms-ds-consistencyguid** et **objectGuid** pour utilisateur hello à partir d’Active Directory. Renommer hello magasin nom tooan magasin approprié dans votre déploiement AD FS. Modifiez également hello revendications de type tooa revendications appropriées en type de votre fédération, tel que défini pour **objectGuid** et **ms-ds-consistencyguid**.

En outre, à l’aide **ajouter** et non **problème**, vous évitez d’ajouter un problème sortant pour l’entité de hello et que vous pouvez utiliser des valeurs de hello en tant que valeurs intermédiaires. Vous prévoyez d’émettre revendication hello dans une règle ultérieure après avoir établi le toouse valeur comme hello immuable ID.

**Règle 2 : Vérifier l’existence de ms-ds-consistencyguid pour l’utilisateur de hello**

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

Cette règle définit un indicateur temporaire appelé **idflag** qui est défini trop**useguid** s’il existe aucune **ms-ds-consistencyguid** remplie pour les utilisateurs de hello. logique de Hello derrière cela est fait hello que AD FS n’autorise pas les revendications vides. Donc lorsque vous ajoutez des revendications http://contoso.com/ws/2016/02/identity/claims/objectguid et http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid dans la règle 1, vous vous retrouvez avec une **msdsconsistencyguid** revendication uniquement si valeur de Hello est remplie pour les utilisateur hello. Si elle n’est pas indiquée, AD FS voit que sa valeur sera vide et le supprime immédiatement. Tous les objets auront un **objectGuid**. Donc, cette revendication sera toujours là après l’exécution de la règle 1.

**Règle 3 : émettre ms-ds-consistencyguid comme ID non modifiable s’il est présent**

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

Il s’agit d’un contrôle **Exist** implicite. Si la valeur hello pour hello revendication existe, puis émettre que comme hello immuable ID. Hello l’exemple précédent utilise hello **nameidentifier** de revendication. Vous aurez toochange ce type de revendication appropriées toohello pour l’ID immuable de hello dans votre environnement.

**Règle 4 : émettre objectGuid comme ID non modifiable si ms-ds-consistencyGuid n’est pas présent**

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

Dans cette règle, vous vérifiez simplement indicateur temporaire de hello **idflag**. Vous décidez si tooissue hello revendication basée sur sa valeur.

> [!NOTE]
> séquence Hello de ces règles est important.

### <a name="sso-with-a-subdomain-upn"></a>Authentification unique avec un UPN de sous-domaine
Vous pouvez ajouter plusieurs toobe domaine fédéré à l’aide d’Azure AD Connect, comme décrit dans [ajouter un nouveau domaine fédéré](active-directory-aadconnect-federation-management.md#addfeddomain). Vous devez modifier la revendication de nom principal (UPN) d’utilisateur hello afin que hello ID de l’émetteur correspondant domaine racine de toohello et non de sous-domaine hello, car le domaine racine fédérée de hello couvre également les enfants hello.

Par défaut, hello de règles de revendication pour l’émetteur de l’ID est défini en tant que :

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Revendication de l’ID d’émetteur par défaut](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

règle par défaut de Hello simplement prend suffixe hello et l’utilise dans une revendication d’ID de l’émetteur hello. Par exemple, John est un utilisateur de sub.contoso.com et contoso.com est fédéré à Azure AD. John insère john@sub.contoso.com comme hello du nom d’utilisateur lors de la signature dans tooAzure AD. règle revendication d’ID de l’émetteur par défaut Hello dans AD FS prend en charge Bonjour suivant de manière :

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

**Valeur de revendication :**  http://sub.contoso.com/adfs/services/trust/

toohave uniquement hello domaine racine de l’émetteur de hello valeur de revendication, modifier hello revendication règle toomatch hello suivants :

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur les [options de connexion de l’utilisateur](active-directory-aadconnect-user-signin.md).
