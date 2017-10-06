---
title: "rôles de contrôle d’accès basée sur les rôles personnalisés aaaCreate et affecter des utilisateurs externes dans Azure et des toointernal | Documents Microsoft"
description: "Attribuer des rôles RBAC personnalisés créés à l’aide de PowerShell et d’Azure CLI à des utilisateurs internes et externes"
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a>Contrôle d’accès en fonction du rôle Azure

Contrôle d’accès basé sur le rôle est une fonctionnalité uniquement du portail Azure autorisant les propriétaires de hello d’un abonnement tooassign granulaires rôles tooother auxquels les utilisateurs qui peuvent gérer les étendues de ressource spécifique dans leur environnement.

RBAC permet une meilleure gestion de la sécurité pour les grandes entreprises et pour les blocs SMB fonctionne avec des collaborateurs externes, des fournisseurs ou indépendants qui doivent accéder aux ressources toospecific dans votre environnement, mais pas nécessairement toohello ensemble de l’infrastructure ou l’une étendues associées à la facturation. RBAC souplesse hello de propriétaire d’un abonnement Azure géré par le compte d’administrateur hello (rôle d’administrateur de service à un niveau d’abonnement) et ont plusieurs toowork utilisateurs invités sous hello même abonnement, mais sans tout d’administration droits pour celle-ci. De gestion et de facturation, fonctionnalité RBAC de hello prouve toobe une option efficace temps et de gestion pour l’utilisation d’Azure dans divers scénarios.

## <a name="prerequisites"></a>Composants requis
L’utilisation de RBAC Bonjour environnement Azure requiert :

* Abonnement Azure ayant un autonome affecté toohello utilisateur comme propriétaire (rôle de l’abonnement)
* Rôle de propriétaire hello Hello abonnement Azure
* Avoir accès toohello [portail Azure](https://portal.azure.com)
* Vérifiez que hello toohave suivant des fournisseurs de ressources inscrit pour l’abonnement d’utilisateur hello : **Microsoft.Authorization**. Pour plus d’informations sur la façon dont tooregister hello des fournisseurs de ressources, consultez [fournisseurs du Gestionnaire de ressources, des régions, des versions d’API et des schémas](/azure-resource-manager/resource-manager-supported-services.md).

> [!NOTE]
> Les abonnements Office 365 ni aucune licence Azure Active Directory (par exemple : accès tooAzure Active Directory) configuré à partir du portail ne qualité l’utilisation de RBAC de hello O365.

## <a name="how-can-rbac-be-used"></a>Comment la fonctionnalité RBAC peut être utilisée
La fonctionnalité RBAC peut être appliquée à trois étendues différentes dans Azure. À partir de hello plus élevés étendue toohello plus basse, ils sont les suivantes :

* Abonnement (la plus élevée)
* Groupe de ressources
* Portée de la ressource (hello plus bas niveau d’accès offre des autorisations ciblées étendue de ressource Azure tooan)

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a>Attribuer des rôles au niveau de l’étendue de l’abonnement hello RBAC
Il existe notamment deux cas courants d’utilisation de la fonctionnalité RBAC :

* Utilisateurs externes d’organisations de hello (n’appartenant pas à client Azure Active Directory de l’utilisateur admin de hello) invité toomanage certaines ressources ou l’abonnement entier de hello
* Utilisation avec des utilisateurs à l’intérieur d’organisation hello (qu’ils appartiennent client Azure Active Directory de l’utilisateur hello) mais la partie de différentes équipes ou les groupes qui ont besoin d’un accès granulaire soit toohello abonnement entière ou les groupes de ressources toocertain ou ressource étendues Bonjour environnement

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a>Octroyer l’accès au niveau d’un abonnement à un utilisateur extérieur à Azure Active Directory
Rôles RBAC peuvent être accordées uniquement par **propriétaires** d’abonnement de hello par conséquent l’utilisateur admin hello doit être enregistré avec un nom d’utilisateur qui a ce rôle déjà affecté ou qui a créé l’abonnement Azure de hello.

À partir de hello portail Azure, après avoir connectez-vous en tant qu’administrateur, sélectionnez « Abonnements » et choisissez hello souhaitée une.
![panneau d’abonnement dans le portail Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) par défaut, si l’utilisateur admin hello a acheté hello abonnement Azure, utilisateur de hello apparaîtront en tant que **Admin. compte**, ce rôle d’abonnement hello. Pour plus d’informations sur les rôles d’abonnement Azure hello, consultez [ajouter ou modifier les rôles administrateur Azure qui gèrent les abonnement hello ou services](/billing/billing-add-change-azure-subscription-administrator.md).

Dans cet exemple, hello utilisateur »alflanigan@outlook.com» est hello **propriétaire** Hello « Version d’évaluation gratuite » abonnement Bonjour AAD locataire « Par défaut le locataire Azure ». Étant donné que cet utilisateur est le créateur de hello Hello abonnement Azure avec hello initiale Account Microsoft « Outlook » (Account Microsoft = Outlook, etc. de Live) hello nom de domaine par défaut pour tous les autres utilisateurs ajoutés dans ce locataire sera **«@alflaniganuoutlook.onmicrosoft.com»**. Par conception, syntaxe hello du nouveau domaine de hello est formé par assembler hello nom d’utilisateur et nom de domaine de l’utilisateur hello qui a créé le locataire de hello et l’extension de hello ajout **«. onmicrosoft.com »**.
En outre, les utilisateurs peuvent connectez-vous avec un nom de domaine personnalisé dans le locataire de hello après l’ajout et la vérification de sa locataire hello. Pour plus d’informations sur comment tooverify un nom de domaine personnalisé dans un locataire Azure Active Directory, voir [ajouter un répertoire de tooyour de nom de domaine personnalisé](/active-directory/active-directory-add-domain).

Dans cet exemple, l’annuaire hello » par défaut locataire Azure » contient uniquement les utilisateurs avec le nom de domaine hello «@alflanigan.onmicrosoft.com».

Après avoir sélectionné un abonnement de hello, l’utilisateur admin hello doit cliquer sur **contrôle d’accès (IAM)** , puis **ajouter un nouveau rôle**.





![fonctionnalité de contrôle d’accès IAM dans le portail Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![ajouter un utilisateur dans la fonctionnalité de contrôle d’accès IAM dans le portail Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

étape suivante de Hello est tooselect hello rôle toobe affecté et utilisateur hello auxquels le rôle RBAC hello sera assigné à. Bonjour **rôle** utilisateur admin de liste déroulante menu hello voit uniquement hello RBAC rôles intégrés qui sont disponibles dans Azure. Pour plus d’explications sur chaque rôle et les étendues qui peuvent lui être attribuées, voir [Rôles intégrés pour contrôle d’accès en fonction du rôle Azure](/active-directory/role-based-access-built-in-roles.md).

l’utilisateur admin Hello doit ensuite l’adresse de messagerie tooadd hello d’utilisateur externe de hello. Hello attendu de comportement pour hello utilisateur externe toonot qui s’affichent dans hello existant du client. Une fois que l’utilisateur externe de hello a été invité, il sera visible sous **abonnements > contrôle d’accès (IAM)** avec tous les utilisateurs actuels hello, qui sont actuellement attribués un rôle RBAC au hello étendue de l’abonnement.





![ajouter le rôle RBAC toonew autorisations](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![liste des rôles RBAC au niveau abonnement](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

utilisateur de Hello »chessercarlton@gmail.com» a été invitée toobe un **propriétaire** pour hello abonnement « D’essai gratuit ». Après l’envoi d’invitation hello, utilisateur externe de hello recevra un e-mail de confirmation avec un lien d’activation.
![e-mail d'invitation pour le rôles RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)

En cours toohello externe organisation, utilisateur hello n’a pas les tous les attributs existants dans le répertoire de « Par défaut le locataire Azure » hello. Ils sont créés après toobe consentement enregistré dans le répertoire hello qui est associé à abonnement hello qui lui ont été affectées à un rôle à utilisateur externe de hello.





![e-mail d’invitation pour le rôle RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

les utilisateurs externes Hello montre Bonjour client Azure Active Directory dès lors que l’utilisateur externe et cela peut être affiché dans hello portail Azure et dans le portail classique de hello.





![panneau des utilisateurs azure active directory sur le portail azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![panneau des utilisateurs azure active directory sur le portail azure classic](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

Bonjour **utilisateurs** vue dans les deux utilisateurs externes de portails hello peut être reconnu par :

* type d’icône différents Hello Bonjour portail Azure
* Hello différent approvisionnement point dans le portail classique de hello

Toutefois, l’octroi **propriétaire** ou **collaborateur** utilisateur externe de l’accès tooan à hello **abonnement** portée, n’autorise pas de répertoire de l’utilisateur admin hello accès toohello, à moins que hello **administrateur Global** l’autorise. Dans les propriétés d’utilisateur hello, hello **Type utilisateur** qui a deux paramètres communs, **membre** et **invité** peut être identifiée. Un membre est un utilisateur qui est enregistré dans le répertoire de hello lors de l’invité est un répertoire de toohello utilisateur invité d’une source externe. Pour plus d’informations, voir [Comment les administrateurs Azure Active Directory ajoutent des utilisateurs B2B Collaboration](/active-directory/active-directory-b2b-admin-add-users).

> [!NOTE]
> Assurez-vous qu’après avoir entré les informations d’identification hello dans le portail de hello, utilisateur externe de hello sélectionne le répertoire approprié de hello toosign dans. Hello même utilisateur peut avoir accès toomultiple répertoires et peuvent sélectionner le des deux d'entre eux en cliquant sur le nom d’utilisateur de hello dans hello partie supérieure droite Bonjour portail Azure, puis choisissez répertoire approprié de hello à partir de la liste déroulante de hello.

Tout en étant un invité dans le répertoire de hello, utilisateur externe de hello peut gérer toutes les ressources pour hello abonnement Azure, mais ne peut pas accéder au répertoire de hello.





![accéder au portail Azure active directory de tooazure restreint](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

Azure Active Directory et un abonnement Azure n’ont pas de relation enfant-parent comme l’ont d’autres ressources Azure (par exemple, Azure Virtual Machines, Azure Virtual Networks, Web Apps, Stockage Azure, etc.). Tous les hello ce dernier est créé, gérés et facturés sous un abonnement Azure, alors qu’un abonnement Azure est utilisé toomanage hello accès tooan Azure active. Pour plus d’informations, consultez [abonnement de la manière dont un Azure est connexe tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).

À partir de tous les hello RBAC rôles intégrés **propriétaire** et **collaborateur** offrent un accès de gestion complète des ressources de tooall dans l’environnement de hello, hello différence qu’un collaborateur ne peut créer et supprimer les nouveaux Rôles RBAC. Hello autres rôles intégrés tels que **contributeur de l’ordinateur virtuel** offrent un accès de gestion complète uniquement les ressources toohello indiqués par le nom hello, quel que soit hello **groupe de ressources** qu’ils sont en cours de création dans.

Rôle affectation RBAC d’intégré hello de **contributeur de l’ordinateur virtuel** à un niveau d’abonnement, signifie que ce rôle de hello hello utilisateur affecté :

* Peut afficher tous les ordinateurs virtuels quelle que soit leurs déploiement date hello groupes de ressources et qu’ils font partie de
* A des machines virtuelles de gestion complète accès toohello dans l’abonnement de hello
* Ne peut pas afficher d’autres types de ressource dans l’abonnement de hello
* ne peut apporter aucune modification sur le plan de la facturation.

> [!NOTE]
> RBAC en cours d’une seule fonctionnalité portail Azure, elle n’accorde pas portail classique d’accès toohello.

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a>Affecter un intégrée RBAC rôle tooan utilisateur externe
Pour un scénario différent dans ce test, hello utilisateur externe «alflanigan@gmail.com» est ajouté en tant qu’un **contributeur de l’ordinateur virtuel**.




![rôle prédéfini de contributeur de machines virtuelles](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

comportement normal de Hello pour cet utilisateur externe avec ce rôle intégré est toosee et gérer uniquement les ordinateurs virtuels et leur adjacents Gestionnaire de ressources uniquement ressources nécessaire lors du déploiement. Par défaut, ces rôles limités offrent un accès seules ressources correspondant tootheir créés Bonjour portail Azure, quel que soit certaines peuvent toujours être déployé dans le portail classique hello et (par exemple : machines virtuelles).





![présentation du rôle contributeur de machines virtuelles dans le portail azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a>Octroi d’accès à un niveau d’abonnement pour un utilisateur dans hello même répertoire
flux de processus Hello est identique tooadding un utilisateur externe, à la fois de hello rôle admin de perspective qui accord hello RBAC, ainsi que des utilisateur hello accordées rôle toohello d’accès. Hello différence est que l’utilisateur invité de hello ne recevra pas les invitations de messagerie car toutes les portées de ressource hello au sein de l’abonnement de hello sera disponibles dans le tableau de bord hello après l’ouverture de session.

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a>Attribuer des rôles au niveau de l’étendue de groupe de ressources hello RBAC
Affectation d’un rôle RBAC à un **groupe de ressources** étendue a un processus identiques pour l’attribution de rôle hello au niveau d’abonnement hello, pour les deux types d’utilisateurs - internes ou externes (dans le cadre du hello même répertoire). Bonjour les utilisateurs qui sont affectés des rôles RBAC de hello est toosee dans leur environnement uniquement le groupe de ressources hello leur a été attribué l’accès à partir de hello **groupes de ressources** icône Bonjour portail Azure.

## <a name="assign-rbac-roles-at-hello-resource-scope"></a>Affecter des rôles RBAC à portée de la ressource hello
Affectation d’un rôle RBAC dans une étendue de ressources dans Azure dispose d’un processus identiques pour l’attribution de rôle hello au niveau d’abonnement hello ou au niveau de groupe de ressources hello, suivant hello même flux de travail pour les deux scénarios. Là encore, les utilisateurs hello qui sont affectés à hello RBAC rôle peuvent voir uniquement les éléments de hello qu’ils ont reçu accès, soit hello en **toutes les ressources** onglet ou directement dans leur tableau de bord.

Un aspect important de RBAC à la fois à l’étendue de groupe de ressources ou de la portée de la ressource est pour le répertoire approprié de hello utilisateurs toomake que dans le toosign toohello.





![connexion à un annuaire dans le portail azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a>Attribuer des rôles RBAC pour un groupe Azure Active Directory
Tous les scénarios de hello à l’aide de RBAC dans hello trois différentes portées d’Azure offre des privilèges de hello de gérer, déployer et administrer les différentes ressources en tant qu’un utilisateur affecté sans hello ont besoin de gérer un abonnement personnel. Rôle RBAC hello quel que soit attribué pour un abonnement, le groupe de ressources ou la portée de la ressource, toutes les ressources hello créées davantage par les utilisateurs de hello affecté sont facturées sous hello un abonnement Azure où les utilisateurs de hello ont accès à. De cette manière, hello les utilisateurs disposant d’autorisations d’administrateur pour que tout abonnement Azure de facturation a une vue d’ensemble complète sur la consommation hello, quel que soit le qui gère les ressources hello.

Pour les grandes entreprises, les rôles RBAC peuvent être appliquées dans hello identique pour les groupes Azure Active Directory tenant compte du point de vue hello utilisateur admin hello veut toogrant hello granulaire de l’accès pour les équipes ou les départements entiers, non pas individuellement pour chaque utilisateur, par conséquent, sa prise en compte en tant qu’extrêmement heure et la gestion efficace option. tooillustrate cet exemple, le hello **collaborateur** rôle a été ajouté à tooone des groupes de hello dans client hello au niveau d’abonnement hello.





![ajouter un rôle RBAC pour les groupes AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

Ces groupes sont des groupes de sécurité qui sont approvisionnés et gérés uniquement dans Azure Active Directory.

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a>Créer un support de tooopen rôle RBAC personnalisé demandes à l’aide de PowerShell
rôles RBAC intégrés Hello, qui sont disponibles dans Azure Vérifiez certains niveaux d’autorisation basée sur les ressources disponibles hello dans l’environnement de hello. Toutefois, si aucun de ces rôles de besoins de l’utilisateur admin de hello, a hello option toolimit accès davantage en créant des rôles RBAC personnalisés.

Création des rôles personnalisés RBAC nécessite tootake un rôle d’intégrés, modifier et puis l’importer dans un environnement de hello. transfert de Hello et téléchargement du rôle de hello sont gérés à l’aide de PowerShell ou CLI.

Il est important toounderstand hello conditions préalables de la création d’un rôle personnalisé qui peuvent accorder un accès granulaire au niveau d’abonnement hello et également autoriser hello invité utilisateur hello flexibilité de l’ouverture de demandes de support.

Pour ce rôle intégré d’exemple hello **lecteur** qui permet aux utilisateurs accès tooview toutes les ressources hello étendues mais pas tooedit les ou créer de nouveaux a été personnalisé tooallow hello utilisateur hello le choix de prise en charge des demandes d’ouverture.

Hello première action d’exportation hello **lecteur** toobe de besoins de rôle s’est terminée dans PowerShell a exécuté avec des autorisations élevées en tant qu’administrateur.

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Capture d’écran de PowerShell pour le rôle RBAC Lecteur](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

Vous devez tooextract modèle JSON hello du rôle de hello.





![Modèle JSON pour le rôle RBAC Lecteur personnalisé](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

Un rôle RBAC classique comprend trois sections principales, **Actions**, **NotActions** et **AssignableScopes**.

Bonjour **Action** section figurent tous hello opérations autorisées pour ce rôle. Il est important toounderstand que chaque action est attribuée à partir d’un fournisseur de ressources. Dans ce cas, pour la création de prise en charge des tickets hello **Microsoft.Support** fournisseur de ressources doit être répertorié.

toosee en mesure de toobe tous hello des fournisseurs de ressources disponibles et enregistrés dans votre abonnement, vous pouvez utiliser PowerShell.
```
Get-AzureRMResourceProvider

```
En outre, vous pouvez vérifier hello les hello disponible PowerShell applets de commande toomanage hello fournisseurs de ressources.
    ![Capture d’écran de PowerShell pour la gestion de fournisseur de ressources](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)

toorestrict tous hello actions pour un rôle RBAC particulier, les ressources fournisseurs sont répertoriés sous la section de hello **NotActions**.
Il est obligatoire de que ce rôle RBAC hello contient l’ID où il est utilisé d’un abonnement explicite hello. ID d’abonnement Hello sont répertoriés sous hello **AssignableScopes**, sinon vous ne serez pas autorisé rôle de hello tooimport dans votre abonnement.

Après la création et personnalisation du rôle RBAC hello, il a besoin d’un environnement de hello arrière importés de toobe.

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

Dans cet exemple, un nom personnalisé pour ce rôle RBAC hello est « lecteur prise en charge des tickets niveau d’accès « autorisant hello utilisateur tooview tous les éléments dans l’abonnement de hello et également les demandes de support tooopen.

> [!NOTE]
> Hello uniquement deux rôles RBAC intégrés, autorisant ainsi une action hello d’ouverture de demandes de support sont **propriétaire** et **collaborateur**. Pour un utilisateur toobe tooopen en mesure de prise en charge les requêtes, il doit être affecté un rôle RBAC uniquement à l’étendue de l’abonnement hello, étant donné que toutes les demandes de prise en charge sont créées d’après un abonnement Azure.

Ce nouveau rôle personnalisé a été affecté tooan utilisateur hello même répertoire.





![capture d’écran du rôle RBAC personnalisé importé Bonjour portail Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![capture d’écran d’attribution personnalisée importé toouser de rôle RBAC Bonjour même répertoire](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![capture d’écran d’autorisations pour un rôle RBAC importé personnalisé](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

exemple de Hello a été plus limites de hello tooemphasize détaillées de ce rôle RBAC personnalisé comme suit :
* Peut créer des demandes de support
* Ne peut pas créer d’étendues de ressource (par exemple, machine virtuelle)
* Ne peut pas créer de groupes de ressources





![capture d’écran d’un rôle RBAC personnalisé créant des demandes de support](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![capture d’écran du rôle RBAC personnalisé n’a pas pu toocreate machines virtuelles](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![capture d’écran du rôle RBAC personnalisé n’a pas pu toocreate RGs nouveau](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a>Créer un support de tooopen rôle RBAC personnalisé demandes à l’aide de CLI d’Azure
En cours d’exécution sur un Mac et sans avoir accès tooPowerShell, CLI d’Azure est toogo de façon hello.

Hello étapes toocreate un rôle personnalisé sont hello identiques, avec hello seule exception que vous utilisez interface CLI rôle de hello ne peut être téléchargé dans un modèle JSON, mais il peuvent être affiché dans hello CLI.

Pour cet exemple, j’ai choisi rôle intégré de hello de **lecteur de sauvegarde**.

```

azure role show "backup reader" --json

```





![Capture d’écran d’interface de ligne de commande pour l’affichage du rôle Lecteur de secours (Backup Reader)](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

Modifiez le rôle hello dans Visual Studio après avoir copié les propriétés hello dans un modèle JSON, hello **Microsoft.Support** fournisseur de ressources a été ajouté dans hello **Actions** sections afin que cet utilisateur peut ouvrir. demandes de support tout en continuant toobe un lecteur de coffres de sauvegarde hello. Là encore il est ID d’abonnement nécessaire tooadd hello où ce rôle sera utilisé dans hello **AssignableScopes** section.

```

azure role create --inputfile <path>

```





![Capture d’écran de l’Interface de ligne de commande pour l’importation de rôle RBAC personnalisé](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

nouveau rôle de Hello est désormais disponible dans hello portail Azure et le processus d’attribution hello est hello même que dans les exemples précédents hello.





![Capture d’écran du portail Azure montrant le rôle RBAC personnalisé créé à l’aide d’Azure CLI 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

À compter de hello dernière Build 2017, hello Azure Cloud Shell est généralement disponible. Azure Cloud Shell est un complément tooIDE et hello portail Azure. Avec ce service, vous bénéficiez d’un interpréteur de commandes basé sur un navigateur, qui est authentifié et hébergé dans Azure, et que vous pouvez utiliser à la place de l’interface de ligne de commande installée sur votre ordinateur.





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
