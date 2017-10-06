---
title: aaaAzure IoT Suite et Azure Active Directory | Documents Microsoft
description: "Décrit comment Azure IoT Suite utilise les autorisations de toomanage d’Azure Active Directory."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: dobett
ms.openlocfilehash: 4768630f2de4bb431731fbd4e8929232bc80b9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-on-hello-azureiotsuitecom-site"></a>Autorisations sur le site de azureiotsuite.com hello

## <a name="what-happens-when-you-sign-in"></a>Que se passe-t-il lorsque vous vous connectez ?

Hello la première fois que vous vous connectez à [azureiotsuite.com][lnk-azureiotsuite], site de hello détermine les niveaux d’autorisation hello s’appuie sur hello actuellement sélectionné de client Azure Active Directory (AAD) et Azure abonnement.

1. Tout d’abord, la liste hello toopopulate du nom d’utilisateur de tooyour suivant locataires vu, hello site trouve à partir d’Azure les locataires AAD auxquels vous appartenez. Actuellement, site de hello peut uniquement obtenir des jetons d’utilisateur pour un locataire à la fois. Par conséquent, lorsque vous basculez des locataires à l’aide de la liste déroulante de hello dans le coin supérieur droit de hello, site de hello vous connecte les jetons de hello tooobtain toothat client pour ce client.

2. Ensuite, site de hello recherche à partir d’Azure, les abonnements que vous avez associé hello sélectionné locataire. Vous consultez les abonnements disponibles hello lorsque vous créez une nouvelle solution préconfigurée.

3. Enfin, site de hello récupère toutes les ressources de hello dans les abonnements hello et groupes de ressources en tant que solutions préconfigurées et remplit les vignettes hello sur la page d’accueil hello.

Hello les sections suivantes décrire les rôles hello qui contrôlent les solutions d’accès toohello préconfiguré.

## <a name="aad-roles"></a>Rôles AAD

rôles AAD Hello hello capacité disposition préconfigurée solutions de contrôle et gérer des utilisateurs dans une solution préconfigurée.

Pour plus d’informations sur les rôles d’administrateur dans ADD, consultez la page [Attribution de rôles d’administrateur dans Azure AD][lnk-aad-admin]. article en cours de Hello se concentre sur hello **administrateur Global** et hello **utilisateur** rôles d’annuaire que celui utilisé par hello préconfiguré solutions.

### <a name="global-administrator"></a>Administrateur général

Il peut y avoir de nombreux administrateurs généraux pour chaque locataire AAD :

* Lorsque vous créez un client AAD, vous êtes administrateur global de hello par défaut de ce client.
* administrateur général de Hello peut configurer une solution préconfigurée et est affectée une **Admin** rôle pour l’application hello dans leur locataire AAD.
* Si un autre utilisateur de hello même locataire AAD crée une application, hello rôle par défaut accordées administrateur global de toohello est **ReadOnly**.
* Un administrateur global peut affecter tooroles d’utilisateurs pour les applications utilisant hello [portail Azure][lnk-portal].

### <a name="domain-user"></a>Utilisateur de domaine

Il peut y avoir de nombreux utilisateurs de domaine pour chaque locataire AAD :

* Un utilisateur de domaine peut configurer une solution préconfigurée via hello [azureiotsuite.com] [ lnk-azureiotsuite] site. Par défaut, utilisateur de domaine hello est accordée hello **Admin** rôle Bonjour approvisionné l’application.
* Un utilisateur de domaine peut créer une application à l’aide du script build.cmd de hello Bonjour [azure-iot-de surveillance à distance][lnk-rm-github-repo], [azure-iot--maintenance prédictive] [ lnk-pm-github-repo], ou [azure iot-connecté-usine] [ lnk-cf-github-repo] référentiel. Toutefois, rôle par défaut de hello accordée est de l’utilisateur de domaine toohello **ReadOnly**, car un utilisateur de domaine n’a pas de rôles tooassign d’autorisation.
* Si un autre utilisateur de client d’AAD hello crée une application, utilisateur de domaine hello est attribué hello **ReadOnly** rôle par défaut pour cette application.
* Un utilisateur de domaine ne peut pas attribuer des rôles pour des applications ; par conséquent, il ne peut pas ajouter des utilisateurs ou des rôles pour les utilisateurs d’une application, même s’ils l’ont approvisionnée.

### <a name="guest-user"></a>Utilisateur invité

Il peut y avoir de nombreux utilisateurs invités pour chaque locataire AAD. Les utilisateurs invités ont un ensemble limité de droits dans le client d’AAD hello. Par conséquent, les utilisateurs invités ne peut pas prévoir une solution préconfigurée dans le client d’AAD hello.

Pour plus d’informations sur les utilisateurs et les rôles dans AAD, consultez hello suivant des ressources :

* [Créer des utilisateurs dans Azure AD][lnk-create-edit-users]
* [Affecter des utilisateurs tooapps][lnk-assign-app-roles]

## <a name="azure-subscription-administrator-roles"></a>Rôles de l’administrateur d’abonnement Azure

rôles d’administrateur Azure Hello contrôlent hello capacité toomap un client de tooan AD abonnement Azure.

En savoir plus sur les rôles d’administrateur Azure hello dans l’article de hello [comment tooadd ou modifier le compte d’administrateur, administrateur de Service et Coadministrateur Azure][lnk-admin-roles].

## <a name="application-roles"></a>Rôles d’application

rôles d’application Hello contrôlent toodevices d’accès dans votre solution préconfigurée.

Une application approvisionnée comporte deux rôles définis et un rôle implicite défini :

* **Administrateur :** a tooadd de contrôle total, gérer, supprimer des appareils et modifier les paramètres.
* **Lecture seule :** peut afficher les appareils, actions, règles, travaux et télémétrie.

Vous pouvez trouver les autorisations hello rôle tooeach Bonjour [RolePermissions.cs] [ lnk-resource-cs] fichier source.

### <a name="changing-application-roles-for-a-user"></a>Modification des rôles d’application pour un utilisateur

Vous pouvez utiliser hello suivant la procédure toomake un utilisateur dans votre annuaire Active Directory, un administrateur de votre solution préconfigurée.

Vous devez être un rôle de toochange AAD administrateur global pour un utilisateur :

1. Accédez toohello [portail Azure][lnk-portal].
2. Sélectionnez **Azure Active Directory**.
3. Assurez-vous que vous utilisez répertoire hello choisi sur azureiotsuite.com lors de la configuration de votre solution. Si vous avez plusieurs annuaires associés à votre abonnement, vous pouvez basculer entre les si vous cliquez sur le nom de votre compte en haut à droite de hello du portail de hello.
4. Cliquez sur **Applications d’entreprise**, puis sur **Toutes les applications**.
4. Affichez **toutes les applications** avec **n’importe quel** état. Recherchez ensuite une application avec le nom de votre solution préconfigurée.
5. Cliquez sur nom hello application hello qui correspond au nom de votre solution préconfigurée.
6. Cliquez sur **Utilisateurs et groupes**.
7. Sélectionnez utilisateur hello tooswitch rôles.
8. Cliquez sur **affecter** et sélectionnez hello rôle (tel que **Admin**) vous aimeriez tooassign toohello utilisateur, cliquez sur la case à cocher hello.

## <a name="faq"></a>Forum Aux Questions

### <a name="im-a-service-administrator-and-id-like-toochange-hello-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a>Je suis un administrateur de service et j’aimerais mappage de répertoire hello toochange entre mon abonnement et un locataire AAD spécifique. Comment mener à bien cette tâche ?

1. Accédez toohello [portail Azure classic][lnk-classic-portal], cliquez sur **paramètres** dans la liste hello des services sur le côté gauche de hello.
2. Sélectionnez l’abonnement hello vous souhaitez que le mappage de répertoire hello toochange à.
3. Cliquez sur **Modifier l’annuaire**.
4. Sélectionnez hello **active** toouse dans la liste déroulante de hello voulue. Cliquez sur flèche ascendante de hello.
5. Confirmer le mappage de répertoire hello et affectées aux coadministrateurs. Si vous migrez à partir d’un autre répertoire, tous les coadministrateurs hello hello répertoire d’origine sont supprimés.

### <a name="im-a-domain-usermember-on-hello-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a>Je suis un utilisateur/membre de domaine sur le client d’AAD hello et j’ai créé une solution préconfigurée. Comment puis-je me voir attribuer un rôle pour mon application ?

Demandez à un administrateur global de toomake vous un administrateur global sur hello AAD locataire et rôles toousers vous affectez. Vous pouvez également demander à un administrateur global de tooassign vous directement un rôle. Si vous souhaitez que le client d’AAD hello toochange sur que votre solution préconfigurée a été déployée, consultez la question suivante de hello.

### <a name="how-do-i-switch-hello-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a>Comment basculer client AAD de hello à que ma solution préconfigurée de contrôle à distance et l’application sont affectés ?

Vous pouvez exécuter un déploiement cloud à partir de <https://github.com/Azure/azure-iot-remote-monitoring>, puis redéployer avec un client AAD nouvellement créé. Car vous n’êtes, par défaut, un administrateur global lorsque vous créez un locataire AAD, vous disposez des autorisations tooadd utilisateurs et attribuer des rôles aux utilisateurs de toothose.

1. Créer un annuaire AAD dans hello [portail Azure][lnk-portal].
2. Accédez trop<https://github.com/Azure/azure-iot-remote-monitoring>.
3. Exécutez `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (par exemple, `build.cmd cloud debug myRMSolution`)
4. Lorsque vous y êtes invité, définissez hello **tenantid** toobe votre client qui vient d’être créée au lieu de votre client précédent.

### <a name="i-want-toochange-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a>Je veux toochange un administrateur de Service ou un Coadministrateur lorsque connecté avec un compte organisationnel

Consultez l’article du support technique hello [modifier un administrateur de Service et le Coadministrateur lorsque connecté avec un compte organisationnel][lnk-service-admins].

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-hello-proper-permissions-toocreate-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a>Pourquoi est-ce que je reçois cette erreur ? « Votre compte n’a pas hello des autorisations appropriées toocreate une solution. Veuillez contacter votre administrateur de compte ou essayer avec un autre compte. »

Examinez hello suivant le schéma pour obtenir des instructions :

![][img-flowchart]

> [!NOTE]
> Si vous continuez d’erreur de hello toosee après la validation, vous êtes un administrateur général sur le client d’AAD hello et un coadministrateur de l’abonnement de hello, demandez à votre administrateur de compte supprimer hello utilisateur et réaffecter les autorisations nécessaires dans cet ordre. Tout d’abord, ajouter un utilisateur de hello en tant qu’un administrateur global et puis ajoutez les utilisateurs en tant que coadministrateur sur hello abonnement Azure. Si les problèmes persistent, contactez le service [Aide et support][lnk-help-support].

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-toocreate-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a>Pourquoi affiche-t-il cette erreur alors que j’ai un abonnement Azure ? « Un abonnement Azure est requis toocreate préconfiguré solutions. Vous pouvez créer un compte d'essai gratuit en quelques minutes seulement. »

Si vous êtes certain de que disposer d’un abonnement Azure, valider un mappage pour votre abonnement de locataire hello et locataire approprié de hello est sélectionnée dans la liste déroulante de hello. Si vous avez validé hello souhaité locataire est correct, suivez hello précédant le diagramme et de valider le mappage hello de votre abonnement et ce locataire AAD.

## <a name="next-steps"></a>Étapes suivantes
toocontinue en savoir plus sur IoT Suite, consultez Comment vous pouvez [personnaliser une solution préconfigurée][lnk-customize].

[img-flowchart]: media/iot-suite-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-classic-portal]: https://manage.windowsazure.com/
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]: ../active-directory/active-directory-coreapps-assign-user-azure-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
