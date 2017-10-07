---
title: "aaaManage Azure Key Vault à l’aide de CLI | Documents Microsoft"
description: "Utilisez ce didacticiel tooautomate des tâches courantes dans le coffre de clés à l’aide de hello CLI 2.0"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a>Gestion de Key Vault à l’aide de l’interface de ligne de commande (CLI) 2.0
Azure Key Vault est disponible dans la plupart des régions. Pour plus d’informations, consultez hello [page de tarification de coffre de clés](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introduction
Utilisez ce didacticiel toohelp que vous obtenez en main d’Azure Key Vault toocreate un conteneur renforcé (un coffre) dans Azure, toostore et gérer les clés de chiffrement et les clés secrètes dans Azure. Il vous guide tout au long des processus de hello d’à l’aide d’une Interface de ligne multiplateforme Azure toocreate un coffre qui contient une clé ou un mot de passe que vous pouvez ensuite utiliser avec une application Windows Azure. Il vous montre également comment une application peut ensuite utiliser cette clé ou ce mot de passe.

**Estimation du temps toocomplete :** 20 minutes

> [!NOTE]
> Ce didacticiel n’inclut pas d’obtenir des instructions sur la façon dont toowrite hello Azure application incluant une des étapes de hello, qui montre comment tooauthorize un toouse application une clé ou au secret dans la clé de hello coffre.
>
> Ce didacticiel utilise hello dernière Azure CLI 2.0.
>
>

Pour plus d’informations générales sur Azure Key Vault, consultez la page [Présentation d’Azure Key Vault](key-vault-whatis.md)

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez avoir hello suivant :

* Un abonnement tooMicrosoft Azure. Si vous n’en avez pas, vous pouvez vous inscrire pour bénéficier d’un [essai gratuit](https://azure.microsoft.com/pricing/free-trial)dès aujourd’hui.
* Interface de ligne de commande Azure, version 2.0 ou ultérieure. tooinstall hello version la plus récente et se connecter tooyour abonnement Azure, consultez [installer et configurer hello une Interface de ligne de Cross-Platform Azure 2.0](/cli/azure/install-azure-cli).
* Une application qui sera la clé de hello toouse configuré ou le mot de passe que vous créez dans ce didacticiel. Un exemple d’application est disponible à partir de hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343). Pour obtenir des instructions, consultez hello qui accompagne le fichier Lisez-moi.

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a>Obtention d’aide avec l’interface de ligne de commande interplateforme Azure
Ce didacticiel suppose que vous êtes familiarisé avec une interface de ligne hello (interpréteur de commandes, Terminal Server, invite de commandes)

Hello--help ou-h paramètre peut être utilisé tooview aide pour des commandes spécifiques. Ou bien, l’aide hello azure [commande] [options] format peut également être utilisé tooreturn hello mêmes informations. Par exemple, suivant de hello commandes retournent tous les hello les mêmes informations :

```
az account set --help
az account set -h
```

En cas de doute sur les paramètres de hello requis par une commande, reportez-vous à l’aide de toohelp--help, -h ou az help [commande].

Vous pouvez également lire hello suivant tooget didacticiels familiarisé avec Azure Resource Manager dans une Interface de ligne multiplateforme Azure :

* [Installation de l’interface de ligne de commande Azure](/cli/azure/install-azure-cli)
* [Prise en main d’Azure CLI 2.0](/cli/azure/get-started-with-azure-cli)

## <a name="connect-tooyour-subscriptions"></a>Se connecter tooyour abonnements
toolog à l’aide d’un compte professionnel, hello utilisez commande suivante :

```
az login -u username@domain.com -p password
```

ou si vous voulez toolog en tapant de manière interactive

```
az login
```

Si vous avez plusieurs abonnements et que vous souhaitez toospecify un un toouse spécifique pour Azure Key Vault, tapez Bonjour suivant toosee les abonnements de hello pour votre compte :

```
az account list
```

Ensuite, toospecify hello abonnement toouse, type :

```
az account set --subscription <subscription name or ID>
```

Pour plus d’informations sur la configuration de l’interface de ligne de commande multiplateforme Azure, consultez la page [Installation de l’interface de ligne de commande multiplateforme Azure](/cli/azure/install-azure-cli).

## <a name="create-a-new-resource-group"></a>Création d’un groupe de ressources
Lorsque vous utilisez Azure Resource Manager, toutes les ressources associées sont créées au sein d’un groupe de ressources. Nous allons créer un groupe de ressources nommé « ContosoResourceGroup » pour ce didacticiel.

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

premier paramètre de Hello est le nom de groupe de ressources et hello deuxième paramètre est emplacement de hello. Pour l’emplacement, utilisez la commande hello `az account list-locations` tooidentify comment toospecify un autre emplacement toohello un dans cet exemple. Si vous avez besoin de plus d’informations, tapez : `az account list-locations -h`.

## <a name="register-hello-key-vault-resource-provider"></a>Inscrire le fournisseur de ressources hello coffre de clés
Assurez-vous que le fournisseur de ressources Key Vault est inscrit dans votre abonnement :

```
az provider register -n Microsoft.KeyVault
```

Cette opération ne doit toobe réalisée une fois par abonnement.

## <a name="create-a-key-vault"></a>Création d’un coffre de clés
Hello d’utilisation `az keyvault create` commande toocreate un coffre de clés. Ce script a trois paramètres obligatoires : un nom de groupe de ressources, d’un coffre de clés et d’un emplacement géographique de hello.

Par exemple, si vous utilisez le nom du coffre hello de ContosoKeyVault, nom de groupe de ressources hello de ContosoResourceGroup et l’emplacement de hello d’Asie orientale, tapez :
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

sortie Hello de cette commande affiche les propriétés du coffre de clés hello que vous venez de créer. propriétés les plus importantes Hello deux sont :

* **nom**: dans l’exemple de hello, cela est ContosoKeyVault. Vous allez utiliser ce nom pour les autres commandes Key Vault.
* **vaultUri**: dans l’exemple de hello, cela est https://contosokeyvault.vault.azure.net. Les applications qui utilisent votre coffre via son API REST doivent utiliser cet URI.

Votre compte Azure est désormais toutes les opérations sur cette clé de coffre tooperform autorisé. coffre de clés.

## <a name="add-a-key-or-secret-toohello-key-vault"></a>Ajouter une clé ou un coffre de clés secrètes toohello
Si vous souhaitez que le coffre de clés Azure toocreate une clé protégée par logiciel pour vous, utilisez hello `az key create` de commandes et tapez Bonjour qui suit :
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
Toutefois, si vous avez une clé existante dans un fichier .pem enregistré en tant que fichier local dans un fichier nommé softkey.pem que vous souhaitez tooupload tooAzure le coffre de clés, tapez Bonjour suivant clé de hello tooimport hello. Fichier PEM, qui protège la clé de hello par logiciel dans hello service Key Vault :
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
Vous pouvez maintenant référencer clé hello que vous avez créé ou téléchargé tooAzure le coffre de clés, à l’aide de son URI. Utilisez **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways obtenir la version actuelle de hello et utiliser **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget cette version spécifique.

tooadd un coffre toohello secrète, qui est un mot de passe nommé SQLPassword et qui a valeur hello Pa$ $w0rd tooAzure le coffre de clés, hello du type suivant :
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
Vous pouvez maintenant référencer ce mot de passe que vous avez ajouté tooAzure le coffre de clés, à l’aide de son URI. Utilisez **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways obtenir la version actuelle de hello et utiliser **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget cette version spécifique.

Examinons la clé de hello ou le secret que vous venez de créer :

* tooview votre type de clé, :`az keyvault key list --vault-name 'ContosoKeyVault'`
* tooview votre secret principal, type :`az keyvault secret list --vault-name 'ContosoKeyVault'`

## <a name="register-an-application-with-azure-active-directory"></a>Inscription d’une application auprès d’Azure Active Directory
Cette étape est généralement effectuée par un développeur et sur un ordinateur distinct. Il n’est pas spécifique tooAzure le coffre de clés, mais est inclus ici, par souci d’exhaustivité.

> [!IMPORTANT]
> didacticiel de hello toocomplete, votre compte, le coffre de hello et l’application hello que vous inscrivez dans cette étape doivent toutes être Bonjour même annuaire Azure.
>
>

Les applications qui utilisent un coffre de clés doivent s’authentifier à l’aide d’un jeton à partir d’Azure Active Directory. toodo, hello propriétaire de l’application hello doit inscrire tout d’abord des application hello dans leur annuaire Active Directory de Azure. À fin hello d’enregistrement, le propriétaire de l’application hello obtient hello valeurs suivantes :

* Un **ID d’Application** (également appelé ID de Client) et **clé d’authentification** (également appelé un secret partagé hello). application Hello doit présenter les deux de ces valeurs de tooAzure Active Directory, tooget un jeton. Comment application hello est configuré toodo que cela dépend application hello. Pour un exemple d’application le coffre de clés de hello, le propriétaire de l’application hello définit ces valeurs dans le fichier app.config hello.

application hello tooregister dans Azure Active Directory :

1. Se connecter toohello portail Azure.
2. Sur hello gauche, cliquez sur **Azure Active Directory**, puis sélectionnez le répertoire hello dans lequel vous allez inscrire votre application. <br> <br> 

> [!Note] 
> Vous devez sélectionner hello même répertoire contienne hello abonnement Azure avec lequel vous avez créé votre coffre de clés. Si vous ne savez pas quel répertoire cela est, cliquez sur **paramètres**, d’identifier l’abonnement hello avec lequel vous avez créé votre coffre de clés et nom de hello note du répertoire de hello affiché dans la dernière colonne de hello.

3. Cliquez sur **APPLICATIONS**. Si aucune application n’a été ajoutée tooyour active, cette page affiche uniquement hello **ajouter une application** lien. Cliquez sur le lien de hello, ou vous pouvez également cliquer hello **ajouter** sur la barre de commandes hello.
4. Bonjour **ajouter une APPLICATION** Assistant, sur hello **comment vous souhaitez toodo ?** , cliquez sur **ajouter une application développée par mon organisation**.
5. Sur hello **Parlez-nous de votre application** page, spécifiez un nom pour votre application et sélectionnez **WEB APPLICATION et/ou API WEB** (hello par défaut). Cliquez sur icône suivant de hello.
6. Sur hello **propriétés de l’application** , spécifiez hello **URL de connexion** et **URI ID d’application** pour votre application web. Si votre application n’a pas ces valeurs, vous pouvez les créer pour cette étape (par exemple, vous pouvez spécifier http://test1.contoso.com pour les deux zones). Il n’a pas d’importance s’il existe de ces sites ; l’essentiel est que URI ID d’application hello pour chaque application est différente pour chaque application dans votre annuaire. répertoire de Hello utilise tooidentify de cette chaîne de votre application.
7. Cliquez sur hello icône terminée toosave vos modifications dans l’Assistant de hello.
8. Dans la page de démarrage rapide de hello, cliquez sur **configurer**.
9. Faites défiler toohello **clés** section, sélectionnez la durée de hello, puis cliquez sur **enregistrer**. page de Hello actualise et affiche maintenant une valeur de clé. Vous devez configurer votre application avec cette valeur de clé et le hello **ID CLIENT** valeur. (Les instructions relatives à cette configuration sont propres à l’application).
10. Copiez la valeur d’ID client hello à partir de cette page, vous allez utiliser dans hello prochaine étape tooset des autorisations sur votre coffre.

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a>Autoriser hello application toouse hello clé ou le secret
tooauthorize hello application tooaccess hello clé ou le secret de coffre hello, utilisez hello `az keyvault set-policy` commande.

Par exemple, si votre nom de coffre est ContosoKeyVault et hello application souhaité tooauthorize a l’ID client 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, et que vous souhaitez tooauthorize hello application toodecrypt et connectez-vous avec des clés dans le coffre, puis exécutez hello suivant :
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

Si vous souhaitez tooauthorize que secrets de tooread même application dans le coffre, exécutez suivante de hello :
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a>Si vous voulez toouse un module de sécurité matériel (HSM)
Pour plus de sûreté, vous pouvez importer ou générer des clés dans les modules de sécurité matériel (HSM) qui ne quittent jamais les limites HSM hello. Hello HSM sont FIPS 140-2 niveau 2 validé. Si cette exigence ne s’applique pas tooyou, ignorez cette section et passez trop[supprimer le coffre de clés hello et les clés associées et les secrets](#delete-the-key-vault-and-associated-keys-and-secrets).

toocreate ces clés protégées par HSM, vous devez avoir un abonnement de coffre qui prend en charge les clés protégées par HSM.

Lorsque vous créez hello keyvault, ajouter le paramètre de 'sku' hello :

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
Vous pouvez ajouter des clés protégées par le logiciel (comme indiqué plus haut) et de coffre de clés protégées par HSM toothis. toocreate une clé protégée par HSM, jeu hello Destination paramètre too'HSM':

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

Vous pouvez utiliser hello suivant commande tooimport une clé à partir d’un fichier .pem sur votre ordinateur. Cette commande importe la clé de hello dans les modules HSM Bonjour service Key Vault :

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
commande suivant Hello importe un « apportez votre propre clé » package (BYOK). Cela vous permet de générer votre clé dans votre HSM local et la transférez tooHSMs Bonjour service Key Vault, sans clé hello en laissant la limite HSM hello :

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
Pour plus d’instructions sur la procédure toogenerate ce package BYOK, consultez [comment toouse clés HSM-Protected avec Azure Key Vault](key-vault-hsm-protected-keys.md).

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a>Supprimer le coffre de clés hello et les clés associées et les secrets
Si vous n’avez plus besoin coffre de clés hello et clé de hello ou le secret qu’il contient, vous pouvez supprimer le coffre de clés hello à l’aide de hello `az keyvault delete` commande :

```
az keyvault delete --name 'ContosoKeyVault'
```

Ou bien, vous pouvez supprimer un groupe de ressources Azure entier, ce qui inclut le coffre de clés hello et d’autres ressources que vous avez incluses dans ce groupe :

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a>Autres interfaces de ligne de commande interplateformes Azure
Autres commandes qui peuvent être utiles pour la gestion d’Azure Key Vault.

Cette commande permet d’obtenir un affichage sous forme de tableau de l’ensemble des clés et des propriétés sélectionnées :

az keyvault key list --vault-name 'ContosoKeyVault'

Cette commande affiche une liste complète des propriétés de clé spécifiée de hello :

az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'

Cette commande permet d’obtenir un affichage sous forme de tableau de l’ensemble des secrets et des propriétés sélectionnées.

az keyvault secret list --vault-name 'ContosoKeyVault'

Voici un exemple de procédure tooremove une clé spécifique :

az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'

Voici un exemple de procédure tooremove un secret spécifique :

az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'


## <a name="next-steps"></a>Étapes suivantes
Pour accéder à une documentation de référence complète sur l’interface Azure CLI pour les commandes Key Vault, consultez le document de [référence sur l’interface de ligne de commande Key Vault](/cli/azure/keyvault).

Pour les références de programmation, consultez [hello guide du développeur Azure Key Vault](key-vault-developers-guide.md).
