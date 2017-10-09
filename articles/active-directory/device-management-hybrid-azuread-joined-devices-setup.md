---
title: "aaaHow tooconfigure hybride Azure Active Directory des appareils joints à un | Documents Microsoft"
description: "Découvrez comment tooconfigure hybride Azure Active Directory appareils joints à un."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: f97ea436eca2833d8a9843acd19e5c633bc0fc07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-hybrid-azure-active-directory-joined-devices"></a>Comment tooconfigure hybride Azure Active Directory appareils joints à un

La fonction de gestion des appareils intégrée à Azure Active Directory (Azure AD) vous permet de vous assurer que vos utilisateurs accèdent à vos ressources à partir d’appareils qui répondent à vos normes de conformité et de sécurité. Pour plus d’informations, consultez [gestion toodevice de présentation dans Azure Active Directory](device-management-introduction.md).

Si vous avez un environnement d’Active Directory local et que vous souhaitez toojoin votre tooAzure périphériques joints au domaine Active Directory, ce faire en configurant hybrides Azure AD joint périphériques. rubrique de Hello fournit hello étapes. 


## <a name="before-you-begin"></a>Avant de commencer

Avant de commencer la configuration des appareils joints à hybrides Azure AD dans votre environnement, vous devez vous familiariser avec les scénarios hello pris en charge et des contraintes de hello.  

une meilleure lisibilité des hello tooimprove des descriptions de hello, cette rubrique utilise hello suivant le terme : 

- **Les appareils Windows actuels** -ce terme fait référence à des appareils appartenant à un toodomain exécutant Windows 10 ou Windows Server 2016.
- **Les appareils Windows de bas niveau** -ce terme fait référence tooall **pris en charge** appareils Windows joints à un domaine qui sont en cours d’exécution Windows 10 ni Windows Server 2016.  


### <a name="windows-current-devices"></a>Appareils Windows actuels

- Pour les périphériques exécutant le système d’exploitation de bureau Windows hello, nous vous recommandons d’à l’aide de la mise à jour de la date anniversaire Windows 10 (version 1607) ou version ultérieure. 
- Hello d’inscription d’appareils en cours de Windows **est** pris en charge dans les environnements non fédérées telles que les configurations de synchronisation de hachage de mot de passe.  


### <a name="windows-down-level-devices"></a>Appareils Windows de bas niveau

- Hello suivant de périphériques de bas niveau de Windows est prises en charge :
    - Windows 8.1
    - Windows 7
    - Windows Server 2012 R2
    - Windows Server 2012
    - Windows Server 2008 R2
- Hello d’inscription d’appareils de bas niveau Windows **est** pris en charge dans les environnements non fédérées via transparente Single Sign On [Azure Active Directory transparente l’authentification unique sur](https://aka.ms/hybrid/sso).
- Hello d’inscription d’appareils de bas niveau Windows **n’est pas** pris en charge pour les appareils à l’aide de profils itinérants. Si vous vous appuyez sur l’itinérance de profils ou de paramètres, utilisez Windows 10.



## <a name="prerequisites"></a>Composants requis

Avant de commencer l’activation de dispositifs de Azure AD joint hybrides dans votre organisation, vous devez toomake que que vous exécutez une version à jour d’Azure AD se connecter.

Azure AD Connect :

- Conserve l’association hello entre le compte d’ordinateur hello dans vos locaux Active Directory (AD) et un objet de périphérique hello dans Azure AD. 
- Permet d’utiliser d’autres fonctionnalités liées aux appareils telles que Windows Hello Entreprise.



## <a name="configuration-steps"></a>Configuration

Vous pouvez configurer des appareils hybrides joints à Azure AD pour différents types de plateformes d’appareils Windows. Cette rubrique comprend les étapes hello requis pour tous les scénarios courants de configuration.  

Utilisez hello suivant table tooget une vue d’ensemble des étapes hello qui sont requis pour votre scénario :  



| Étapes                                      | Appareils Windows actuels et synchronisation du hachage de mot de passe | Appareils Windows actuels et fédération | Appareils Windows de bas niveau |
| :--                                        | :-:                                    | :-:                            | :-:                |
| Étape 1 : Configuration du point de connexion de service | ![Vérification][1]                            | ![Vérification][1]                    | ![Vérification][1]        |
| Étape 2 : Configuration de l’émission de revendications           |                                        | ![Vérification][1]                    | ![Vérification][1]        |
| Étape 3 : Activation d’appareils non-Windows 10      |                                        |                                | ![Vérification][1]        |
| Étape 4 : Contrôle du déploiement et du lancement     | ![Vérification][1]                            | ![Vérification][1]                    | ![Vérification][1]        |
| Étape 5 : Vérification des appareils joints          | ![Vérification][1]                            | ![Vérification][1]                    | ![Vérification][1]        |



## <a name="step-1-configure-service-connection-point"></a>Étape 1 : Configuration du point de connexion de service

objet de point de connexion de service Hello est utilisé par vos périphériques pendant l’inscription de hello toodiscover informations du locataire Azure AD. Dans vos locaux Active Directory (AD), objet hello SCP pour les appareils Azure AD joint hello hybride doit exister dans hello d’affectation de noms contexte partition de configuration de la forêt de l’ordinateur hello. Il n’existe qu’un seul contexte d’appellation de configuration par forêt. Dans une configuration d’Active Directory de forêts multiples, le point de connexion de service hello doit exister dans toutes les forêts contenant des ordinateurs joints au domaine.

Vous pouvez utiliser hello [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) applet de commande tooretrieve hello configuration contexte d’appellation de votre forêt.  

Pour une forêt avec le nom de domaine Active Directory hello *fabrikam.com*, contexte d’appellation de configuration hello est :

`CN=Configuration,DC=fabrikam,DC=com`

Dans votre forêt, objet hello SCP pour hello auto-inscription de périphériques joints au domaine se trouve dans :  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

Selon la façon dont vous avez déployé Azure AD Connect, objet de SCP hello peut ont déjà été configurée.
Vous pouvez vérifier l’existence de hello d’objet de hello et récupérer des valeurs de découverte hello à l’aide de hello Windows PowerShell script suivant : 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

Hello **$scp. Mots clés** sortie affiche les informations du locataire hello Azure AD, par exemple :

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

Si le point de connexion de service hello n’existe pas, vous pouvez le créer en exécutant hello `Initialize-ADSyncDomainJoinedComputerSync` applet de commande sur votre serveur Azure AD Connect. Informations d’identification de Enterprise admin est obligatoire toorun cette applet de commande.  
applet de commande Hello :

- Crée le point de connexion de service hello dans la forêt Active Directory de hello À qu'azure AD Connect est connecté. 
- Requiert que vous toospecify hello `AdConnectorAccount` paramètre. Il s’agit de compte hello qui est configuré en tant que compte de connecteur dans Azure AD de se connecter de Active Directory. 


Hello script suivant montre un exemple d’utilisation d’applet de commande hello. Dans ce script, `$aadAdminCred = Get-Credential` nécessite que vous tootype un nom d’utilisateur. Vous avez besoin de nom d’utilisateur hello tooprovide hello format nom utilisateur principal (UPN) (`user@example.com`). 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

Hello `Initialize-ADSyncDomainJoinedComputerSync` applet de commande :

- Utilise le module Active Directory PowerShell hello, qui s’appuie sur les Services Web Active Directory s’exécutant sur un contrôleur de domaine. Les services Web Active Directory sont pris en charge sur les contrôleurs de domaine exécutant Windows Server 2008 R2 et les versions ultérieures.
- Est uniquement pris en charge par hello **MSOnline PowerShell version du module 1.1.166.0**. toodownload ce module, utilisez cette [lien](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).   

Pour les contrôleurs de domaine exécutant Windows Server 2008 ou versions antérieures, utilisez le script de hello sous le point de connexion de service toocreate hello.

Dans une configuration à plusieurs forêts, vous devez utiliser hello suivant le point de connexion de service script toocreate hello dans chaque forêt où les ordinateurs existent :
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a>Étape 2 : Configuration de l’émission de revendications

Dans Azure fédéré configuration d’Active Directory, les appareils s’appuient sur les Services de fédération Active Directory (AD FS) ou un tiers 3e localement tooAzure de tooauthenticate service de fédération Active Directory. Les appareils s’authentifient tooget un tooregister de jeton d’accès contre hello Azure Active Directory Device Registration Service (DRS Azure).

Les appareils en cours s’authentifient à l’aide de l’authentification Windows intégrée tooan WS-Trust point de terminaison actif (versions 1.3 ou 2005) hébergé par le service de fédération local hello de Windows.

> [!NOTE]
> En cas d’utilisation d’AD FS, il est nécessaire d’activer **adfs/services/trust/13/windowstransport** ou **adfs/services/trust/2005/windowstransport**. Si vous utilisez hello Web d’authentification Proxy, vérifiez également que ce point de terminaison est publié via le proxy hello. Vous pouvez voir les points d’arrêt sont activés via la console de gestion hello AD FS sous **Service > points de terminaison**.
>
>Si vous n’avez pas AD FS en tant que votre service de fédération local, suivez les instructions de hello de votre fournisseur de toomake assurer qu’ils prennent en charge WS-Trust 1.3 ou des points de terminaison 2005 et qu’ils sont publiés via hello fichier d’échange de métadonnées (MEX).

Hello revendications suivantes doivent exister dans le jeton hello reçue par le service DRS Azure pour toocomplete d’inscription de périphérique. DRS Azure crée un objet de périphérique dans Azure AD avec certaines de ces informations sont ensuite utilisées par l’objet de périphérique Azure AD Connect tooassociate hello nouvellement créée avec hello ordinateur compte local.

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

Si vous avez plusieurs noms de domaine vérifié, vous devez hello tooprovide suivant revendication pour les ordinateurs :

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

Si vous émettez déjà une revendication ImmutableID (par exemple, les ID de connexion de substitution), vous devez tooprovide une revendication correspondante pour les ordinateurs :

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

Dans les sections suivantes de hello, trouver des informations sur :
 
- les valeurs Hello chaque revendication doit avoir.
- L’aspect d’une définition dans AD FS

définition de Hello vous aide à tooverify si les valeurs hello sont présentes, ou si vous avez besoin de toocreate les.

> [!NOTE]
> Si vous n’utilisez pas AD FS pour votre serveur de fédération local, suivez tooissue de configuration approprié de votre fournisseur instructions toocreate hello ces revendications.

### <a name="issue-account-type-claim"></a>Émission de la revendication du type de compte

**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Cette revendication doit contenir une valeur de **DJ**, qui identifie le périphérique hello en tant qu’un ordinateur joint au domaine. Dans AD FS, vous pouvez ajouter une règle de transformation d’émission ressemblant à ceci :

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a>ObjectGUID de problème de hello ordinateur compte local

**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Cette revendication doit contenir hello **objectGUID** valeur Hello local compte d’ordinateur. Dans AD FS, vous pouvez ajouter une règle de transformation d’émission ressemblant à ceci :

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a>Émettre objectSID de hello ordinateur compte local

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Cette revendication doit contenir Bonjour Bonjour **objectSid** valeur Hello local compte d’ordinateur. Dans AD FS, vous pouvez ajouter une règle de transformation d’émission ressemblant à ceci :

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a>Émission de la valeur issuerID pour l’ordinateur s’il existe plusieurs noms de domaine vérifiés dans Azure AD

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Cette revendication doit contenir hello identificateur URI (Uniform Resource) de n’importe quel Hello vérifié les noms de domaine qui se connectent avec hello localement le jeton de hello émettrice federation Services (AD FS ou 3e partie). Dans AD FS, vous pouvez ajouter des règles de transformation d’émission qui ressemblent à celles hello ci-dessous dans la mesure où un ordre spécifique après ceux hello ci-dessus. Notez qu’un tooexplicitly problème hello la règle pour les utilisateurs est nécessaire. Dans les règles de hello ci-dessous, une première règle identifiant utilisateur ou l’authentification d’ordinateur est ajoutée.

    @RuleName = "Issue account type with hello value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


Dans la revendication hello ci-dessus,

- `$<domain>`est l’URL du service hello AD FS
- `<verified-domain-name>`est un espace réservé que vous avez besoin de tooreplace avec l’un de vos noms de domaine vérifié dans Azure AD



Pour plus d’informations sur les noms de domaine vérifié, consultez [ajouter un tooAzure de nom de domaine personnalisé Active Directory](active-directory-add-domain.md).  
tooget une liste de vos domaines de société vérifiés, vous pouvez utiliser hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) applet de commande. 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a>Émission de la valeur ImmutableID pour l’ordinateur s’il en existe une pour les utilisateurs (par exemple, définition d’un ID de connexion alternatif)

**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** : cette revendication doit contenir une valeur valide pour les ordinateurs. Dans AD FS, vous pouvez créer une règle de transformation d’émission comme suit :

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a>Règles de transformation d’émission d’application d’assistance script toocreate hello AD FS

Hello script suivant vous aide à avec création de hello d’émission de hello transformer les règles décrites ci-dessus.

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a>Remarques 

- Ce script ajoute des règles existantes de hello règles toohello. N’exécutez ne pas hello script à deux reprises car hello ensemble de règles est ajouté à deux reprises. Assurez-vous qu’aucune règle correspondant n’existe pour ces revendications (dans des conditions hello) avant de réexécuter le script de hello.

- Si vous avez plusieurs noms de domaine vérifié (comme indiqué dans le portail de hello Azure AD ou via l’applet de commande Get-MsolDomains de hello), valeur hello **$multipleVerifiedDomainNames** Bonjour script trop**$true**. Veillez également à supprimer toute revendication issuerid existante pouvant avoir été créée par Azure AD Connect ou par d’autres moyens. Voici un exemple de cette règle :


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- Si vous avez déjà émis un **ImmutableID** de revendication pour les comptes d’utilisateur, la valeur hello **$immutableIDAlreadyIssuedforUsers** Bonjour script trop**$true**.

## <a name="step-3-enable-windows-down-level-devices"></a>Étape 3 : Activation des appareils Windows de bas niveau

Si certains de vos appareils joints à un domaine sont des appareils Windows de bas niveau, vous devez :

- Définir une stratégie dans Azure AD tooenable tooregister les appareils des utilisateurs.
 
- Configurer votre toosupport revendications tooissue de service de fédération local **l’authentification Windows (intégrée)** pour l’inscription de périphérique.
 
- Ajoutez des hello Azure AD appareil authentification point de terminaison toohello local Intranet zones tooavoid certificat invite lors de l’authentification d’appareil de hello.

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a>Définir la stratégie dans Azure AD tooenable tooregister les appareils des utilisateurs

périphériques de bas niveau tooregister Windows, vous devez toomake que ce hello définissant tooallow utilisateurs tooregister appareils dans Azure AD est défini. Bonjour portail Azure, vous pouvez trouver ce paramètre sous :

`Azure Active Directory > Users and groups > Device settings`
    
Hello stratégie suivante doit être défini trop**tous les**: **les utilisateurs peuvent inscrire leurs appareils auprès d’Azure AD**

![Inscrire des appareils](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a>Configurer le service de fédération local 

Votre service de fédération local doit prendre en charge hello émettrice **authenticationmehod** et **wiaormultiauthn** revendications lors de la réception d’une authentification demande toohello Azure AD de confiance contenant un resouce_params paramètre avec une valeur codée comme indiqué ci-dessous :

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

Lorsqu’une telle demande est fourni, service de fédération local hello doit authentifier l’utilisateur hello à l’aide de l’authentification Windows intégrée et en cas de réussite, elle doit émettre hello suivant deux revendications :

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

Dans AD FS, vous devez ajouter une règle de transformation d’émission de cette méthode d’authentification transmet via hello.  

**tooadd cette règle :**

1. Dans la console de gestion hello AD FS, accédez trop`AD FS > Trust Relationships > Relying Party Trusts`.
2. Objet d’approbation de partie de confiance de plateforme d’identité Microsoft Office 365 hello d’avec le bouton droit et sélectionnez **modifier les règles de revendication**.
3. Sur hello **règles de transformation d’émission** onglet, sélectionnez **ajouter une règle**.
4. Bonjour **règle de revendication** liste des modèles, sélectionnez **envoyer des revendications à l’aide d’une règle personnalisée**.
5. Sélectionnez **Suivant**.
6. Bonjour **nom de règle de revendication** , tapez **règle de revendication de méthode d’authentification**.
7. Bonjour **règle de revendication** boîte, hello type règle :

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. Sur votre serveur de fédération, tapez la commande PowerShell de hello ci-dessous après le remplacement  **\<RPObjectName\>**  avec hello partie de confiance nom de l’objet pour votre objet Azure AD approbation de partie de confiance. Cet objet est généralement nommé **plateforme d’identité Microsoft Office 365**.
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a>Ajouter des zones Intranet Local de hello Azure AD appareil authentification point d’arrêt toohello

certificat de tooavoid invite lorsque les utilisateurs de périphériques de Registre authentifient tooAzure AD, vous pouvez transmettre un Bonjour de tooadd stratégie tooyour périphériques joints au domaine suivant la zone d’Intranet Local toohello URL dans Internet Explorer :

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a>Étape 4 : Contrôle du déploiement et du lancement

Lorsque vous avez terminé les étapes de hello requis, les périphériques joints au domaine sont tooautomatically prêt jointure Azure AD :

- Tous les appareils joints à un domaine qui exécutent Mise à jour anniversaire Windows 10 et Windows Server 2016 s’inscrivent automatiquement auprès d’Azure AD lors du redémarrage des appareils ou de la connexion des utilisateurs. 

- Nouveaux périphériques s’inscrire auprès d’Azure AD quand les appareils hello redémarre après que l’opération de jointure de domaine hello est terminée.

- Inscrit des appareils qui ont été précédemment Azure AD (par exemple, pour Windows Intune) trop de transition «*joints à un domaine, enregistré avec AAD*« ; toutefois il prend un certain temps pour toocomplete de ce processus sur tous les périphériques en raison de toohello le flux normal de activité des utilisateurs et de domaine.

### <a name="remarks"></a>Remarques

- Vous pouvez utiliser un déploiement de hello de toocontrol d’objet stratégie de groupe de l’inscription automatique de Windows 10 et les ordinateurs joints à un domaine Windows Server 2016.

- Windows 10 novembre 2015 mise à jour se connecte automatiquement auprès d’Azure AD **uniquement** si l’objet de stratégie de groupe de déploiement hello est définie.

- toorollout des ordinateurs de bas niveau de Windows, vous pouvez déployer un [package Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toocomputers que vous sélectionnez.

- Si vous envoyez des appareils joints au domaine hello stratégie de groupe objet tooWindows 8.1, une jointure est tentée ; Il est toutefois recommandé d’utiliser hello [package Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toojoin tous vos appareils de bas niveau de Windows. 

### <a name="create-a-group-policy-object"></a>Créer un objet de stratégie de groupe 

lancement de hello toocontrol des ordinateurs en cours de Windows, vous devez déployer hello **inscrire des ordinateurs joints au domaine en tant qu’appareils** stratégie de groupe objet toohello périphériques tooregister. Par exemple, vous pouvez déployer hello stratégie tooan unité ou le groupe de sécurité tooa.

**stratégie tooset hello :**

1. Ouvrez **le Gestionnaire de serveur**, puis passez trop`Tools > Group Policy Management`.
2. Atteindre le nœud de domaine toohello correspondant toohello domaine dans lequel tooactivate-d’enregistrement automatique des ordinateurs en cours de Windows.
3. Cliquez avec le bouton droit sur **Objets de stratégie de groupe**, puis sélectionnez **Nouveau**.
4. Entrez un nom pour votre objet de stratégie de groupe. Par exemple, *jonction Azure AD hybride. 
5. Cliquez sur **OK**.
6. Cliquez avec le bouton droit sur votre nouvel objet de stratégie de groupe, puis sélectionnez **Modifier**.
7. Accédez trop**Configuration ordinateur** > **stratégies** > **modèles d’administration** > **Windows Composants** > **DRS**. 
8. Cliquez avec le bouton droit sur **Enregistrer les ordinateurs appartenant à un domaine en tant qu’appareils**, puis sélectionnez **Modifier**.
   
   > [!NOTE]
   > Ce modèle de stratégie de groupe a été renommé à partir de versions antérieures de la console de gestion des stratégies de groupe hello. Si vous utilisez une version antérieure de la console de hello, passez trop`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`. 

7. Sélectionnez **Activé**, puis cliquez sur **Appliquer**.
8. Cliquez sur **OK**.
9. Hello lien emplacement de tooa d’objet de stratégie de groupe de votre choix. Par exemple, vous pouvez le lier tooa unité d’organisation spécifique. Vous également pouvez lier le groupe de sécurité spécifique tooa des ordinateurs qui joint automatiquement auprès d’Azure AD. tooset cette stratégie pour tous les ordinateurs joints au domaine Windows 10 et Windows Server 2016 dans votre organisation, le domaine toohello objet lien hello stratégie de groupe.

### <a name="windows-installer-packages-for-non-windows-10-computers"></a>Packages Windows Installer pour les ordinateurs autres que Windows 10

ordinateurs de bas niveau Windows appartenant au domaine toojoin dans un environnement fédéré, vous pouvez télécharger et installer ces packages Windows Installer (.msi) à partir du centre de téléchargement à hello [Microsoft jonction d’espace pour les ordinateurs non Windows 10](https://www.microsoft.com/en-us/download/details.aspx?id=53554)page.

Vous pouvez déployer le package de hello à l’aide d’un système de distribution de logiciels tels que System Center Configuration Manager. Hello package prend en charge les options d’installation silencieuse standard hello avec hello *silencieux* paramètre. Branche actuelle de System Center Configuration Manager offre des avantages supplémentaires à partir de versions antérieures, telles que les enregistrements de hello capacité tootrack s’est terminée. Pour plus d’informations, consultez l’article [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).

programme d’installation Hello crée une tâche planifiée sur le système hello qui s’exécute dans le contexte de l’utilisateur hello. tâche Hello est déclenchée lorsque l’utilisateur de hello se connecte tooWindows. tâche Hello joint en mode silencieux appareil hello avec Azure AD avec des informations d’identification utilisateur de hello après avoir authentifié à l’aide de l’authentification Windows intégrée. toosee la tâche planifiée de hello, dans l’unité de hello, accédez trop**Microsoft** > **jonction**, puis passez la bibliothèque du Planificateur de tâches toohello.

## <a name="step-5-verify-joined-devices"></a>Étape 5 : Vérification des appareils joints

Vous pouvez vérifier les appareils joints au succès de votre organisation à l’aide de hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) applet de commande Bonjour [module Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).

sortie Hello de cette applet de commande affiche les périphériques qui sont enregistrés et joint à Azure AD. tooget tous les appareils, utilisez hello **-tous les** paramètre, puis filtre les à l’aide de hello **deviceTrustType** propriété. Les appareils joints à un domaine présentent la valeur **Joint au domaine**.

## <a name="next-steps"></a>Étapes suivantes

* [Gestion de toodevice introduction dans Azure Active Directory](device-management-introduction.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
