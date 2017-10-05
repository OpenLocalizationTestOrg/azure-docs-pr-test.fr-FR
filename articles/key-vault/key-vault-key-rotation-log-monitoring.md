---
title: "Configuration d’Azure Key Vault avec une rotation des clés et un audit de bout en bout | Microsoft Docs"
description: "Utilisez cette procédure pour configurer la rotation des clés et la surveillance des journaux de Key Vault."
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: 38c342802ed687985ac6f84f5a590a1a0dcc6c6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a><span data-ttu-id="22fd8-103">Configurer Azure Key Vault avec une rotation des clés et un audit de bout en bout</span><span class="sxs-lookup"><span data-stu-id="22fd8-103">Set up Azure Key Vault with end-to-end key rotation and auditing</span></span>
## <a name="introduction"></a><span data-ttu-id="22fd8-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="22fd8-104">Introduction</span></span>
<span data-ttu-id="22fd8-105">Une fois votre coffre de clés (Key Vault) créé, vous pouvez commencer à l’utiliser pour stocker vos clés et secrets.</span><span class="sxs-lookup"><span data-stu-id="22fd8-105">After creating your key vault, you will be able to start using that vault to store your keys and secrets.</span></span> <span data-ttu-id="22fd8-106">Vos applications ne doivent plus nécessairement conserver vos clés et secrets, mais les demanderont au coffre de clés en cas de besoin.</span><span class="sxs-lookup"><span data-stu-id="22fd8-106">Your applications no longer need to persist your keys or secrets, but rather will request them from the key vault as needed.</span></span> <span data-ttu-id="22fd8-107">Cela vous permet de mettre à jour les clés et les secrets sans affecter le comportement de votre application, et de disposer ainsi de toute une multitude de possibilités de gestion des clés et secrets.</span><span class="sxs-lookup"><span data-stu-id="22fd8-107">This allows you to update keys and secrets without affecting the behavior of your application, which opens up a breadth of possibilities around your key and secret management.</span></span>

<span data-ttu-id="22fd8-108">Cet article présente un exemple d’utilisation d’Azure Key Vault pour stocker un secret, dans notre exemple une clé de compte de stockage Azure à laquelle une application accède.</span><span class="sxs-lookup"><span data-stu-id="22fd8-108">This article walks through an example of using Azure Key Vault to store a secret, in this case an Azure Storage Account key that is accessed by an application.</span></span> <span data-ttu-id="22fd8-109">Il vous propose également une démonstration d’implémentation d’une rotation planifiée de cette clé de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="22fd8-109">It also demonstrates implementation of a scheduled rotation of that storage account key.</span></span> <span data-ttu-id="22fd8-110">Pour finir, il vous présente, par le biais d’une démonstration, comment contrôler les journaux d’audit du coffre de clés et déclencher des alertes en cas de requêtes inattendues.</span><span class="sxs-lookup"><span data-stu-id="22fd8-110">Finally, it walks through a demonstration of how to monitor the key vault audit logs and raise alerts when unexpected requests are made.</span></span>

> [!NOTE]
> <span data-ttu-id="22fd8-111">Ce didacticiel n’a pas pour vocation d’expliquer en détail la configuration initiale de votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="22fd8-111">This tutorial is not intended to explain in detail the initial setup of your key vault.</span></span> <span data-ttu-id="22fd8-112">Pour plus d’informations, consultez [Prise en main d’Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="22fd8-112">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="22fd8-113">Pour connaître la marche à suivre avec l’interface de ligne de commande interplateforme, consultez la rubrique [Gestion de Key Vault à l’aide de l’interface de ligne de commande (CLI)](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="22fd8-113">For Cross-Platform Command-Line Interface instructions, see [Manage Key Vault using CLI](key-vault-manage-with-cli2.md).</span></span>
>
>

## <a name="set-up-key-vault"></a><span data-ttu-id="22fd8-114">Configuration d’Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="22fd8-114">Set up Key Vault</span></span>
<span data-ttu-id="22fd8-115">Pour qu’une application puisse récupérer un secret dans Key Vault, vous devez tout d’abord créer le secret et le télécharger dans votre coffre.</span><span class="sxs-lookup"><span data-stu-id="22fd8-115">To enable an application to retrieve a secret from Key Vault, you must first create the secret and upload it to your vault.</span></span> <span data-ttu-id="22fd8-116">Procédez en démarrant une session Azure PowerShell et en vous connectant à votre compte Azure avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="22fd8-116">This can be accomplished by starting an Azure PowerShell session and signing in to your Azure account with the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="22fd8-117">Dans la fenêtre contextuelle de votre navigateur, entrez votre nom d’utilisateur et votre mot de passe Azure.</span><span class="sxs-lookup"><span data-stu-id="22fd8-117">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="22fd8-118">PowerShell obtient alors tous les abonnements associés à ce compte.</span><span class="sxs-lookup"><span data-stu-id="22fd8-118">PowerShell will get all the subscriptions that are associated with this account.</span></span> <span data-ttu-id="22fd8-119">PowerShell utilise le premier par défaut.</span><span class="sxs-lookup"><span data-stu-id="22fd8-119">PowerShell uses the first one by default.</span></span>

<span data-ttu-id="22fd8-120">Si vous disposez de plusieurs abonnements, vous devrez peut-être spécifier celui qui a été utilisé pour créer votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="22fd8-120">If you have multiple subscriptions, you might have to specify the one that was used to create your key vault.</span></span> <span data-ttu-id="22fd8-121">Entrez la commande suivante pour afficher les abonnements de votre compte :</span><span class="sxs-lookup"><span data-stu-id="22fd8-121">Enter the following to see the subscriptions for your account:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="22fd8-122">Pour spécifier l’abonnement associé au coffre de clés que vous allez consigner, entrez :</span><span class="sxs-lookup"><span data-stu-id="22fd8-122">To specify the subscription that's associated with the key vault you will be logging, enter:</span></span>

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

<span data-ttu-id="22fd8-123">Cet article présentant le stockage d’une clé de compte de stockage sous la forme d’un secret, vous devez obtenir cette clé de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="22fd8-123">Because this article demonstrates storing a storage account key as a secret, you must get that storage account key.</span></span>

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

<span data-ttu-id="22fd8-124">Une fois votre secret récupéré (votre clé de compte de stockage dans notre exemple), vous devez le convertir en une chaîne sécurisée, puis créer un secret avec cette valeur dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="22fd8-124">After retrieving your secret (in this case, your storage account key), you must convert that to a secure string and then create a secret with that value in your key vault.</span></span>

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
<span data-ttu-id="22fd8-125">Ensuite, obtenez l’URI pour le secret que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="22fd8-125">Next, get the URI for the secret you created.</span></span> <span data-ttu-id="22fd8-126">Il sera utilisé dans une étape ultérieure lorsque vous appellerez le coffre de clés pour récupérer votre secret.</span><span class="sxs-lookup"><span data-stu-id="22fd8-126">This is used in a later step when you call the key vault to retrieve your secret.</span></span> <span data-ttu-id="22fd8-127">Exécutez la commande PowerShell suivante et notez la valeur de l’ID, qui correspond à l’URI du secret :</span><span class="sxs-lookup"><span data-stu-id="22fd8-127">Run the following PowerShell command and make note of the ID value, which is the secret URI:</span></span>

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-the-application"></a><span data-ttu-id="22fd8-128">Configurer d’application</span><span class="sxs-lookup"><span data-stu-id="22fd8-128">Set up the application</span></span>
<span data-ttu-id="22fd8-129">Maintenant que vous disposez d’une clé secrète stockée, vous pouvez utiliser le code pour la récupérer et l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="22fd8-129">Now that you have a secret stored, you can use code to retrieve and use it.</span></span> <span data-ttu-id="22fd8-130">Quelques étapes sont nécessaires pour y parvenir.</span><span class="sxs-lookup"><span data-stu-id="22fd8-130">There are a few steps required to achieve this.</span></span> <span data-ttu-id="22fd8-131">La première et la plus importante d’entre elles consiste à enregistrer votre application dans Azure Active Directory et à fournir à Key Vault des informations sur votre application afin qu’il autorise les requêtes provenant de votre application.</span><span class="sxs-lookup"><span data-stu-id="22fd8-131">The first and most important step is registering your application with Azure Active Directory and then telling Key Vault your application information so that it can allow requests from your application.</span></span>

> [!NOTE]
> <span data-ttu-id="22fd8-132">Votre application doit être créée sur le même client Azure Active Directory que votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="22fd8-132">Your application must be created on the same Azure Active Directory tenant as your key vault.</span></span>
>
>

<span data-ttu-id="22fd8-133">Ouvrez l’onglet des applications d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="22fd8-133">Open the applications tab of Azure Active Directory.</span></span>

![Ouvrir des applications dans Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

<span data-ttu-id="22fd8-135">Choisissez **AJOUTER** pour ajouter une application à votre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="22fd8-135">Choose **ADD** to add an application to your Azure Active Directory.</span></span>

![Choisir AJOUTER](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

<span data-ttu-id="22fd8-137">Conservez le type d’application **APPLICATION WEB ET/OU API WEB** et donnez un nom à votre application.</span><span class="sxs-lookup"><span data-stu-id="22fd8-137">Leave the application type as **WEB APPLICATION AND/OR WEB API** and give your application a name.</span></span>

![Nommer l’application](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

<span data-ttu-id="22fd8-139">Attribuez à votre application une **URL DE CONNEXION** et un **URI ID D’APPLICATION**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-139">Give your application a **SIGN-ON URL** and an **APP ID URI**.</span></span> <span data-ttu-id="22fd8-140">Pour cette démonstration, il peut s’agir de n’importe quel URL/URI, et vous pouvez les modifier ultérieurement si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="22fd8-140">These can be anything you want for this demo, and they can be changed later if needed.</span></span>

![Fournir les URI nécessaires](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

<span data-ttu-id="22fd8-142">Une fois l’application ajoutée à Azure Active Directory, vous accédez à la page de l’application.</span><span class="sxs-lookup"><span data-stu-id="22fd8-142">After the application is added to Azure Active Directory, you will be brought into the application page.</span></span> <span data-ttu-id="22fd8-143">Cliquez sur l’onglet **Configurer**, puis recherchez et copiez la valeur de **l’ID client**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-143">Click the **Configure** tab and then find and copy the **Client ID** value.</span></span> <span data-ttu-id="22fd8-144">Notez l’ID client pour les étapes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="22fd8-144">Make note of the client ID for later steps.</span></span>

<span data-ttu-id="22fd8-145">Ensuite, générez une clé pour votre application afin qu’elle puisse interagir avec votre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="22fd8-145">Next, generate a key for your application so it can interact with your Azure Active Directory.</span></span> <span data-ttu-id="22fd8-146">Vous pouvez la créer dans la section **Clés** de l’onglet **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-146">You can create this under the **Keys** section in the **Configuration** tab.</span></span> <span data-ttu-id="22fd8-147">Notez la clé générée par votre application Azure Active Directory pour pouvoir l’utiliser dans une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="22fd8-147">Make note of the newly generated key from your Azure Active Directory application for use in a later step.</span></span>

![Clés d’application Azure Active Directory](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

<span data-ttu-id="22fd8-149">Avant de créer des appels de votre coffre de clés par votre application, vous devez fournir au coffre de clés des informations sur votre application et ses autorisations.</span><span class="sxs-lookup"><span data-stu-id="22fd8-149">Before establishing any calls from your application into the key vault, you must tell the key vault about your application and its permissions.</span></span> <span data-ttu-id="22fd8-150">La commande suivante récupère le nom du coffre et l’ID client dans votre application Azure Active Directory et accorde à l’application un accès **Get** à votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="22fd8-150">The following command takes the vault name and the client ID from your Azure Active Directory app and grants **Get** access to your key vault for the application.</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

<span data-ttu-id="22fd8-151">À ce stade, vous êtes prêt à créer vos appels d’application.</span><span class="sxs-lookup"><span data-stu-id="22fd8-151">At this point, you are ready to start building your application calls.</span></span> <span data-ttu-id="22fd8-152">Dans votre application, vous devez installer les packages NuGet nécessaires pour interagir avec Azure Key Vault et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="22fd8-152">In your application, you must install the NuGet packages required to interact with Azure Key Vault and Azure Active Directory.</span></span> <span data-ttu-id="22fd8-153">Entrez les commandes suivantes dans la console du gestionnaire de package Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="22fd8-153">From the Visual Studio Package Manager console, enter the following commands.</span></span> <span data-ttu-id="22fd8-154">Au moment de la rédaction de cet article, la version du package Azure Active Directory est la version 3.10.305231913. Nous vous conseillons donc de vérifier que vous disposez de la dernière version et de mettre à jour si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="22fd8-154">At the writing of this article, the current version of the Azure Active Directory package is 3.10.305231913, so you might want to confirm the latest version and update accordingly.</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

<span data-ttu-id="22fd8-155">Dans votre code d’application, créez une classe qui contiendra la méthode d’authentification de votre Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="22fd8-155">In your application code, create a class to hold the method for your Azure Active Directory authentication.</span></span> <span data-ttu-id="22fd8-156">Dans cet exemple, la classe est appelée **Utils**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-156">In this example, that class is called **Utils**.</span></span> <span data-ttu-id="22fd8-157">Ajoutez les instructions using suivantes :</span><span class="sxs-lookup"><span data-stu-id="22fd8-157">Add the following using statement:</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="22fd8-158">Ajoutez ensuite la méthode suivante pour récupérer le jeton JWT d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="22fd8-158">Next, add the following method to retrieve the JWT token from Azure Active Directory.</span></span> <span data-ttu-id="22fd8-159">Pour faciliter la maintenance, vous souhaiterez peut-être déplacer les valeurs de chaîne codées en dur dans votre configuration web ou d’application.</span><span class="sxs-lookup"><span data-stu-id="22fd8-159">For maintainability, you may want to move the hard-coded string values into your web or application configuration.</span></span>

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

<span data-ttu-id="22fd8-160">Ajoutez le code nécessaire pour appeler Key Vault et récupérer votre valeur secrète.</span><span class="sxs-lookup"><span data-stu-id="22fd8-160">Add the necessary code to call Key Vault and retrieve your secret value.</span></span> <span data-ttu-id="22fd8-161">Vous devez tout d’abord ajouter l’instruction « using » suivante :</span><span class="sxs-lookup"><span data-stu-id="22fd8-161">First you must add the following using statement:</span></span>

```csharp
using Microsoft.Azure.KeyVault;
```

<span data-ttu-id="22fd8-162">Ajoutez les appels de méthode pour appeler Key Vault et récupérer votre secret.</span><span class="sxs-lookup"><span data-stu-id="22fd8-162">Add the method calls to invoke Key Vault and retrieve your secret.</span></span> <span data-ttu-id="22fd8-163">Dans cette méthode, vous fournissez l’URI de secret que vous avez enregistré dans une étape précédente.</span><span class="sxs-lookup"><span data-stu-id="22fd8-163">In this method, you provide the secret URI that you saved in a previous step.</span></span> <span data-ttu-id="22fd8-164">Notez l’utilisation de la méthode **GetToken** à partir de la classe **Utils** créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="22fd8-164">Note the use of the **GetToken** method from the **Utils** class created previously.</span></span>

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

<span data-ttu-id="22fd8-165">Lorsque vous exécutez votre application, vous devez désormais vous authentifier auprès d’Azure Active Directory et récupérer votre valeur secrète dans Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="22fd8-165">When you run your application, you should now be authenticating to Azure Active Directory and then retrieving your secret value from Azure Key Vault.</span></span>

## <a name="key-rotation-using-azure-automation"></a><span data-ttu-id="22fd8-166">Rotation des clés à l’aide d’Azure Automation</span><span class="sxs-lookup"><span data-stu-id="22fd8-166">Key rotation using Azure Automation</span></span>
<span data-ttu-id="22fd8-167">Diverses options de mise en œuvre d’une stratégie de rotation sont possibles pour les valeurs que vous stockez sous forme de secrets Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="22fd8-167">There are various options for implementing a rotation strategy for values you store as Azure Key Vault secrets.</span></span> <span data-ttu-id="22fd8-168">La rotation des secrets peut être manuelle, elle peut également être effectuée par programmation à l’aide d’appels d’API ou à l’aide d’un script Automation.</span><span class="sxs-lookup"><span data-stu-id="22fd8-168">Secrets can be rotated as part of a manual process, they may be rotated programmatically by using API calls, or they may be rotated by way of an Automation script.</span></span> <span data-ttu-id="22fd8-169">Dans cet article, vous utiliserez Azure PowerShell et Azure Automation pour modifier une clé d’accès de compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="22fd8-169">For the purposes of this article, you will be using Azure PowerShell combined with Azure Automation to change an Azure Storage Account access key.</span></span> <span data-ttu-id="22fd8-170">Ensuite, vous mettrez à jour un secret de coffre de clés avec cette nouvelle clé.</span><span class="sxs-lookup"><span data-stu-id="22fd8-170">You will then update a key vault secret with that new key.</span></span>

<span data-ttu-id="22fd8-171">Pour qu’Azure Automation puisse définir des valeurs secrètes dans votre coffre de clés, vous devez obtenir l’ID client pour la connexion nommée AzureRunAsConnection créée pendant la définition de votre instance Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="22fd8-171">To allow Azure Automation to set secret values in your key vault, you must get the client ID for the connection named AzureRunAsConnection, which was created when you established your Azure Automation instance.</span></span> <span data-ttu-id="22fd8-172">Vous pouvez obtenir cet ID en choisissant **Actifs** dans votre instance Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="22fd8-172">You can find this ID by choosing **Assets** from your Azure Automation instance.</span></span> <span data-ttu-id="22fd8-173">Sélectionnez ensuite **Connexions**, puis le principal du service **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-173">From there, you choose **Connections** and then select the **AzureRunAsConnection** service principle.</span></span> <span data-ttu-id="22fd8-174">Notez **l’ID d’application**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-174">Take note of the **Application ID**.</span></span>

![ID client Azure Automation](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

<span data-ttu-id="22fd8-176">Dans **Actifs**, choisissez **Modules**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-176">In **Assets**, choose **Modules**.</span></span> <span data-ttu-id="22fd8-177">Sous **Modules**, sélectionnez **Galerie**, puis recherchez et **importez** les versions à jour de chacun des modules suivants :</span><span class="sxs-lookup"><span data-stu-id="22fd8-177">From **Modules**, select **Gallery**, and then search for and **Import** updated versions of each of the following modules:</span></span>

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> <span data-ttu-id="22fd8-178">Au moment de la rédaction de cet article, seuls les modules mentionnés précédemment devaient être mis à jour pour le script suivant.</span><span class="sxs-lookup"><span data-stu-id="22fd8-178">At the writing of this article, only the previously noted modules needed to be updated for the following script.</span></span> <span data-ttu-id="22fd8-179">Si vous constatez un échec de votre tâche d’automatisation, vérifiez que tous les modules nécessaires et leurs dépendances ont été importés.</span><span class="sxs-lookup"><span data-stu-id="22fd8-179">If you find that your automation job is failing, confirm that you have imported all necessary modules and their dependencies.</span></span>
>
>

<span data-ttu-id="22fd8-180">Une fois que vous avez récupéré l’ID d’application pour votre connexion Azure Automation, vous devez indiquer à votre coffre de clés que cette application est autorisée à accéder aux secrets dans votre coffre pour les mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="22fd8-180">After you have retrieved the application ID for your Azure Automation connection, you must tell your key vault that this application has access to update secrets in your vault.</span></span> <span data-ttu-id="22fd8-181">Cela peut être effectué avec la commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="22fd8-181">This can be accomplished with the following PowerShell command:</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

<span data-ttu-id="22fd8-182">Sélectionnez ensuite **Runbooks** sous votre instance Azure Automation, puis **Ajouter un runbook**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-182">Next, select **Runbooks** under your Azure Automation instance, and then select **Add a Runbook**.</span></span> <span data-ttu-id="22fd8-183">Sélectionnez **Création rapide**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-183">Select **Quick Create**.</span></span> <span data-ttu-id="22fd8-184">Donnez un nom à votre runbook et sélectionnez **PowerShell** comme type de runbook.</span><span class="sxs-lookup"><span data-stu-id="22fd8-184">Name your runbook and select **PowerShell** as the runbook type.</span></span> <span data-ttu-id="22fd8-185">Vous avez la possibilité d’ajouter une description.</span><span class="sxs-lookup"><span data-stu-id="22fd8-185">You have the option to add a description.</span></span> <span data-ttu-id="22fd8-186">Pour finir, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-186">Finally, click **Create**.</span></span>

![Créer un runbook](./media/keyvault-keyrotation/Create_Runbook.png)

<span data-ttu-id="22fd8-188">Collez le script PowerShell suivant dans le volet de l’éditeur de votre nouveau runbook :</span><span class="sxs-lookup"><span data-stu-id="22fd8-188">Paste the following PowerShell script in the editor pane for your new runbook:</span></span>

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get the connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in to Azure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set the following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for the storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

<span data-ttu-id="22fd8-189">Dans le volet de l’éditeur, choisissez le volet **Test** pour tester votre script.</span><span class="sxs-lookup"><span data-stu-id="22fd8-189">From the editor pane, choose **Test pane** to test your script.</span></span> <span data-ttu-id="22fd8-190">Une fois le script exécutez sans erreur, vous pouvez sélectionner **Publier**, puis appliquer une planification du runbook dans le volet de configuration du runbook.</span><span class="sxs-lookup"><span data-stu-id="22fd8-190">Once the script is running without error, you can select **Publish**, and then you can apply a schedule for the runbook back in the runbook configuration pane.</span></span>

## <a name="key-vault-auditing-pipeline"></a><span data-ttu-id="22fd8-191">Pipeline d’audit de Key Vault</span><span class="sxs-lookup"><span data-stu-id="22fd8-191">Key Vault auditing pipeline</span></span>
<span data-ttu-id="22fd8-192">Lorsque vous configurez un coffre de clés, vous pouvez activer la fonction d’audit afin de collecter des journaux de demandes d’accès au coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="22fd8-192">When you set up a key vault, you can turn on auditing to collect logs on access requests made to the key vault.</span></span> <span data-ttu-id="22fd8-193">Ces journaux sont stockés dans un compte de stockage Azure spécifié et peuvent être récupérés, contrôlés et analysés.</span><span class="sxs-lookup"><span data-stu-id="22fd8-193">These logs are stored in a designated Azure Storage account and can be pulled out, monitored, and analyzed.</span></span> <span data-ttu-id="22fd8-194">Le scénario suivant utilise Azure Functions, Azure Logic Apps et des journaux d’audit du coffre de clés afin de créer un pipeline pour envoyer un e-mail lorsqu’une application qui ne correspond pas à l’ID de l’application web récupère´des secrets du coffre.</span><span class="sxs-lookup"><span data-stu-id="22fd8-194">The following scenario uses Azure functions, Azure logic apps, and key vault audit logs to create a pipeline to send an email when an app that does match the app ID of the web app retrieves secrets from the vault.</span></span>

<span data-ttu-id="22fd8-195">Vous devez tout d’abord activer la journalisation sur votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="22fd8-195">First, you must enable logging on your key vault.</span></span> <span data-ttu-id="22fd8-196">Vous pouvez utiliser pour cela les commandes PowerShell suivantes (pour plus de détails, consultez [key-vault-logging](key-vault-logging.md)) :</span><span class="sxs-lookup"><span data-stu-id="22fd8-196">This can be done via the following PowerShell commands (full details can be seen at [key-vault-logging](key-vault-logging.md)):</span></span>

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

<span data-ttu-id="22fd8-197">Une fois cette option activée, les journaux d’audit commencent la collecte dans le compte de stockage spécifié.</span><span class="sxs-lookup"><span data-stu-id="22fd8-197">After this is enabled, audit logs start collecting into the designated storage account.</span></span> <span data-ttu-id="22fd8-198">Ces journaux contiennent des événements indiquant la méthode et la date/l’heure d’accès à vos coffres de clés, et qui y a accédé.</span><span class="sxs-lookup"><span data-stu-id="22fd8-198">These logs contain events about how and when your key vaults are accessed, and by whom.</span></span>

> [!NOTE]
> <span data-ttu-id="22fd8-199">Vous pouvez accéder aux informations de journalisation 10 minutes après l’opération sur le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="22fd8-199">You can access your logging information 10 minutes after the key vault operation.</span></span> <span data-ttu-id="22fd8-200">Elles sont généralement disponibles plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="22fd8-200">It will usually be quicker than this.</span></span>
>
>

<span data-ttu-id="22fd8-201">L’étape suivante consiste à [créer une file d’attente Azure Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="22fd8-201">The next step is to [create an Azure Service Bus queue](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span> <span data-ttu-id="22fd8-202">C’est dans celle-ci que les journaux d’audit de coffre de clés sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="22fd8-202">This is where key vault audit logs are pushed.</span></span> <span data-ttu-id="22fd8-203">Lorsque les messages du journal d’audit se trouvent dans la file d’attente, l’application logique les récupère et agit en conséquence.</span><span class="sxs-lookup"><span data-stu-id="22fd8-203">When the audit log messages are in the queue, the logic app picks them up and acts on them.</span></span> <span data-ttu-id="22fd8-204">Procédez comme suit pour créer un Service Bus :</span><span class="sxs-lookup"><span data-stu-id="22fd8-204">Create a service bus with the following steps:</span></span>

1. <span data-ttu-id="22fd8-205">Créez un espace de noms Service Bus (si vous en avez déjà un et souhaitez l’utiliser ici, passez à l’étape 2).</span><span class="sxs-lookup"><span data-stu-id="22fd8-205">Create a Service Bus namespace (if you already have one that you want to use for this, skip to Step 2).</span></span>
2. <span data-ttu-id="22fd8-206">Recherchez le Service Bus dans le portail Azure, puis sélectionnez l’espace de noms dans lequel vous souhaitez créer la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="22fd8-206">Browse to the service bus in the Azure portal and select the namespace you want to create the queue in.</span></span>
3. <span data-ttu-id="22fd8-207">Sélectionnez **Nouveau** et choisissez **Service Bus > File d’attente**, puis entrez les informations demandées.</span><span class="sxs-lookup"><span data-stu-id="22fd8-207">Select **New** and choose **Service Bus > Queue** and enter the required details.</span></span>
4. <span data-ttu-id="22fd8-208">Sélectionnez les informations de connexion Service Bus en choisissant l’espace de noms et en cliquant sur **Informations de connexion**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-208">Select the Service Bus connection information by choosing the namespace and clicking **Connection Information**.</span></span> <span data-ttu-id="22fd8-209">Vous aurez besoin de ces informations dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="22fd8-209">You will need this information for the next section.</span></span>

<span data-ttu-id="22fd8-210">Ensuite, [créez une fonction Azure](../azure-functions/functions-create-first-azure-function.md) pour interroger les journaux de coffre de clés dans le compte de stockage et récupérer les nouveaux événements.</span><span class="sxs-lookup"><span data-stu-id="22fd8-210">Next, [create an Azure function](../azure-functions/functions-create-first-azure-function.md) to poll key vault logs within the storage account and pick up new events.</span></span> <span data-ttu-id="22fd8-211">Il s’agit d’une fonction déclenchée de manière planifiée.</span><span class="sxs-lookup"><span data-stu-id="22fd8-211">This will be a function that is triggered on a schedule.</span></span>

<span data-ttu-id="22fd8-212">Pour créer une fonction Azure, choisissez **Nouveau > Function App** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="22fd8-212">To create an Azure function, choose **New > Function App** in the Azure portal.</span></span> <span data-ttu-id="22fd8-213">Lors de la création, vous pouvez utiliser un plan d’hébergement existant ou en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="22fd8-213">During creation, you can use an existing hosting plan or create a new one.</span></span> <span data-ttu-id="22fd8-214">Vous pouvez également opter pour un hébergement dynamique.</span><span class="sxs-lookup"><span data-stu-id="22fd8-214">You could also opt for dynamic hosting.</span></span> <span data-ttu-id="22fd8-215">Vous trouverez plus d’informations sur les options d’hébergement de fonction dans la rubrique [Mise à l’échelle d’Azure Functions](../azure-functions/functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="22fd8-215">More details on Function hosting options can be found at [How to scale Azure Functions](../azure-functions/functions-scale.md).</span></span>

<span data-ttu-id="22fd8-216">Une fois la fonction Azure créée, accédez-y, choisissez une fonction de minuteur et C\#.</span><span class="sxs-lookup"><span data-stu-id="22fd8-216">When the Azure function is created, navigate to it and choose a timer function and C\#.</span></span> <span data-ttu-id="22fd8-217">Cliquez ensuite sur **Créer cette fonction**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-217">Then click **Create this function**.</span></span>

![Panneau d’accueil d’Azure Functions](./media/keyvault-keyrotation/Azure_Functions_Start.png)

<span data-ttu-id="22fd8-219">Dans l’onglet **Développement** , remplacez le code run.csx par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="22fd8-219">On the **Develop** tab, replace the run.csx code with the following:</span></span>

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting to now.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required to order by time as they may not be in the file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending to ServiceBus, use the payloadStream and set keeporiginal to true
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate the shared access signature on the container, setting the constraints directly on the signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> <span data-ttu-id="22fd8-220">Veillez à remplacer les variables du code précédent de façon à ce qu’elles pointent vers votre compte de stockage dans lequel les journaux de coffre de clés sont écrits, le Service Bus que vous avez créé précédemment, et le chemin d’accès spécifique des journaux de stockage du coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="22fd8-220">Make sure to replace the variables in the preceding code to point to your storage account where the key vault logs are written, the service bus you created earlier, and the specific path to the key vault storage logs.</span></span>
>
>

<span data-ttu-id="22fd8-221">La fonction récupère le dernier fichier journal du compte de stockage dans lequel les journaux de coffre de clés sont écrits, extrait les événements les plus récents de ce fichier et les place dans une file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="22fd8-221">The function picks up the latest log file from the storage account where the key vault logs are written, grabs the latest events from that file, and pushes them to a Service Bus queue.</span></span> <span data-ttu-id="22fd8-222">Étant donné qu’un même fichier peut comporter plusieurs événements, vous devez créer un fichier sync.txt que la fonction examine également pour déterminer l’horodatage du dernier événement récupéré.</span><span class="sxs-lookup"><span data-stu-id="22fd8-222">Since a single file could have multiple events, you should create a sync.txt file that the function also looks at to determine the time stamp of the last event that was picked up.</span></span> <span data-ttu-id="22fd8-223">Cela vous permet de vous assurer que le même événement n’est pas envoyé plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="22fd8-223">This ensures that you don't push the same event multiple times.</span></span> <span data-ttu-id="22fd8-224">Ce fichier sync.txt contient l’horodatage du dernier événement rencontré.</span><span class="sxs-lookup"><span data-stu-id="22fd8-224">This sync.txt file contains a timestamp for the last encountered event.</span></span> <span data-ttu-id="22fd8-225">Les journaux, une fois chargés, doivent être triés en fonction de l’horodatage pour s’assurer qu’ils sont classés correctement.</span><span class="sxs-lookup"><span data-stu-id="22fd8-225">The logs, when loaded, have to be sorted based on the timestamp to ensure they are ordered correctly.</span></span>

<span data-ttu-id="22fd8-226">Pour cette fonction, nous faisons référence à deux bibliothèques supplémentaires qui ne sont pas disponibles dans Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="22fd8-226">For this function, we reference a couple of additional libraries that are not available out of the box in Azure Functions.</span></span> <span data-ttu-id="22fd8-227">Pour pouvoir les inclure, Azure Functions doit le faire à l’aide de NuGet.</span><span class="sxs-lookup"><span data-stu-id="22fd8-227">To include these, we need Azure Functions to pull them using NuGet.</span></span> <span data-ttu-id="22fd8-228">Choisissez l’option **Afficher les fichiers**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-228">Choose the **View Files** option.</span></span>

![Option Afficher les fichiers](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

<span data-ttu-id="22fd8-230">Et ajoutez un fichier appelé project.json avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="22fd8-230">And add a file called project.json with following content:</span></span>

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
<span data-ttu-id="22fd8-231">Lorsque vous cliquez sur **Enregistrer**, Azure Functions télécharge les fichiers binaires nécessaires.</span><span class="sxs-lookup"><span data-stu-id="22fd8-231">Upon **Save**, Azure Functions will download the required binaries.</span></span>

<span data-ttu-id="22fd8-232">Basculez vers l’onglet **Intégration** et donnez un nom explicite au paramètre du minuteur à utiliser dans la fonction.</span><span class="sxs-lookup"><span data-stu-id="22fd8-232">Switch to the **Integrate** tab and give the timer parameter a meaningful name to use within the function.</span></span> <span data-ttu-id="22fd8-233">Dans le code précédent, le minuteur est appelé *myTimer*.</span><span class="sxs-lookup"><span data-stu-id="22fd8-233">In the preceding code, it expects the timer to be called *myTimer*.</span></span> <span data-ttu-id="22fd8-234">Spécifiez une [expression CRON](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) comme suit : 0 \* \* \* \* \* pour le minuteur qui activera l’exécution de la fonction une fois par minute.</span><span class="sxs-lookup"><span data-stu-id="22fd8-234">Specify a [CRON expression](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) as follows: 0 \* \* \* \* \* for the timer that will cause the function to run once a minute.</span></span>

<span data-ttu-id="22fd8-235">Dans ce même onglet **Intégration**, ajoutez une entrée de type **Stockage Blob Azure**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-235">On the same **Integrate** tab, add an input of the type **Azure Blob Storage**.</span></span> <span data-ttu-id="22fd8-236">Elle pointera vers le fichier sync.txt contenant l’horodatage du dernier événement examiné par la fonction.</span><span class="sxs-lookup"><span data-stu-id="22fd8-236">This will point to the sync.txt file that contains the timestamp of the last event looked at by the function.</span></span> <span data-ttu-id="22fd8-237">Elle sera disponible dans la fonction en tant que nom de paramètre.</span><span class="sxs-lookup"><span data-stu-id="22fd8-237">This will be available within the function by the parameter name.</span></span> <span data-ttu-id="22fd8-238">Dans le code précédent, l’entrée Azure Blob Storage attend le nom de paramètre *inputBlob*.</span><span class="sxs-lookup"><span data-stu-id="22fd8-238">In the preceding code, the Azure Blob Storage input expects the parameter name to be *inputBlob*.</span></span> <span data-ttu-id="22fd8-239">Choisissez le compte de stockage dans lequel se trouvera le fichier sync.txt (il peut s’agir du même compte de stockage ou d’un autre).</span><span class="sxs-lookup"><span data-stu-id="22fd8-239">Choose the storage account where the sync.txt file will reside (it could be the same or a different storage account).</span></span> <span data-ttu-id="22fd8-240">Dans le champ Chemin d’accès, indiquez le chemin d’accès au fichier au le format {container-name}/path/to/sync.txt.</span><span class="sxs-lookup"><span data-stu-id="22fd8-240">In the path field, provide the path where the file lives in the format {container-name}/path/to/sync.txt.</span></span>

<span data-ttu-id="22fd8-241">Ajoutez une sortie de type *Stockage Blob Azure*.</span><span class="sxs-lookup"><span data-stu-id="22fd8-241">Add an output of the type *Azure Blob Storage* output.</span></span> <span data-ttu-id="22fd8-242">Elle pointe vers le fichier sync.txt que vous avez défini dans l’entrée.</span><span class="sxs-lookup"><span data-stu-id="22fd8-242">This will point to the sync.txt file you defined in the input.</span></span> <span data-ttu-id="22fd8-243">Elle est utilisée par la fonction pour écrire l’horodatage du dernier événement examiné.</span><span class="sxs-lookup"><span data-stu-id="22fd8-243">This is used by the function to write the timestamp of the last event looked at.</span></span> <span data-ttu-id="22fd8-244">Dans le code précédent, le paramètre doit être appelé *outputBlob*.</span><span class="sxs-lookup"><span data-stu-id="22fd8-244">The preceding code expects this parameter to be called *outputBlob*.</span></span>

<span data-ttu-id="22fd8-245">À ce stade, la fonction est prête.</span><span class="sxs-lookup"><span data-stu-id="22fd8-245">At this point, the function is ready.</span></span> <span data-ttu-id="22fd8-246">N’oubliez pas de revenir à l’onglet **Développement** et d’enregistrer le code.</span><span class="sxs-lookup"><span data-stu-id="22fd8-246">Make sure to switch back to the **Develop** tab and save the code.</span></span> <span data-ttu-id="22fd8-247">Dans la fenêtre de résultat, recherchez d’éventuelles erreurs de compilation et corrigez-les.</span><span class="sxs-lookup"><span data-stu-id="22fd8-247">Check the output window for any compilation errors and correct them accordingly.</span></span> <span data-ttu-id="22fd8-248">S’il est compilé, le code doit maintenant vérifier les journaux du coffre de clés chaque minute et placer tout nouvel événement dans la file d’attente Service Bus définie.</span><span class="sxs-lookup"><span data-stu-id="22fd8-248">If the code compiles, then the code should now be checking the key vault logs every minute and pushing any new events onto the defined Service Bus queue.</span></span> <span data-ttu-id="22fd8-249">Vous devez voir des informations de journalisation dans la fenêtre du journal à chaque déclenchement de la fonction.</span><span class="sxs-lookup"><span data-stu-id="22fd8-249">You should see logging information write out to the log window every time the function is triggered.</span></span>

### <a name="azure-logic-app"></a><span data-ttu-id="22fd8-250">Application logique Azure</span><span class="sxs-lookup"><span data-stu-id="22fd8-250">Azure logic app</span></span>
<span data-ttu-id="22fd8-251">Vous devez ensuite créer une application logique Azure qui sélectionne les événements que la fonction place dans la file d’attente Service Bus, analyse le contenu et envoie un e-mail lorsqu’une condition est remplie.</span><span class="sxs-lookup"><span data-stu-id="22fd8-251">Next you must create an Azure logic app that picks up the events that the function is pushing to the Service Bus queue, parses the content, and sends an email based on a condition being matched.</span></span>

<span data-ttu-id="22fd8-252">[Créez une application logique](../logic-apps/logic-apps-create-a-logic-app.md) en accédant à **Nouveau > Application logique**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-252">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) by going to **New > Logic App**.</span></span>

<span data-ttu-id="22fd8-253">Une fois l’application logique créée, accédez à celle-ci et choisissez **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-253">Once the logic app is created, navigate to it and choose **edit**.</span></span> <span data-ttu-id="22fd8-254">Dans l’éditeur d’application logique, choisissez la **File d’attente Service Bus** et entrez vos informations d’identification Service Bus pour la connecter à la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="22fd8-254">Within the logic app editor, choose **Service Bus Queue** and enter your Service Bus credentials to connect it to the queue.</span></span>

![Service Bus d’application logique Azure](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

<span data-ttu-id="22fd8-256">Choisissez ensuite **Ajouter une condition**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-256">Next choose **Add a condition**.</span></span> <span data-ttu-id="22fd8-257">Dans la condition, basculez vers l’éditeur avancé, puis entrez le code suivant, en remplaçant l’APP_ID par le véritable APP_ID réel de votre application web :</span><span class="sxs-lookup"><span data-stu-id="22fd8-257">In the condition, switch to the advanced editor and enter the following code, replacing APP_ID with the actual APP_ID of your web app:</span></span>

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

<span data-ttu-id="22fd8-258">Cette expression retourne essentiellement la valeur **false** si *l’appid* de l’événement entrant (à savoir le corps du message Service Bus) ne correspond pas à *l’appid* de l’application.</span><span class="sxs-lookup"><span data-stu-id="22fd8-258">This expression essentially returns **false** if the *appid* from the incoming event (which is the body of the Service Bus message) is not the *appid* of the app.</span></span>

<span data-ttu-id="22fd8-259">Créez maintenant une action sous **Si non, ne rien faire**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-259">Now, create an action under **If no, do nothing**.</span></span>

![Choisir une action d’application logique Azure](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

<span data-ttu-id="22fd8-261">Pour l’action, choisissez **Office 365 - Envoyer un message électronique**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-261">For the action, choose **Office 365 - send email**.</span></span> <span data-ttu-id="22fd8-262">Renseignez les champs pour créer un e-mail à envoyer lorsque la condition définie retourne **false**.</span><span class="sxs-lookup"><span data-stu-id="22fd8-262">Fill out the fields to create an email to send when the defined condition returns **false**.</span></span> <span data-ttu-id="22fd8-263">Si vous n’avez pas Office 365, vous pouvez rechercher des alternatives pour parvenir aux mêmes résultats.</span><span class="sxs-lookup"><span data-stu-id="22fd8-263">If you do not have Office 365, you could look at alternatives to achieve the same results.</span></span>

<span data-ttu-id="22fd8-264">À ce stade, vous disposez d’un pipeline de bout en bout qui recherche les nouveaux journaux d’audit de coffre de clés une fois par minute.</span><span class="sxs-lookup"><span data-stu-id="22fd8-264">At this point, you have an end to end pipeline that looks for new key vault audit logs once a minute.</span></span> <span data-ttu-id="22fd8-265">Il place les nouveaux journaux qu’il trouve dans une file d’attente Service Bus.</span><span class="sxs-lookup"><span data-stu-id="22fd8-265">It pushes new logs it finds to a service bus queue.</span></span> <span data-ttu-id="22fd8-266">L’application logique est déclenchée lorsqu’un nouveau message arrive dans la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="22fd8-266">The logic app is triggered when a new message lands in the queue.</span></span> <span data-ttu-id="22fd8-267">Si *l’appid* au sein de l’événement ne correspond pas à l’ID d’application de l’application appelante, il envoie un e-mail.</span><span class="sxs-lookup"><span data-stu-id="22fd8-267">If the *appid* within the event does not match the app ID of the calling application, it sends an email.</span></span>
