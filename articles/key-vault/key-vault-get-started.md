---
title: "aaaGet main d’Azure Key Vault | Documents Microsoft"
description: "Utilisez ce didacticiel toohelp que vous obtenez en main d’Azure Key Vault toocreate un conteneur renforcé dans Azure, toostore et gérer les clés de chiffrement et les clés secrètes dans Azure."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 36721e1d-38b8-4a15-ba6f-14ed5be4de79
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 865853b778dec5fca5c7db0d060627554c0a9cb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-key-vault"></a>Prise en main du coffre de clés Azure
Azure Key Vault est disponible dans la plupart des régions. Pour plus d’informations, consultez hello [page de tarification de coffre de clés](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introduction
Utilisez ce didacticiel toohelp que vous obtenez en main d’Azure Key Vault toocreate un conteneur renforcé (un coffre) dans Azure, toostore et gérer les clés de chiffrement et les clés secrètes dans Azure. Il vous guide tout au long des processus de hello d’à l’aide d’Azure PowerShell toocreate un coffre qui contient une clé ou un mot de passe que vous pouvez ensuite utiliser avec une application Windows Azure. Il vous montre également comment une application peut utiliser cette clé ou ce mot de passe.

**Estimation du temps toocomplete :** 20 minutes

> [!NOTE]
> Ce didacticiel n’inclut pas les instructions relatives à la toowrite hello application Azure qui a une des étapes de hello inclut, à savoir comment tooauthorize un toouse application une clé ou au secret dans la clé de hello coffre.
>
> Ce didacticiel utilise Azure PowerShell. Pour connaître la marche à suivre avec l’interface de ligne de commande interplateforme, consultez [ce didacticiel équivalent](key-vault-manage-with-cli2.md).
>
>

Pour plus d’informations générales sur Azure Key Vault, consultez la page [Présentation d’Azure Key Vault](key-vault-whatis.md)

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez avoir hello suivant :

* Un abonnement tooMicrosoft Azure. Si vous n’en possédez pas, vous pouvez vous inscrire pour créer dès aujourd’hui un [compte gratuit](https://azure.microsoft.com/pricing/free-trial/).
* Azure PowerShell, **version 1.1.0 minimale**. tooinstall Azure PowerShell et associez-le à votre abonnement Azure, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview). Si vous avez déjà installé Azure PowerShell et que vous ne connaissez pas la version de hello, à partir de la console de hello Azure PowerShell, tapez `(Get-Module azure -ListAvailable).Version`. Si vous utilisez Azure PowerShell version 0.9.1 à 0.9.8, vous pouvez toujours utiliser ce didacticiel en y apportant quelques changements mineurs. Par exemple, vous devez utiliser hello `Switch-AzureMode AzureResourceManager` commande et des commandes de coffre de clés Azure hello ont été modifiés. Pour obtenir la liste de hello applets de commande de coffre de clés pour les versions 0.9.1 via 0.9.8, consultez [applets de commande Azure Key Vault](/powershell/module/azurerm.keyvault/#key_vault).
* Une application qui sera la clé de hello toouse configuré ou le mot de passe que vous créez dans ce didacticiel. Un exemple d’application est disponible à partir de hello [Microsoft Download Center](http://www.microsoft.com/en-us/download/details.aspx?id=45343). Pour obtenir des instructions, consultez hello qui accompagne le fichier Lisez-moi.

Ce didacticiel est conçu pour les débutants d’Azure PowerShell, mais il suppose que vous comprenez les concepts de base hello, tels que des modules, applets de commande et des sessions. Pour plus d’informations, consultez la section [Prise en main de Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx).

aide pour une applet de commande que vous voyez dans ce didacticiel, utilisez hello de détaillée tooget **Get-Help** applet de commande.

    Get-Help <cmdlet-name> -Detailed

Par exemple, tooget aide hello **AzureRmAccount de connexion** applet, tapez :

    Get-Help Login-AzureRmAccount -Detailed

Vous pouvez également lire hello suivant tooget didacticiels familiarisé avec Azure Resource Manager dans Azure PowerShell :

* [Comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview)
* [Utilisation d’Azure PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md)

## <a id="connect"></a>Se connecter tooyour abonnements
Démarrer une session Azure PowerShell et connectez-vous à tooyour compte Azure avec hello de commande suivante :  

    Login-AzureRmAccount

Notez que si vous utilisez une instance spécifique de Azure, par exemple, le secteur public Azure, utilisez hello - paramètre d’environnement avec cette commande. Par exemple : `Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`

Dans la fenêtre contextuelle du navigateur de hello, entrez votre nom d’utilisateur de compte Azure et un mot de passe. Azure PowerShell Obtient tous les abonnements hello qui sont associés à ce compte et par défaut, utilise hello premier.

Si vous avez plusieurs abonnements et que vous souhaitez toospecify un un toouse spécifique pour Azure Key Vault, tapez Bonjour suivant toosee les abonnements de hello pour votre compte :

    Get-AzureRmSubscription

Ensuite, toospecify hello abonnement toouse, type :

    Set-AzureRmContext -SubscriptionId <subscription ID>

Pour plus d’informations sur la configuration d’Azure PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

## <a id="resource"></a>Création d’un groupe de ressources
Lorsque vous utilisez Azure Resource Manager, toutes les ressources associées sont créées au sein d’un groupe de ressources. Nous allons créer un groupe de ressources nommé **ContosoResourceGroup** pour ce didacticiel :

    New-AzureRmResourceGroup –Name 'ContosoResourceGroup' –Location 'East Asia'


## <a id="vault"></a>Création d’un coffre de clés
Hello d’utilisation [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) toocreate de l’applet de commande un coffre de clés. Cette applet de commande a trois paramètres obligatoires : un **nom de groupe de ressources**, un **coffre de clés**et hello **emplacement géographique**.

Par exemple, si vous utilisez le nom de coffre de hello **ContosoKeyVault**, nom de groupe de ressources hello de **ContosoResourceGroup**et l’emplacement de hello de **Asie orientale**, type :

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

sortie Hello de cette applet de commande affiche les propriétés du coffre de clés hello que vous venez de créer. propriétés les plus importantes Hello deux sont :

* **Nom de coffre**: dans l’exemple de hello, il s’agit **ContosoKeyVault**. Vous allez utiliser ce nom pour les autres applets de commande Key Vault.
* **URI de coffre**: dans l’exemple de hello, il s’agit https://contosokeyvault.vault.azure.net/. Les applications qui utilisent votre coffre via son API REST doivent utiliser cet URI.

Votre compte Azure est désormais toutes les opérations sur cette clé de coffre tooperform autorisé. coffre de clés.

> [!NOTE]
> Si vous voyez l’erreur de hello **abonnement de hello n’est pas inscrit toouse, espace de noms 'Microsoft.KeyVault'** lorsque vous essayez toocreate votre nouveau coffre de clés, exécutez `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"` , puis réexécutez la commande New-AzureRmKeyVault. Pour plus d’informations, consultez [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider).
>
>

## <a id="add"></a>Ajouter une clé ou un coffre de clés secrètes toohello
Si vous souhaitez que le coffre de clés Azure toocreate une clé protégée par logiciel pour vous, utilisez hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) applet de commande et tapez Bonjour qui suit :

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -Destination 'Software'

Toutefois, si vous avez une clé protégée par logiciel un. PFX fichier enregistré tooyour C:\ lecteur dans un fichier nommé softkey.pfx que vous souhaitez tooupload tooAzure le coffre de clés, hello du type suivant tooset hello variable **securepfxpwd** un mot de passe de **123** pour hello. Fichier PFX :

    $securepfxpwd = ConvertTo-SecureString –String '123' –AsPlainText –Force

Puis tapez Bonjour suivant clé de hello tooimport hello. Fichier PFX, qui protège la clé de hello par logiciel dans hello service Key Vault :

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd


Vous pouvez maintenant référencer cette clé que vous avez créé ou téléchargé tooAzure le coffre de clés, à l’aide de son URI. Utilisez **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways obtenir la version actuelle de hello et utiliser **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget cette version spécifique.  

toodisplay hello URI pour cette clé, de type :

    $Key.key.kid

tooadd un coffre toohello secrète, qui est un mot de passe nommé SQLPassword et a la valeur hello Pa$ $w0rd tooAzure le coffre de clés, convertissez d’abord les valeur hello de chaîne sécurisée de Pa$ $w0rd tooa en tapant hello suivante :

    $secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force

Ensuite, tapez ce qui suit hello :

    $secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword' -SecretValue $secretvalue

Vous pouvez maintenant référencer ce mot de passe que vous avez ajouté tooAzure le coffre de clés, à l’aide de son URI. Utilisez **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways obtenir la version actuelle de hello et utiliser **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget cette version spécifique.

toodisplay hello URI pour ce secret, type :

    $secret.Id

Examinons la clé de hello ou le secret que vous venez de créer :

* tooview votre type de clé, :`Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`
* tooview votre secret principal, type :`Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`

Votre coffre de clés et la clé ou le secret est maintenant prête pour les applications toouse. Vous devez autoriser les applications toouse les.  

## <a id="register"></a>Inscription d’une application auprès d’Azure Active Directory
Cette étape est généralement effectuée par un développeur et sur un ordinateur distinct. Il n’est pas spécifique tooAzure le coffre de clés, mais il est inclus ici par souci d’exhaustivité.

> [!IMPORTANT]
> didacticiel de hello toocomplete, votre compte, le coffre de hello et l’application hello que vous inscrivez dans cette étape doivent toutes être Bonjour même annuaire Azure.
>
>

Les applications qui utilisent un coffre de clés doivent s’authentifier à l’aide d’un jeton à partir d’Azure Active Directory. toodo, hello propriétaire de l’application hello doit inscrire tout d’abord des application hello dans leur annuaire Active Directory de Azure. À fin hello d’enregistrement, le propriétaire de l’application hello obtient hello valeurs suivantes :

* Un **ID d’Application** (également appelé ID de Client) et **clé d’authentification** (également appelé un secret partagé hello). application Hello doit présenter à la fois ces valeurs tooAzure Active Directory, tooget un jeton. Comment application hello est configuré toodo que cela dépend application hello. Pour un exemple d’application le coffre de clés de hello, le propriétaire de l’application hello définit ces valeurs dans le fichier app.config hello.

application hello tooregister dans Azure Active Directory :

1. Se connecter toohello portail Azure classic.
2. Sur hello gauche, cliquez sur **Active Directory**, puis sélectionnez le répertoire hello dans lequel vous allez inscrire votre application. <br> <br> **Remarque :** vous devez sélectionner hello même répertoire contienne hello abonnement Azure avec lequel vous avez créé votre coffre de clés. Si vous ne savez pas quel répertoire cela est, cliquez sur **paramètres**, d’identifier l’abonnement hello avec lequel vous avez créé votre coffre de clés et nom de hello note du répertoire de hello affiché dans la dernière colonne de hello.
3. Cliquez sur **APPLICATIONS**. Si aucune application n’a été ajoutée tooyour active, cette page affiche uniquement hello **ajouter une application** lien. Cliquez sur le lien de hello, ou vous pouvez également cliquer sur **ajouter** sur la barre de commandes hello.
4. Bonjour **ajouter une APPLICATION** Assistant, sur hello **comment vous souhaitez toodo ?** , cliquez sur **ajouter une application développée par mon organisation**.
5. Sur hello **Parlez-nous de votre application** page, spécifiez un nom pour votre application, puis sélectionnez **WEB APPLICATION et/ou API WEB** (hello par défaut). Cliquez sur hello **suivant** icône.
6. Sur hello **propriétés de l’application** , spécifiez hello **URL de connexion** et **URI ID d’application** pour votre application web. Si votre application n’a pas ces valeurs, vous pouvez les créer pour cette étape (par exemple, vous pouvez spécifier http://test1.contoso.com pour les deux zones). Peu importe si ces sites existent. L’essentiel est que URI ID d’application hello pour chaque application est différente pour chaque application dans votre annuaire. répertoire de Hello utilise tooidentify de cette chaîne de votre application.
7. Cliquez sur hello **Complete** icône toosave vos modifications dans l’Assistant de hello.
8. Sur hello **Quick Start** , cliquez sur **configurer**.
9. Faites défiler toohello **clés** section, sélectionnez la durée de hello, puis cliquez sur **enregistrer**. page de Hello actualise et affiche maintenant une valeur de clé. Vous devez configurer votre application avec cette valeur de clé et le hello **ID CLIENT** valeur. (Les instructions relatives à cette configuration sont propres à l’application.)
10. Copiez la valeur d’ID client hello à partir de cette page, vous allez utiliser dans hello prochaine étape tooset des autorisations sur votre coffre.

## <a id="authorize"></a>Autoriser hello application toouse hello clé ou le secret
tooauthorize hello application tooaccess hello clé ou le secret de coffre hello, utilisez le [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) applet de commande.

Par exemple, si le nom de votre coffre est **ContosoKeyVault** , puis hello application tooauthorize a l’ID client 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed et que vous souhaitez tooauthorize hello application toodecrypt et connectez-vous avec les clés dans le coffre, exécutez hello suivante :

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

Si vous souhaitez tooauthorize que secrets de tooread même application dans le coffre, exécutez suivante de hello :

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get

## <a id="HSM"></a>Si vous voulez toouse un module de sécurité matériel (HSM)
Pour plus de sûreté, vous pouvez importer ou générer des clés dans les modules de sécurité matériel (HSM) qui ne quittent jamais les limites HSM hello. Hello HSM sont FIPS 140-2 niveau 2 validé. Si cette exigence ne s’applique pas tooyou, ignorez cette section et passez trop[supprimer le coffre de clés hello et les clés associées et les secrets](#delete).

toocreate ces clés protégées par HSM, vous devez utiliser hello [clés protégées par HSM toosupport le niveau de service Azure Key Vault Premium](https://azure.microsoft.com/pricing/free-trial/). En outre, notez que cette fonctionnalité n’est pas disponible pour Azure en Chine.

Lorsque vous créez le coffre de clés hello, ajouter hello **- référence (SKU)** paramètre :

    New-AzureRmKeyVault -VaultName 'ContosoKeyVaultHSM' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -SKU 'Premium'



Vous pouvez ajouter les clés à protection logicielle (comme indiqué plus haut) et le coffre de clés toothis clés protégées par HSM. toocreate une clé protégée par HSM, jeu hello **-Destination** too'HSM de paramètre ' :

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -Destination 'HSM'

Vous pouvez utiliser hello suivant commande tooimport une clé à partir d’un. Fichier PFX sur votre ordinateur. Cette commande importe la clé de hello dans les modules HSM Bonjour service Key Vault :

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd -Destination 'HSM'


commande suivant Hello importe un « apportez votre propre clé » package (BYOK). Ce scénario vous permet de générer votre clé dans votre HSM local et la transférez tooHSMs Bonjour service Key Vault, sans clé hello en laissant la limite HSM hello :

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\ITByok.byok' -Destination 'HSM'

Pour plus d’instructions sur la procédure toogenerate ce package BYOK, consultez [comment toogenerate et transfert de clés protégées par HSM pour Azure Key Vault](key-vault-hsm-protected-keys.md).

## <a id="delete"></a>Supprimer le coffre de clés hello et les clés associées et les secrets
Si vous n’avez plus besoin coffre de clés hello et clé de hello ou le secret qu’il contient, vous pouvez supprimer le coffre de clés hello à l’aide de hello [Remove-AzureRmKeyVault](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) applet de commande :

    Remove-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Ou bien, vous pouvez supprimer un groupe de ressources Azure entier, ce qui inclut le coffre de clés hello et d’autres ressources que vous avez incluses dans ce groupe :

    Remove-AzureRmResourceGroup -ResourceGroupName 'ContosoResourceGroup'


## <a id="other"></a>Autres applets de commande Azure PowerShell
Autres commandes pouvant être utiles pour la gestion du coffre de clés Azure.

* `$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`: cette commande permet d’obtenir un affichage sous forme de tableau de l’ensemble des clés et propriétés sélectionnées.
* `$Keys[0]`: Cette commande affiche une liste complète des propriétés de clé spécifiée de hello
* `Get-AzureKeyVaultSecret`: cette commande permet d’obtenir un affichage sous forme de tableau de l’ensemble des secrets et des propriétés sélectionnés.
* `Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`: Exemple comment tooremove une clé spécifique.
* `Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`: Exemple comment tooremove un secret spécifique.

## <a id="next"></a>Étapes suivantes
Pour assurer le suivi d'un didacticiel sur l'utilisation d'Azure Key Vault dans une application web, consultez la page [Utilisation d'Azure Key Vault à partir d'une application web](key-vault-use-from-web-application.md).

toosee votre coffre de clés est utilisée, voir [journalisation d’Azure Key Vault](key-vault-logging.md).

Pour obtenir la liste des dernières applets de commande PowerShell Azure hello pour Azure Key Vault, consultez [applets de commande Azure Key Vault](/powershell/module/azurerm.keyvault/#key_vault).

Pour les références de programmation, consultez [hello guide du développeur Azure Key Vault](key-vault-developers-guide.md).
