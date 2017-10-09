---
title: aaaHow toouse hello Azure Mobile Apps SDK pour Android | Documents Microsoft
description: Comment toouse hello Azure Mobile Apps SDK pour Android
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a><span data-ttu-id="e66a6-103">Comment toouse hello Azure Mobile Apps SDK pour Android</span><span class="sxs-lookup"><span data-stu-id="e66a6-103">How toouse hello Azure Mobile Apps SDK for Android</span></span>

<span data-ttu-id="e66a6-104">Ce guide vous explique comment toouse hello client Android SDK pour applications mobiles tooimplement les scénarios courants, tels que :</span><span class="sxs-lookup"><span data-stu-id="e66a6-104">This guide shows you how toouse hello Android client SDK for Mobile Apps tooimplement common scenarios, such as:</span></span>

* <span data-ttu-id="e66a6-105">Interrogation des données (insertion, mise à jour et suppression).</span><span class="sxs-lookup"><span data-stu-id="e66a6-105">Querying for data (inserting, updating, and deleting).</span></span>
* <span data-ttu-id="e66a6-106">Authentification.</span><span class="sxs-lookup"><span data-stu-id="e66a6-106">Authentication.</span></span>
* <span data-ttu-id="e66a6-107">Gestion des erreurs.</span><span class="sxs-lookup"><span data-stu-id="e66a6-107">Handling errors.</span></span>
* <span data-ttu-id="e66a6-108">Personnalisation de client de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-108">Customizing hello client.</span></span>

<span data-ttu-id="e66a6-109">Ce guide se concentre sur hello côté client SDK Android.</span><span class="sxs-lookup"><span data-stu-id="e66a6-109">This guide focuses on hello client-side Android SDK.</span></span>  <span data-ttu-id="e66a6-110">toolearn savoir plus sur hello des kits de développement logiciel côté serveur pour les applications mobiles, consultez [fonctionne avec le serveur principal .NET SDK] [ 10] ou [comment toouse hello Node.js principal SDK] [ 11].</span><span class="sxs-lookup"><span data-stu-id="e66a6-110">toolearn more about hello server-side SDKs for Mobile Apps, see [Work with .NET backend SDK][10] or [How toouse hello Node.js backend SDK][11].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="e66a6-111">Documentation de référence</span><span class="sxs-lookup"><span data-stu-id="e66a6-111">Reference Documentation</span></span>

<span data-ttu-id="e66a6-112">Vous pouvez trouver hello [référence de l’API de Javadocs] [ 12] pour la bibliothèque de client Android hello sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="e66a6-112">You can find hello [Javadocs API reference][12] for hello Android client library on GitHub.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="e66a6-113">Plateformes prises en charge</span><span class="sxs-lookup"><span data-stu-id="e66a6-113">Supported Platforms</span></span>

<span data-ttu-id="e66a6-114">Hello Azure Mobile Apps SDK pour Android prend en charge les niveaux d’API 19 et 24 (KitKat via la commande) pour le téléphone et tablette facteurs de forme.</span><span class="sxs-lookup"><span data-stu-id="e66a6-114">hello Azure Mobile Apps SDK for Android supports API levels 19 through 24 (KitKat through Nougat) for phone and tablet form factors.</span></span>  <span data-ttu-id="e66a6-115">L’authentification, utilise en particulier, d’informations d’identification de toogather approche commune web framework.</span><span class="sxs-lookup"><span data-stu-id="e66a6-115">Authentication, in particular, utilizes a common web framework approach toogather credentials.</span></span>  <span data-ttu-id="e66a6-116">L’authentification de flux serveur ne fonctionne pas avec les appareils compacts comme les montres.</span><span class="sxs-lookup"><span data-stu-id="e66a6-116">Server-flow authentication does not work with small form factor devices such as watches.</span></span>

## <a name="setup-and-prerequisites"></a><span data-ttu-id="e66a6-117">Configuration et conditions préalables</span><span class="sxs-lookup"><span data-stu-id="e66a6-117">Setup and Prerequisites</span></span>

<span data-ttu-id="e66a6-118">Hello complète [démarrage rapide des applications mobiles](app-service-mobile-android-get-started.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e66a6-118">Complete hello [Mobile Apps quickstart](app-service-mobile-android-get-started.md) tutorial.</span></span>  <span data-ttu-id="e66a6-119">Cette tâche garantit que toutes les conditions préalables au développement d’Azure Mobile Apps ont été remplies.</span><span class="sxs-lookup"><span data-stu-id="e66a6-119">This task ensures all pre-requisites for developing Azure Mobile Apps have been met.</span></span>  <span data-ttu-id="e66a6-120">Hello démarrage rapide vous aide également à configurer votre compte et de créer votre première principal de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="e66a6-120">hello Quickstart also helps you configure your account and create your first Mobile App backend.</span></span>

<span data-ttu-id="e66a6-121">Si vous décidez de toocomplete pas le didacticiel de démarrage rapide hello, procédez hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="e66a6-121">If you decide not toocomplete hello Quickstart tutorial, complete hello following tasks:</span></span>

* <span data-ttu-id="e66a6-122">[créer un service principal de l’application Mobile] [ 13] toouse avec votre application Android.</span><span class="sxs-lookup"><span data-stu-id="e66a6-122">[create a Mobile App backend][13] toouse with your Android app.</span></span>
* <span data-ttu-id="e66a6-123">Dans Android Studio, [mise à jour hello Gradle les fichiers de build](#gradle-build).</span><span class="sxs-lookup"><span data-stu-id="e66a6-123">In Android Studio, [update hello Gradle build files](#gradle-build).</span></span>
* <span data-ttu-id="e66a6-124">[activer les autorisations Internet](#enable-internet).</span><span class="sxs-lookup"><span data-stu-id="e66a6-124">[Enable internet permission](#enable-internet).</span></span>

### <span data-ttu-id="e66a6-125"><a name="gradle-build"></a>Hello Gradle générer fichier de mise à jour</span><span class="sxs-lookup"><span data-stu-id="e66a6-125"><a name="gradle-build"></a>Update hello Gradle build file</span></span>

<span data-ttu-id="e66a6-126">Modifiez les deux fichiers **build.gradle** :</span><span class="sxs-lookup"><span data-stu-id="e66a6-126">Change both **build.gradle** files:</span></span>

1. <span data-ttu-id="e66a6-127">Ajouter ce code toohello *projet* niveau **build.gradle** fichier hello *buildscript* balise :</span><span class="sxs-lookup"><span data-stu-id="e66a6-127">Add this code toohello *Project* level **build.gradle** file inside hello *buildscript* tag:</span></span>

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. <span data-ttu-id="e66a6-128">Ajouter ce code toohello *Module application* niveau **build.gradle** fichier hello *dépendances* balise :</span><span class="sxs-lookup"><span data-stu-id="e66a6-128">Add this code toohello *Module app* level **build.gradle** file inside hello *dependencies* tag:</span></span>

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    <span data-ttu-id="e66a6-129">Actuellement la version la plus récente hello est 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="e66a6-129">Currently hello latest version is 3.3.0.</span></span> <span data-ttu-id="e66a6-130">les versions Hello pris en charge sont répertoriées [sur bintray][14].</span><span class="sxs-lookup"><span data-stu-id="e66a6-130">hello supported versions are listed [on bintray][14].</span></span>

### <span data-ttu-id="e66a6-131"><a name="enable-internet"></a>activer les autorisations Internet.</span><span class="sxs-lookup"><span data-stu-id="e66a6-131"><a name="enable-internet"></a>Enable internet permission</span></span>

<span data-ttu-id="e66a6-132">tooaccess Azure, votre application doit avoir d’autorisations INTERNET hello activée.</span><span class="sxs-lookup"><span data-stu-id="e66a6-132">tooaccess Azure, your app must have hello INTERNET permission enabled.</span></span> <span data-ttu-id="e66a6-133">S’il n’est pas déjà activé, ajouter hello suivant la ligne de code tooyour **AndroidManifest.xml** fichier :</span><span class="sxs-lookup"><span data-stu-id="e66a6-133">If it's not already enabled, add hello following line of code tooyour **AndroidManifest.xml** file:</span></span>

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a><span data-ttu-id="e66a6-134">Créer une connexion cliente</span><span class="sxs-lookup"><span data-stu-id="e66a6-134">Create a Client Connection</span></span>

<span data-ttu-id="e66a6-135">Les applications mobiles Azure fournit quatre fonctions tooyour des applications mobiles :</span><span class="sxs-lookup"><span data-stu-id="e66a6-135">Azure Mobile Apps provides four functions tooyour mobile application:</span></span>

* <span data-ttu-id="e66a6-136">Accès aux données et synchronisation hors connexion avec un service Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="e66a6-136">Data Access and Offline Synchronization with an Azure Mobile Apps Service.</span></span>
* <span data-ttu-id="e66a6-137">Appeler les API personnalisées écrites avec hello Azure Mobile Apps Server SDK.</span><span class="sxs-lookup"><span data-stu-id="e66a6-137">Call Custom APIs written with hello Azure Mobile Apps Server SDK.</span></span>
* <span data-ttu-id="e66a6-138">Authentification avec l’authentification et l’autorisation Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="e66a6-138">Authentication with Azure App Service Authentication and Authorization.</span></span>
* <span data-ttu-id="e66a6-139">Inscription de notifications Push avec Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="e66a6-139">Push Notification Registration with Notification Hubs.</span></span>

<span data-ttu-id="e66a6-140">Pour chacune de ces fonctions, vous devez créer un objet `MobileServiceClient` au préalable.</span><span class="sxs-lookup"><span data-stu-id="e66a6-140">Each of these functions first requires that you create a `MobileServiceClient` object.</span></span>  <span data-ttu-id="e66a6-141">Seul un objet `MobileServiceClient` doit être créé au sein de votre client mobile (autrement dit, il doit être un modèle de Singleton).</span><span class="sxs-lookup"><span data-stu-id="e66a6-141">Only one `MobileServiceClient` object should be created within your mobile client (that is, it should be a Singleton pattern).</span></span>  <span data-ttu-id="e66a6-142">toocreate un `MobileServiceClient` objet :</span><span class="sxs-lookup"><span data-stu-id="e66a6-142">toocreate a `MobileServiceClient` object:</span></span>

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

<span data-ttu-id="e66a6-143">Hello `<MobileAppUrl>` est une chaîne ou un objet de l’URL qui pointe backend mobile de tooyour.</span><span class="sxs-lookup"><span data-stu-id="e66a6-143">hello `<MobileAppUrl>` is either a string or a URL object that points tooyour mobile backend.</span></span>  <span data-ttu-id="e66a6-144">Si vous utilisez Azure App Service toohost votre serveur principal mobile, puis assurez-vous utiliser hello sécurisé `https://` version de l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-144">If you are using Azure App Service toohost your mobile backend, then ensure you use hello secure `https://` version of hello URL.</span></span>

<span data-ttu-id="e66a6-145">client de Hello requiert également accès toohello activité ou contexte - hello `this` paramètre dans l’exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-145">hello client also requires access toohello Activity or Context - hello `this` parameter in hello example.</span></span>  <span data-ttu-id="e66a6-146">Hello MobileServiceClient construction doit se produire dans hello `onCreate()` méthode Hello activité référencée Bonjour `AndroidManifest.xml` fichier.</span><span class="sxs-lookup"><span data-stu-id="e66a6-146">hello MobileServiceClient construction should happen within hello `onCreate()` method of hello Activity referenced in hello `AndroidManifest.xml` file.</span></span>

<span data-ttu-id="e66a6-147">Nous vous recommandons d’extraire la communication du serveur dans sa propre classe (modèle singleton).</span><span class="sxs-lookup"><span data-stu-id="e66a6-147">As a best practice, you should abstract server communication into its own (singleton-pattern) class.</span></span>  <span data-ttu-id="e66a6-148">Dans ce cas, vous devez passer hello activité au sein de hello constructeur tooappropriately configurer le service de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-148">In this case, you should pass hello Activity within hello constructor tooappropriately configure hello service.</span></span>  <span data-ttu-id="e66a6-149">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e66a6-149">For example:</span></span>

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

<span data-ttu-id="e66a6-150">Vous pouvez maintenant appeler `AzureServiceAdapter.Initialize(this);` Bonjour `onCreate()` méthode de votre activité principale.</span><span class="sxs-lookup"><span data-stu-id="e66a6-150">You can now call `AzureServiceAdapter.Initialize(this);` in hello `onCreate()` method of your main activity.</span></span>  <span data-ttu-id="e66a6-151">Toutes les autres méthodes nécessitant le client d’accès toohello utilisent `AzureServiceAdapter.getInstance();` tooobtain une carte de service référence toohello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-151">Any other methods needing access toohello client use `AzureServiceAdapter.getInstance();` tooobtain a reference toohello service adapter.</span></span>

## <a name="data-operations"></a><span data-ttu-id="e66a6-152">Opérations de données</span><span class="sxs-lookup"><span data-stu-id="e66a6-152">Data Operations</span></span>

<span data-ttu-id="e66a6-153">core Hello Hello Azure Mobile Apps SDK est toodata d’accès tooprovide stockée dans SQL Azure sur le serveur principal de l’application Mobile hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-153">hello core of hello Azure Mobile Apps SDK is tooprovide access toodata stored within SQL Azure on hello Mobile App backend.</span></span>  <span data-ttu-id="e66a6-154">Vous pouvez accéder à ces données à l’aide de classes fortement typées (recommandé) ou de requêtes non typées (déconseillé).</span><span class="sxs-lookup"><span data-stu-id="e66a6-154">You can access this data using strongly typed classes (preferred) or untyped queries (not recommended).</span></span>  <span data-ttu-id="e66a6-155">bloc Hello de cette section porte sur l’utilisation des classes fortement typées.</span><span class="sxs-lookup"><span data-stu-id="e66a6-155">hello bulk of this section deals with using strongly typed classes.</span></span>

### <a name="define-client-data-classes"></a><span data-ttu-id="e66a6-156">Définir des classes de données client</span><span class="sxs-lookup"><span data-stu-id="e66a6-156">Define client data classes</span></span>

<span data-ttu-id="e66a6-157">tooaccess des données à partir des tables de SQL Azure, définir des classes de données de client qui correspondent toohello des tables dans le service principal de l’application Mobile hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-157">tooaccess data from SQL Azure tables, define client data classes that correspond toohello tables in hello Mobile App backend.</span></span> <span data-ttu-id="e66a6-158">Exemples de cette rubrique supposent une table nommée **MyDataTable**, qui a hello suivant des colonnes :</span><span class="sxs-lookup"><span data-stu-id="e66a6-158">Examples in this topic assume a table named **MyDataTable**, which has hello following columns:</span></span>

* <span data-ttu-id="e66a6-159">id</span><span class="sxs-lookup"><span data-stu-id="e66a6-159">id</span></span>
* <span data-ttu-id="e66a6-160">text</span><span class="sxs-lookup"><span data-stu-id="e66a6-160">text</span></span>
* <span data-ttu-id="e66a6-161">terminé</span><span class="sxs-lookup"><span data-stu-id="e66a6-161">complete</span></span>

<span data-ttu-id="e66a6-162">Hello correspondant objet côté client typé réside dans un fichier appelé **MyDataTable.java**:</span><span class="sxs-lookup"><span data-stu-id="e66a6-162">hello corresponding typed client-side object resides in a file called **MyDataTable.java**:</span></span>

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

<span data-ttu-id="e66a6-163">Incluez des méthodes getter et setter pour chaque champ que vous ajoutez.</span><span class="sxs-lookup"><span data-stu-id="e66a6-163">Add getter and setter methods for each field that you add.</span></span>  <span data-ttu-id="e66a6-164">Si votre table SQL Azure contient plus de colonnes, vous devez ajouter la classe toothis champs correspondante de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-164">If your SQL Azure table contains more columns, you would add hello corresponding fields toothis class.</span></span>  <span data-ttu-id="e66a6-165">Par exemple, si hello DTO (objet de transfert de données) a une colonne d’entiers priorité, puis vous pouvez ajouter ce champ, ainsi que ses méthodes getter et setter :</span><span class="sxs-lookup"><span data-stu-id="e66a6-165">For example, if hello DTO (data transfer object) had an integer Priority column, then you might add this field, along with its getter and setter methods:</span></span>

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

<span data-ttu-id="e66a6-166">toolearn toocreate des tables supplémentaires dans votre service principal Mobile Apps, voir [Comment : définir un contrôleur de table] [ 15] (principal .NET) ou [définissent des Tables à l’aide d’un schéma dynamique] [ 16] (Node.js principal).</span><span class="sxs-lookup"><span data-stu-id="e66a6-166">toolearn how toocreate additional tables in your Mobile Apps backend, see [How to: Define a table controller][15] (.NET backend) or [Define Tables using a Dynamic Schema][16] (Node.js backend).</span></span>

<span data-ttu-id="e66a6-167">Une table de serveur principal les applications mobiles Azure définit cinq champs spéciaux, dont quatre sont tooclients disponibles :</span><span class="sxs-lookup"><span data-stu-id="e66a6-167">An Azure Mobile Apps backend table defines five special fields, four of which are available tooclients:</span></span>

* <span data-ttu-id="e66a6-168">`String id`: hello ID global unique pour l’enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-168">`String id`: hello globally unique ID for hello record.</span></span>  <span data-ttu-id="e66a6-169">Comme meilleure pratique, rendre hello id hello chaîne représentant un [UUID] [ 17] objet.</span><span class="sxs-lookup"><span data-stu-id="e66a6-169">As a best practice, make hello id hello String representation of a [UUID][17] object.</span></span>
* <span data-ttu-id="e66a6-170">`DateTimeOffset updatedAt`: hello date/heure de dernière mise à jour de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-170">`DateTimeOffset updatedAt`: hello date/time of hello last update.</span></span>  <span data-ttu-id="e66a6-171">champ d’updatedAt Hello est définie par le serveur de hello et ne doit jamais être définie par votre code client.</span><span class="sxs-lookup"><span data-stu-id="e66a6-171">hello updatedAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="e66a6-172">`DateTimeOffset createdAt`: hello date/heure de cet objet hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="e66a6-172">`DateTimeOffset createdAt`: hello date/time that hello object was created.</span></span>  <span data-ttu-id="e66a6-173">champ de créédans Hello est définie par le serveur de hello et ne doit jamais être définie par votre code client.</span><span class="sxs-lookup"><span data-stu-id="e66a6-173">hello createdAt field is set by hello server and should never be set by your client code.</span></span>
* <span data-ttu-id="e66a6-174">`byte[] version`: Version de hello normalement représenté sous forme de chaîne, est également définie par le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-174">`byte[] version`: Normally represented as a string, hello version is also set by hello server.</span></span>
* <span data-ttu-id="e66a6-175">`boolean deleted`: Indique que l’enregistrement de hello a été supprimé mais ne pas encore été purgé.</span><span class="sxs-lookup"><span data-stu-id="e66a6-175">`boolean deleted`: Indicates that hello record has been deleted but not purged yet.</span></span>  <span data-ttu-id="e66a6-176">N’utilisez pas `deleted` en tant que propriété dans votre classe.</span><span class="sxs-lookup"><span data-stu-id="e66a6-176">Do not use `deleted` as a property in your class.</span></span>

<span data-ttu-id="e66a6-177">Hello `id` champ est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="e66a6-177">hello `id` field is required.</span></span>  <span data-ttu-id="e66a6-178">Hello `updatedAt` champ et `version` sont utilisés pour la synchronisation hors connexion (pour la résolution de conflit et de synchronisation incrémentielle respectivement).</span><span class="sxs-lookup"><span data-stu-id="e66a6-178">hello `updatedAt` field and `version` field are used for offline synchronization (for incremental sync and conflict resolution respectively).</span></span>  <span data-ttu-id="e66a6-179">Hello `createdAt` champ est un champ de référence et n’est pas utilisé par le client de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-179">hello `createdAt` field is a reference field and is not used by hello client.</span></span>  <span data-ttu-id="e66a6-180">les noms de Hello sont des noms de « entre simultanée » des propriétés de hello et ne sont pas réglables.</span><span class="sxs-lookup"><span data-stu-id="e66a6-180">hello names are "across-the-wire" names of hello properties and are not adjustable.</span></span>  <span data-ttu-id="e66a6-181">Toutefois, vous pouvez créer un mappage entre les hello noms « entre simultanée » à l’aide de hello [gson] [ 3] bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="e66a6-181">However, you can create a mapping between your object and hello "across-the-wire" names using hello [gson][3] library.</span></span>  <span data-ttu-id="e66a6-182">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e66a6-182">For example:</span></span>

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a><span data-ttu-id="e66a6-183">Créer une référence de table</span><span class="sxs-lookup"><span data-stu-id="e66a6-183">Create a Table Reference</span></span>

<span data-ttu-id="e66a6-184">tooaccess une table, commencez par créer un [MobileServiceTable] [ 8] objet en appelant hello **getTable** méthode sur hello [MobileServiceClient][9].</span><span class="sxs-lookup"><span data-stu-id="e66a6-184">tooaccess a table, first create a [MobileServiceTable][8] object by calling hello **getTable** method on hello [MobileServiceClient][9].</span></span>  <span data-ttu-id="e66a6-185">Cette méthode comporte deux surcharges :</span><span class="sxs-lookup"><span data-stu-id="e66a6-185">This method has two overloads:</span></span>

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

<span data-ttu-id="e66a6-186">Bonjour, suivant le code, **mClient** est un objet de MobileServiceClient tooyour référence.</span><span class="sxs-lookup"><span data-stu-id="e66a6-186">In hello following code, **mClient** is a reference tooyour MobileServiceClient object.</span></span>  <span data-ttu-id="e66a6-187">la première surcharge de Hello est utilisée où nom de la classe hello et le nom de la table hello même hello et hello un sert Bonjour démarrage rapide :</span><span class="sxs-lookup"><span data-stu-id="e66a6-187">hello first overload is used where hello class name and hello table name are hello same, and is hello one used in hello Quickstart:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

<span data-ttu-id="e66a6-188">Hello deuxième surcharge est utilisée lorsque le nom de la table hello est différent du nom de classe hello : hello premier paramètre est nom de la table hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-188">hello second overload is used when hello table name is different from hello class name: hello first parameter is hello table name.</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <span data-ttu-id="e66a6-189"><a name="query"></a>Interroger une table de serveur principal</span><span class="sxs-lookup"><span data-stu-id="e66a6-189"><a name="query"></a>Query a Backend Table</span></span>

<span data-ttu-id="e66a6-190">Commencez par obtenir une référence de table.</span><span class="sxs-lookup"><span data-stu-id="e66a6-190">First, obtain a table reference.</span></span>  <span data-ttu-id="e66a6-191">Ensuite, exécutez une requête sur la référence de table hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-191">Then execute a query on hello table reference.</span></span>  <span data-ttu-id="e66a6-192">Une requête est une combinaison des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e66a6-192">A query is any combination of:</span></span>

* <span data-ttu-id="e66a6-193">Une [clause de filtre](#filtering) `.where()`.</span><span class="sxs-lookup"><span data-stu-id="e66a6-193">A `.where()` [filter clause](#filtering).</span></span>
* <span data-ttu-id="e66a6-194">Une [clause de classement](#sorting) `.orderBy()`.</span><span class="sxs-lookup"><span data-stu-id="e66a6-194">An `.orderBy()` [ordering clause](#sorting).</span></span>
* <span data-ttu-id="e66a6-195">Une [clause de sélection de champ](#selection) `.select()`.</span><span class="sxs-lookup"><span data-stu-id="e66a6-195">A `.select()` [field selection clause](#selection).</span></span>
* <span data-ttu-id="e66a6-196">Un élément `.skip()` et `.top()` pour les [résultats paginés](#paging).</span><span class="sxs-lookup"><span data-stu-id="e66a6-196">A `.skip()` and `.top()` for [paged results](#paging).</span></span>

<span data-ttu-id="e66a6-197">les clauses Hello doivent être présentés dans hello précédant l’ordre.</span><span class="sxs-lookup"><span data-stu-id="e66a6-197">hello clauses must be presented in hello preceding order.</span></span>

### <span data-ttu-id="e66a6-198"><a name="filter"></a> Filtrage des résultats</span><span class="sxs-lookup"><span data-stu-id="e66a6-198"><a name="filter"></a> Filtering Results</span></span>

<span data-ttu-id="e66a6-199">Hello la forme générale d’une requête est :</span><span class="sxs-lookup"><span data-stu-id="e66a6-199">hello general form of a query is:</span></span>

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

<span data-ttu-id="e66a6-200">Hello exemple précédent retourne tous les résultats (haut toohello taille de page maximale définie par le serveur de hello).</span><span class="sxs-lookup"><span data-stu-id="e66a6-200">hello preceding example returns all results (up toohello maximum page size set by hello server).</span></span>  <span data-ttu-id="e66a6-201">Hello `.execute()` méthode s’exécute les requêtes hello sur hello principal.</span><span class="sxs-lookup"><span data-stu-id="e66a6-201">hello `.execute()` method executes hello query on hello backend.</span></span>  <span data-ttu-id="e66a6-202">requête Hello est converti tooan [OData v3] [ 19] requête avant transmission toohello Mobile Apps principal.</span><span class="sxs-lookup"><span data-stu-id="e66a6-202">hello query is converted tooan [OData v3][19] query before transmission toohello Mobile Apps backend.</span></span>  <span data-ttu-id="e66a6-203">À la réception, principal des applications mobiles hello convertit les requêtes hello dans une instruction SQL avant de l’exécuter sur l’instance de SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-203">On receipt, hello Mobile Apps backend converts hello query into an SQL statement before executing it on hello SQL Azure instance.</span></span>  <span data-ttu-id="e66a6-204">Étant donné que l’activité réseau prend du temps, hello `.execute()` méthode retourne un [ `ListenableFuture<E>` ] [ 18].</span><span class="sxs-lookup"><span data-stu-id="e66a6-204">Since network activity takes some time, hello `.execute()` method returns a [`ListenableFuture<E>`][18].</span></span>

### <span data-ttu-id="e66a6-205"><a name="filtering"></a>Filtrer les données renvoyées</span><span class="sxs-lookup"><span data-stu-id="e66a6-205"><a name="filtering"></a>Filter returned data</span></span>

<span data-ttu-id="e66a6-206">Hello après l’exécution de la requête retourne tous les éléments à partir de hello **ToDoItem** table dans laquelle **complète** est égal à **false**.</span><span class="sxs-lookup"><span data-stu-id="e66a6-206">hello following query execution returns all items from hello **ToDoItem** table where **complete** equals **false**.</span></span>

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

<span data-ttu-id="e66a6-207">**mToDoTable** est hello toohello service mobile table de référence que nous avons créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="e66a6-207">**mToDoTable** is hello reference toohello mobile service table that we created previously.</span></span>

<span data-ttu-id="e66a6-208">Définir un filtre à l’aide de hello **où** appel de méthode sur la référence de table hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-208">Define a filter using hello **where** method call on hello table reference.</span></span> <span data-ttu-id="e66a6-209">Hello **où** méthode est suivie par une **champ** méthode suivie par une méthode qui spécifie le prédicat de logique hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-209">hello **where** method is followed by a **field** method followed by a method that specifies hello logical predicate.</span></span> <span data-ttu-id="e66a6-210">Méthodes de prédicat possibles : **eq** (égal à), **ne** (différent de), **gt** (supérieur à), **ge** (supérieur ou égal à), **lt** (inférieur à), **le** (inférieur ou égal à).</span><span class="sxs-lookup"><span data-stu-id="e66a6-210">Possible predicate methods include **eq** (equals), **ne** (not equal), **gt** (greater than), **ge** (greater than or equal to), **lt** (less than), **le** (less than or equal to).</span></span> <span data-ttu-id="e66a6-211">Ces méthodes vous permettent de comparer le nombre et les valeurs de toospecific des champs de chaîne.</span><span class="sxs-lookup"><span data-stu-id="e66a6-211">These methods let you compare number and string fields toospecific values.</span></span>

<span data-ttu-id="e66a6-212">Vous pouvez activer des filtres sur les dates.</span><span class="sxs-lookup"><span data-stu-id="e66a6-212">You can filter on dates.</span></span> <span data-ttu-id="e66a6-213">Hello méthodes suivantes vous permettent de comparer le champ de date complète hello ou des parties de date de hello : **année**, **mois**, **jour**, **heure**, **minute**, et **deuxième**.</span><span class="sxs-lookup"><span data-stu-id="e66a6-213">hello following methods let you compare hello entire date field or parts of hello date: **year**, **month**, **day**, **hour**, **minute**, and **second**.</span></span> <span data-ttu-id="e66a6-214">Hello exemple suivant ajoute un filtre pour les éléments dont *date d’échéance* est égal à 2013.</span><span class="sxs-lookup"><span data-stu-id="e66a6-214">hello following example adds a filter for items whose *due date* equals 2013.</span></span>

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

<span data-ttu-id="e66a6-215">Hello méthodes suivantes prennent en charge des filtres complexes sur des champs de chaîne : **startsWith**, **endsWith**, **concat**, **sous-chaîne**, **indexOf**, **remplacer**, **toLower**, **toUpper**, **trim**, et  **longueur**.</span><span class="sxs-lookup"><span data-stu-id="e66a6-215">hello following methods support complex filters on string fields: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **replace**, **toLower**, **toUpper**, **trim**, and **length**.</span></span> <span data-ttu-id="e66a6-216">Hello suivant l’exemple de filtre de lignes de la table où hello *texte* colonne commence par « PRI0 ».</span><span class="sxs-lookup"><span data-stu-id="e66a6-216">hello following example filters for table rows where hello *text* column starts with "PRI0."</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="e66a6-217">Hello suivant les méthodes d’opérateur est pris en charge sur les champs numériques : **ajouter**, **sub**, **mul**, **div**, **mod**, **floor**, **plafond**, et **arrondir**.</span><span class="sxs-lookup"><span data-stu-id="e66a6-217">hello following operator methods are supported on number fields: **add**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, and **round**.</span></span> <span data-ttu-id="e66a6-218">Hello suivant l’exemple de filtre de lignes de la table où hello **durée** est un nombre pair.</span><span class="sxs-lookup"><span data-stu-id="e66a6-218">hello following example filters for table rows where hello **duration** is an even number.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

<span data-ttu-id="e66a6-219">Vous pouvez combiner les prédicats avec les méthodes logiques **and**, **or** et **not**.</span><span class="sxs-lookup"><span data-stu-id="e66a6-219">You can combine predicates with these logical methods: **and**, **or** and **not**.</span></span> <span data-ttu-id="e66a6-220">Bonjour à l’exemple suivant combine deux Hello précédant les exemples.</span><span class="sxs-lookup"><span data-stu-id="e66a6-220">hello following example combines two of hello preceding examples.</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

<span data-ttu-id="e66a6-221">Regrouper et imbriquer des opérateurs logiques :</span><span class="sxs-lookup"><span data-stu-id="e66a6-221">Group and nest logical operators:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

<span data-ttu-id="e66a6-222">Pour plus d’informations détaillées de discussion et des exemples de filtrage, consultez [exploration richesse hello du modèle de requête cliente Android hello][20].</span><span class="sxs-lookup"><span data-stu-id="e66a6-222">For more detailed discussion and examples of filtering, see [Exploring hello richness of hello Android client query model][20].</span></span>

### <span data-ttu-id="e66a6-223"><a name="sorting"></a>Trier les données renvoyées</span><span class="sxs-lookup"><span data-stu-id="e66a6-223"><a name="sorting"></a>Sort returned data</span></span>

<span data-ttu-id="e66a6-224">Hello de code suivant retourne tous les éléments d’une table de **ToDoItems** triée par ordre croissant par hello *texte* champ.</span><span class="sxs-lookup"><span data-stu-id="e66a6-224">hello following code returns all items from a table of **ToDoItems** sorted ascending by hello *text* field.</span></span> <span data-ttu-id="e66a6-225">*mToDoTable* est hello toohello principal table de référence que vous avez créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="e66a6-225">*mToDoTable* is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

<span data-ttu-id="e66a6-226">Hello du premier paramètre de hello **orderBy** méthode est un nom de toohello égal de chaîne du champ hello sur le toosort.</span><span class="sxs-lookup"><span data-stu-id="e66a6-226">hello first parameter of hello **orderBy** method is a string equal toohello name of hello field on which toosort.</span></span> <span data-ttu-id="e66a6-227">deuxième paramètre de Hello utilise hello **QueryOrder** toospecify d’énumération si toosort par ordre croissant ou décroissant.</span><span class="sxs-lookup"><span data-stu-id="e66a6-227">hello second parameter uses hello **QueryOrder** enumeration toospecify whether toosort ascending or descending.</span></span>  <span data-ttu-id="e66a6-228">Si vous filtrez à l’aide de hello ***où*** (méthode), hello ***où*** méthode doit être appelée avant hello ***orderBy*** (méthode).</span><span class="sxs-lookup"><span data-stu-id="e66a6-228">If you are filtering using hello ***where*** method, hello ***where*** method must be invoked before hello ***orderBy*** method.</span></span>

### <span data-ttu-id="e66a6-229"><a name="selection"></a>Sélectionner des colonnes spécifiques</span><span class="sxs-lookup"><span data-stu-id="e66a6-229"><a name="selection"></a>Select specific columns</span></span>

<span data-ttu-id="e66a6-230">Hello de code suivant illustre comment tooreturn tous les éléments d’une table de **ToDoItems**, mais n’affiche que hello **complète** et **texte** champs.</span><span class="sxs-lookup"><span data-stu-id="e66a6-230">hello following code illustrates how tooreturn all items from a table of **ToDoItems**, but only displays hello **complete** and **text** fields.</span></span> <span data-ttu-id="e66a6-231">**mToDoTable** est hello toohello principal table de référence que nous avons créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="e66a6-231">**mToDoTable** is hello reference toohello backend table that we created previously.</span></span>

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

<span data-ttu-id="e66a6-232">fonction de Hello paramètres toohello select sont des noms de chaîne hello hello du colonnes de table que vous souhaitez tooreturn.</span><span class="sxs-lookup"><span data-stu-id="e66a6-232">hello parameters toohello select function are hello string names of hello table's columns that you want tooreturn.</span></span>  <span data-ttu-id="e66a6-233">Hello **sélectionnez** méthode doit toofollow des méthodes, telles que **où** et **orderBy**.</span><span class="sxs-lookup"><span data-stu-id="e66a6-233">hello **select** method needs toofollow methods like **where** and **orderBy**.</span></span> <span data-ttu-id="e66a6-234">Elle peut être suivie de méthodes de pagination telles que **skip** et **top**.</span><span class="sxs-lookup"><span data-stu-id="e66a6-234">It can be followed by paging methods like **skip** and **top**.</span></span>

### <span data-ttu-id="e66a6-235"><a name="paging"></a>Renvoyer les données de pages</span><span class="sxs-lookup"><span data-stu-id="e66a6-235"><a name="paging"></a>Return data in pages</span></span>

<span data-ttu-id="e66a6-236">Les données sont **TOUJOURS** renvoyées dans les pages.</span><span class="sxs-lookup"><span data-stu-id="e66a6-236">Data is **ALWAYS** returned in pages.</span></span>  <span data-ttu-id="e66a6-237">nombre maximal de Hello d’enregistrements renvoyés est définie par le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-237">hello maximum number of records returned is set by hello server.</span></span>  <span data-ttu-id="e66a6-238">Si le client de hello demande plus d’enregistrements, serveur de hello retourne le nombre maximal de hello d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="e66a6-238">If hello client requests more records, then hello server returns hello maximum number of records.</span></span>  <span data-ttu-id="e66a6-239">Par défaut, la taille de page maximale de hello sur le serveur hello est 50 enregistrements.</span><span class="sxs-lookup"><span data-stu-id="e66a6-239">By default, hello maximum page size on hello server is 50 records.</span></span>

<span data-ttu-id="e66a6-240">Hello premier exemple montre comment tooselect hello supérieur cinq éléments à partir d’une table.</span><span class="sxs-lookup"><span data-stu-id="e66a6-240">hello first example shows how tooselect hello top five items from a table.</span></span> <span data-ttu-id="e66a6-241">requête de Hello retourne des éléments de hello dans une table de **ToDoItems**.</span><span class="sxs-lookup"><span data-stu-id="e66a6-241">hello query returns hello items from a table of **ToDoItems**.</span></span> <span data-ttu-id="e66a6-242">**mToDoTable** est hello toohello principal table de référence que vous avez créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="e66a6-242">**mToDoTable** is hello reference toohello backend table that you created previously:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

<span data-ttu-id="e66a6-243">Voici une requête qu’ignore hello cinq premiers éléments, puis retourne hello cinq suivant :</span><span class="sxs-lookup"><span data-stu-id="e66a6-243">Here's a query that skips hello first five items, and then returns hello next five:</span></span>

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

<span data-ttu-id="e66a6-244">Si vous le souhaitez tooget tous les enregistrements dans une table, implémentent tooiterate du code sur toutes les pages :</span><span class="sxs-lookup"><span data-stu-id="e66a6-244">If you wish tooget all records in a table, implement code tooiterate over all pages:</span></span>

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

<span data-ttu-id="e66a6-245">Une demande pour tous les enregistrements à l’aide de cette méthode crée un minimum de deux requêtes toohello Mobile Apps principal.</span><span class="sxs-lookup"><span data-stu-id="e66a6-245">A request for all records using this method creates a minimum of two requests toohello Mobile Apps backend.</span></span>

> [!TIP]
> <span data-ttu-id="e66a6-246">En choisissant l’option taille de page de droite hello est un équilibre entre l’utilisation de la mémoire pendant la demande de hello, l’utilisation de la bande passante et retard dans la réception des données de salutation complètement.</span><span class="sxs-lookup"><span data-stu-id="e66a6-246">Choosing hello right page size is a balance between memory usage while hello request is happening, bandwidth usage and delay in receiving hello data completely.</span></span>  <span data-ttu-id="e66a6-247">la valeur par défaut de Hello (50 enregistrements) est adaptée à tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="e66a6-247">hello default (50 records) is suitable for all devices.</span></span>  <span data-ttu-id="e66a6-248">Si vous utilisez exclusivement sur les périphériques de mémoire supérieure, augmenter jusqu'à too500.</span><span class="sxs-lookup"><span data-stu-id="e66a6-248">If you exclusively operate on larger memory devices, increase up too500.</span></span>  <span data-ttu-id="e66a6-249">Nous avons constaté que taille de la page hello augmenter au-delà de 500 enregistre les résultats dans des délais inacceptables et les problèmes de mémoire de grande taille.</span><span class="sxs-lookup"><span data-stu-id="e66a6-249">We have found that increasing hello page size beyond 500 records results in unacceptable delays and large memory issues.</span></span>

### <span data-ttu-id="e66a6-250"><a name="chaining"></a>Procédure de concaténation de méthodes de requête</span><span class="sxs-lookup"><span data-stu-id="e66a6-250"><a name="chaining"></a>How to: Concatenate query methods</span></span>

<span data-ttu-id="e66a6-251">les méthodes Hello utilisées lors de l’interrogation des tables du serveur principal peuvent être concaténées.</span><span class="sxs-lookup"><span data-stu-id="e66a6-251">hello methods used in querying backend tables can be concatenated.</span></span> <span data-ttu-id="e66a6-252">Chaînage des propriétés de la requête de méthodes vous permet de tooselect des colonnes spécifiques de lignes filtrées triées et réserve paginées.</span><span class="sxs-lookup"><span data-stu-id="e66a6-252">Chaining query methods allows you tooselect specific columns of filtered rows that are sorted and paged.</span></span> <span data-ttu-id="e66a6-253">Vous pouvez créer des filtres logiques complexes.</span><span class="sxs-lookup"><span data-stu-id="e66a6-253">You can create complex logical filters.</span></span>  <span data-ttu-id="e66a6-254">Chaque méthode de requête retourne un objet de requête.</span><span class="sxs-lookup"><span data-stu-id="e66a6-254">Each query method returns a Query object.</span></span> <span data-ttu-id="e66a6-255">série de hello tooend de méthodes et de requête d’exécution réellement hello, appel hello **exécuter** (méthode).</span><span class="sxs-lookup"><span data-stu-id="e66a6-255">tooend hello series of methods and actually run hello query, call hello **execute** method.</span></span> <span data-ttu-id="e66a6-256">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e66a6-256">For example:</span></span>

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

<span data-ttu-id="e66a6-257">Hello chaînés requête méthodes doivent être classées comme suit :</span><span class="sxs-lookup"><span data-stu-id="e66a6-257">hello chained query methods must be ordered as follows:</span></span>

1. <span data-ttu-id="e66a6-258">Filtrage des méthodes (**where**).</span><span class="sxs-lookup"><span data-stu-id="e66a6-258">Filtering (**where**) methods.</span></span>
2. <span data-ttu-id="e66a6-259">Tri des méthodes (**orderBy**).</span><span class="sxs-lookup"><span data-stu-id="e66a6-259">Sorting (**orderBy**) methods.</span></span>
3. <span data-ttu-id="e66a6-260">Sélection des méthodes (**select**).</span><span class="sxs-lookup"><span data-stu-id="e66a6-260">Selection (**select**) methods.</span></span>
4. <span data-ttu-id="e66a6-261">pagination des méthodes (**skip** et **top**).</span><span class="sxs-lookup"><span data-stu-id="e66a6-261">paging (**skip** and **top**) methods.</span></span>

## <span data-ttu-id="e66a6-262"><a name="binding"></a>Lier l’interface utilisateur de données toohello</span><span class="sxs-lookup"><span data-stu-id="e66a6-262"><a name="binding"></a>Bind data toohello user interface</span></span>

<span data-ttu-id="e66a6-263">La liaison des données nécessite trois composants :</span><span class="sxs-lookup"><span data-stu-id="e66a6-263">Data binding involves three components:</span></span>

* <span data-ttu-id="e66a6-264">source de données Hello</span><span class="sxs-lookup"><span data-stu-id="e66a6-264">hello data source</span></span>
* <span data-ttu-id="e66a6-265">disposition de l’écran Hello</span><span class="sxs-lookup"><span data-stu-id="e66a6-265">hello screen layout</span></span>
* <span data-ttu-id="e66a6-266">adaptateur Hello que ties hello deux ensemble.</span><span class="sxs-lookup"><span data-stu-id="e66a6-266">hello adapter that ties hello two together.</span></span>

<span data-ttu-id="e66a6-267">Dans notre exemple de code, nous retournent des données de hello à partir de la table de Mobile applications SQL Azure hello **ToDoItem** dans un tableau.</span><span class="sxs-lookup"><span data-stu-id="e66a6-267">In our sample code, we return hello data from hello Mobile Apps SQL Azure table **ToDoItem** into an array.</span></span> <span data-ttu-id="e66a6-268">Cette activité est un cas de figure très courant pour les applications de données.</span><span class="sxs-lookup"><span data-stu-id="e66a6-268">This activity is a common pattern for data applications.</span></span>  <span data-ttu-id="e66a6-269">Requêtes de base de données retournent souvent une collection de lignes qui hello client obtient dans une liste ou un tableau.</span><span class="sxs-lookup"><span data-stu-id="e66a6-269">Database queries often return a collection of rows that hello client gets in a list or array.</span></span> <span data-ttu-id="e66a6-270">Dans cet exemple, le tableau de hello est source de données hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-270">In this sample, hello array is hello data source.</span></span>  <span data-ttu-id="e66a6-271">code de Hello spécifie une disposition de l’écran qui définit la vue hello de données hello qui s’affiche sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-271">hello code specifies a screen layout that defines hello view of hello data that appears on hello device.</span></span>  <span data-ttu-id="e66a6-272">Hello deux sont liés avec un adaptateur, dans ce code est une extension de hello **ArrayAdapter&lt;ToDoItem&gt;**  classe.</span><span class="sxs-lookup"><span data-stu-id="e66a6-272">hello two are bound together with an adapter, which in this code is an extension of hello **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span>

#### <span data-ttu-id="e66a6-273"><a name="layout"></a>Définir hello mise en page</span><span class="sxs-lookup"><span data-stu-id="e66a6-273"><a name="layout"></a>Define hello Layout</span></span>

<span data-ttu-id="e66a6-274">mise en page Hello est définie par plusieurs extraits de code XML.</span><span class="sxs-lookup"><span data-stu-id="e66a6-274">hello layout is defined by several snippets of XML code.</span></span> <span data-ttu-id="e66a6-275">Étant donné une mise en page existante, hello suivant code représente hello **ListView** nous souhaitons toopopulate avec nos données de serveur.</span><span class="sxs-lookup"><span data-stu-id="e66a6-275">Given an existing layout, hello following code represents hello **ListView** we want toopopulate with our server data.</span></span>

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

<span data-ttu-id="e66a6-276">Bonjour précédant le code, hello *listitem* attribut spécifie l’id hello de disposition hello pour une ligne spécifique dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-276">In hello preceding code, hello *listitem* attribute specifies hello id of hello layout for an individual row in hello list.</span></span> <span data-ttu-id="e66a6-277">Ce code spécifie une case à cocher et son texte associé et est instancié une fois pour chaque élément de liste de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-277">This code specifies a check box and its associated text and gets instantiated once for each item in hello list.</span></span> <span data-ttu-id="e66a6-278">Cette mise en page ne s’affiche pas hello **id** champ et une mise en page plus complexe seraient spécifier des champs supplémentaires dans l’affichage de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-278">This layout does not display hello **id** field, and a more complex layout would specify additional fields in hello display.</span></span> <span data-ttu-id="e66a6-279">Ce code est Bonjour **row_list_to_do.xml** fichier.</span><span class="sxs-lookup"><span data-stu-id="e66a6-279">This code is in hello **row_list_to_do.xml** file.</span></span>

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <span data-ttu-id="e66a6-280"><a name="adapter"></a>Définir l’adaptateur hello</span><span class="sxs-lookup"><span data-stu-id="e66a6-280"><a name="adapter"></a>Define hello adapter</span></span>
<span data-ttu-id="e66a6-281">Étant donné que la source de données hello de notre vue est un tableau de **ToDoItem**, nous sous-classe notre adaptateur à partir d’un **ArrayAdapter&lt;ToDoItem&gt;**  classe.</span><span class="sxs-lookup"><span data-stu-id="e66a6-281">Since hello data source of our view is an array of **ToDoItem**, we subclass our adapter from an **ArrayAdapter&lt;ToDoItem&gt;** class.</span></span> <span data-ttu-id="e66a6-282">Cette sous-classe génère une vue pour chaque **ToDoItem** à l’aide de hello **row_list_to_do** mise en page.</span><span class="sxs-lookup"><span data-stu-id="e66a6-282">This subclass produces a View for every **ToDoItem** using hello **row_list_to_do** layout.</span></span>  <span data-ttu-id="e66a6-283">Dans notre code, nous définissons hello suivant de classe est une extension de hello **ArrayAdapter&lt;E&gt;**  classe :</span><span class="sxs-lookup"><span data-stu-id="e66a6-283">In our code, we define hello following class that is an extension of hello **ArrayAdapter&lt;E&gt;** class:</span></span>

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

<span data-ttu-id="e66a6-284">Remplacer les adaptateurs hello **getView** (méthode).</span><span class="sxs-lookup"><span data-stu-id="e66a6-284">Override hello adapters **getView** method.</span></span> <span data-ttu-id="e66a6-285">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e66a6-285">For example:</span></span>

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

<span data-ttu-id="e66a6-286">Nous créons une instance de cette classe dans notre activité, comme suit :</span><span class="sxs-lookup"><span data-stu-id="e66a6-286">We create an instance of this class in our Activity as follows:</span></span>

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

<span data-ttu-id="e66a6-287">Hello deuxième paramètre toohello ToDoItemAdapter constructeur est une disposition de toohello de référence.</span><span class="sxs-lookup"><span data-stu-id="e66a6-287">hello second parameter toohello ToDoItemAdapter constructor is a reference toohello layout.</span></span> <span data-ttu-id="e66a6-288">Nous pouvons maintenant d’instancier hello **ListView** et affecter hello adaptateur toohello **ListView**.</span><span class="sxs-lookup"><span data-stu-id="e66a6-288">We can now instantiate hello **ListView** and assign hello adapter toohello **ListView**.</span></span>

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <span data-ttu-id="e66a6-289"><a name="use-adapter"></a>Utilisez hello adaptateur tooBind toohello l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="e66a6-289"><a name="use-adapter"></a>Use hello Adapter tooBind toohello UI</span></span>

<span data-ttu-id="e66a6-290">Vous êtes maintenant prêt toouse la liaison de données.</span><span class="sxs-lookup"><span data-stu-id="e66a6-290">You are now ready toouse data binding.</span></span> <span data-ttu-id="e66a6-291">Hello de code suivant montre comment tooget des éléments dans la table de hello et de remplissages hello adaptateur local avec hello articles retourné.</span><span class="sxs-lookup"><span data-stu-id="e66a6-291">hello following code shows how tooget items in hello table and fills hello local adapter with hello returned items.</span></span>

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

<span data-ttu-id="e66a6-292">Appeler l’adaptateur hello chaque fois que vous modifiez hello **ToDoItem** table.</span><span class="sxs-lookup"><span data-stu-id="e66a6-292">Call hello adapter any time you modify hello **ToDoItem** table.</span></span> <span data-ttu-id="e66a6-293">Comme les modifications se font enregistrement par enregistrement, vous ne gérez qu’une seule ligne, et non une collection.</span><span class="sxs-lookup"><span data-stu-id="e66a6-293">Since modifications are done on a record by record basis, you handle a single row instead of a collection.</span></span> <span data-ttu-id="e66a6-294">Lorsque vous insérez un élément, appelez hello **ajouter** méthode sur hello adaptateur ; lors de la suppression, appelez hello **supprimer** (méthode).</span><span class="sxs-lookup"><span data-stu-id="e66a6-294">When you insert an item, call hello **add** method on hello adapter; when deleting, call hello **remove** method.</span></span>

<span data-ttu-id="e66a6-295">Vous trouverez un exemple complet dans hello [projet de démarrage rapide Android][21].</span><span class="sxs-lookup"><span data-stu-id="e66a6-295">You can find a complete example in hello [Android Quickstart Project][21].</span></span>

## <span data-ttu-id="e66a6-296"><a name="inserting"></a>Insérer des données dans le back-end hello</span><span class="sxs-lookup"><span data-stu-id="e66a6-296"><a name="inserting"></a>Insert data into hello backend</span></span>

<span data-ttu-id="e66a6-297">Instancier une instance de hello *ToDoItem* classe et définissez ses propriétés.</span><span class="sxs-lookup"><span data-stu-id="e66a6-297">Instantiate an instance of hello *ToDoItem* class and set its properties.</span></span>

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

<span data-ttu-id="e66a6-298">Utilisez ensuite **insert()** tooinsert un objet :</span><span class="sxs-lookup"><span data-stu-id="e66a6-298">Then use **insert()** tooinsert an object:</span></span>

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="e66a6-299">Hello retourné correspond à des entités données hello insérées dans la table principale de hello, ID de hello inclus et d’autres valeurs (par exemple hello `createdAt`, `updatedAt`, et `version` champs) définie sur hello principal.</span><span class="sxs-lookup"><span data-stu-id="e66a6-299">hello returned entity matches hello data inserted into hello backend table, included hello ID and any other values (such as hello `createdAt`, `updatedAt`, and `version` fields) set on hello backend.</span></span>

<span data-ttu-id="e66a6-300">Les tables Mobile Apps nécessitent une colonne de clé primaire nommée **id**. Cette colonne doit être une chaîne.</span><span class="sxs-lookup"><span data-stu-id="e66a6-300">Mobile Apps tables require a primary key column named **id**. This column must be a string.</span></span> <span data-ttu-id="e66a6-301">valeur par défaut de Hello hello colonne d’ID est un GUID.</span><span class="sxs-lookup"><span data-stu-id="e66a6-301">hello default value of hello ID column is a GUID.</span></span>  <span data-ttu-id="e66a6-302">Vous pouvez fournir d’autres valeurs uniques, telles que des adresses de messagerie ou des noms d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="e66a6-302">You can provide other unique values, such as email addresses or usernames.</span></span> <span data-ttu-id="e66a6-303">Lorsqu’une valeur d’ID de chaîne n’est pas fournie pour un enregistrement inséré, hello principal génère un nouveau GUID.</span><span class="sxs-lookup"><span data-stu-id="e66a6-303">When a string ID value is not provided for an inserted record, hello backend generates a new GUID.</span></span>

<span data-ttu-id="e66a6-304">Fournissent des valeurs d’ID de chaîne hello suivant avantages :</span><span class="sxs-lookup"><span data-stu-id="e66a6-304">String ID values provide hello following advantages:</span></span>

* <span data-ttu-id="e66a6-305">ID peuvent être générés sans passer d’une base de données toohello aller-retour.</span><span class="sxs-lookup"><span data-stu-id="e66a6-305">IDs can be generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="e66a6-306">Les enregistrements sont toomerge plus facile à partir de différentes tables ou bases de données.</span><span class="sxs-lookup"><span data-stu-id="e66a6-306">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="e66a6-307">Les valeurs d’ID s’intègrent mieux à la logique d’une application.</span><span class="sxs-lookup"><span data-stu-id="e66a6-307">ID values integrate better with an application's logic.</span></span>

<span data-ttu-id="e66a6-308">Les valeurs d’ID de chaîne sont **obligatoires** pour la prise en charge de la synchronisation hors connexion.</span><span class="sxs-lookup"><span data-stu-id="e66a6-308">String ID values are **REQUIRED** for offline sync support.</span></span>  <span data-ttu-id="e66a6-309">Vous ne pouvez pas modifier un Id une fois qu’il est stocké dans la base de données principale hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-309">You cannot change an Id once it is stored in hello backend database.</span></span>

## <span data-ttu-id="e66a6-310"><a name="updating"></a>Mettre à jour des données dans une application mobile</span><span class="sxs-lookup"><span data-stu-id="e66a6-310"><a name="updating"></a>Update data in a mobile app</span></span>

<span data-ttu-id="e66a6-311">tooupdate des données dans une table, passez hello nouvel objet toohello **update()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="e66a6-311">tooupdate data in a table, pass hello new object toohello **update()** method.</span></span>

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

<span data-ttu-id="e66a6-312">Dans cet exemple, *élément* est une ligne de tooa référence Bonjour *ToDoItem* table, ce qui a été tooit de certaines modifications apportées.</span><span class="sxs-lookup"><span data-stu-id="e66a6-312">In this example, *item* is a reference tooa row in hello *ToDoItem* table, which has had some changes made tooit.</span></span>  <span data-ttu-id="e66a6-313">ligne Hello avec hello même **id** est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="e66a6-313">hello row with hello same **id** is updated.</span></span>

## <span data-ttu-id="e66a6-314"><a name="deleting"></a>Supprimer des données dans une application mobile</span><span class="sxs-lookup"><span data-stu-id="e66a6-314"><a name="deleting"></a>Delete data in a mobile app</span></span>

<span data-ttu-id="e66a6-315">Hello suivant de code montre comment toodelete des données à partir d’une table en spécifiant hello objet de données.</span><span class="sxs-lookup"><span data-stu-id="e66a6-315">hello following code shows how toodelete data from a table by specifying hello data object.</span></span>

```java
mToDoTable
    .delete(item);
```

<span data-ttu-id="e66a6-316">Vous pouvez également supprimer un élément en spécifiant hello **id** champ hello ligne toodelete.</span><span class="sxs-lookup"><span data-stu-id="e66a6-316">You can also delete an item by specifying hello **id** field of hello row toodelete.</span></span>

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <span data-ttu-id="e66a6-317"><a name="lookup"></a>Rechercher un élément spécifique par ID</span><span class="sxs-lookup"><span data-stu-id="e66a6-317"><a name="lookup"></a>Look up a specific item by Id</span></span>

<span data-ttu-id="e66a6-318">Rechercher un élément avec un spécifique **id** champ hello **lookUp()** méthode :</span><span class="sxs-lookup"><span data-stu-id="e66a6-318">Look up an item with a specific **id** field with hello **lookUp()** method:</span></span>

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <span data-ttu-id="e66a6-319"><a name="untyped"></a>Procédure : utilisation de données non typées</span><span class="sxs-lookup"><span data-stu-id="e66a6-319"><a name="untyped"></a>How to: Work with untyped data</span></span>

<span data-ttu-id="e66a6-320">modèle de programmation non typé Hello donne exacte contrôler la sérialisation JSON.</span><span class="sxs-lookup"><span data-stu-id="e66a6-320">hello untyped programming model gives you exact control over JSON serialization.</span></span>  <span data-ttu-id="e66a6-321">Il existe quelques scénarios courants où vous pouvez toouse un modèle de programmation non typé.</span><span class="sxs-lookup"><span data-stu-id="e66a6-321">There are some common scenarios where you may wish toouse an untyped programming model.</span></span> <span data-ttu-id="e66a6-322">Par exemple, si votre table principale contient de nombreuses colonnes et que vous ne devez tooreference un sous-ensemble de colonnes de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-322">For example, if your backend table contains many columns and you only need tooreference a subset of hello columns.</span></span>  <span data-ttu-id="e66a6-323">modèle de type Hello nécessite toodefine toutes les colonnes hello définis dans le back-end des applications mobiles hello dans votre classe de données.</span><span class="sxs-lookup"><span data-stu-id="e66a6-323">hello typed model requires you toodefine all hello columns defined in hello Mobile Apps backend in your data class.</span></span>  <span data-ttu-id="e66a6-324">La plupart des appels d’API pour accéder aux données de hello est similaire toohello tapé des appels de programmation.</span><span class="sxs-lookup"><span data-stu-id="e66a6-324">Most of hello API calls for accessing data are similar toohello typed programming calls.</span></span> <span data-ttu-id="e66a6-325">Hello principale différence est que dans le modèle non typée de hello vous appelez des méthodes sur hello **MobileServiceJsonTable** objet au lieu de hello **MobileServiceTable** objet.</span><span class="sxs-lookup"><span data-stu-id="e66a6-325">hello main difference is that in hello untyped model you invoke methods on hello **MobileServiceJsonTable** object, instead of hello **MobileServiceTable** object.</span></span>

### <span data-ttu-id="e66a6-326"><a name="json_instance"></a>Créer une instance de table non typée</span><span class="sxs-lookup"><span data-stu-id="e66a6-326"><a name="json_instance"></a>Create an instance of an untyped table</span></span>

<span data-ttu-id="e66a6-327">Toohello similaire tapé le modèle, vous commencez par obtenir une référence de table, mais dans ce cas, il est un **MobileServicesJsonTable** objet.</span><span class="sxs-lookup"><span data-stu-id="e66a6-327">Similar toohello typed model, you start by getting a table reference, but in this case it's a **MobileServicesJsonTable** object.</span></span> <span data-ttu-id="e66a6-328">Obtenir la référence de hello en appelant hello **getTable** méthode sur une instance du client de hello :</span><span class="sxs-lookup"><span data-stu-id="e66a6-328">Obtain hello reference by calling hello **getTable** method on an instance of hello client:</span></span>

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

<span data-ttu-id="e66a6-329">Une fois que vous avez créé une instance de hello **MobileServiceJsonTable**, il a hello virtuellement même API disponible en tant que modèle de programmation typée hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-329">Once you have created an instance of hello **MobileServiceJsonTable**, it has virtually hello same API available as with hello typed programming model.</span></span> <span data-ttu-id="e66a6-330">Dans certains cas, les méthodes hello prennent un paramètre non typé au lieu d’un paramètre typé.</span><span class="sxs-lookup"><span data-stu-id="e66a6-330">In some cases, hello methods take an untyped parameter instead of a typed parameter.</span></span>

### <span data-ttu-id="e66a6-331"><a name="json_insert"></a>Insérer une table non typée</span><span class="sxs-lookup"><span data-stu-id="e66a6-331"><a name="json_insert"></a>Insert into an untyped table</span></span>
<span data-ttu-id="e66a6-332">Hello suivant de code montre comment toodo une instruction insert.</span><span class="sxs-lookup"><span data-stu-id="e66a6-332">hello following code shows how toodo an insert.</span></span> <span data-ttu-id="e66a6-333">première étape Hello est toocreate un [JsonObject][1], qui fait partie de hello [gson] [ 3] bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="e66a6-333">hello first step is toocreate a [JsonObject][1], which is part of hello [gson][3] library.</span></span>

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

<span data-ttu-id="e66a6-334">Ensuite, utilisez **insert()** objet non typé de tooinsert hello dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-334">Then, Use **insert()** tooinsert hello untyped object into hello table.</span></span>

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

<span data-ttu-id="e66a6-335">Si vous devez tooget hello ID objet de hello inséré, utilisez hello **getAsJsonPrimitive()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="e66a6-335">If you need tooget hello ID of hello inserted object, use hello **getAsJsonPrimitive()** method.</span></span>

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <span data-ttu-id="e66a6-336"><a name="json_delete"></a>Supprimer d’une table non typée</span><span class="sxs-lookup"><span data-stu-id="e66a6-336"><a name="json_delete"></a>Delete from an untyped table</span></span>
<span data-ttu-id="e66a6-337">Hello de code suivant montre comment toodelete une instance, hello dans ce cas, la même instance d’un **JsonObject** qui a été créé avant de hello *insérer* exemple.</span><span class="sxs-lookup"><span data-stu-id="e66a6-337">hello following code shows how toodelete an instance, in this case, hello same instance of a **JsonObject** that was created in hello prior *insert* example.</span></span> <span data-ttu-id="e66a6-338">code de Hello est hello même chose avec hello tapé du cas, mais la méthode hello possède une signature différente, car elle fait référence à un **JsonObject**.</span><span class="sxs-lookup"><span data-stu-id="e66a6-338">hello code is hello same as with hello typed case, but hello method has a different signature since it references an **JsonObject**.</span></span>

```java
mToDoTable
    .delete(insertedItem);
```

<span data-ttu-id="e66a6-339">Vous pouvez aussi directement supprimer une instance avec son ID :</span><span class="sxs-lookup"><span data-stu-id="e66a6-339">You can also delete an instance directly by using its ID:</span></span>

```java
mToDoTable.delete(ID);
```

### <span data-ttu-id="e66a6-340"><a name="json_get"></a>Renvoyer toutes les lignes d’une table non typée</span><span class="sxs-lookup"><span data-stu-id="e66a6-340"><a name="json_get"></a>Return all rows from an untyped table</span></span>
<span data-ttu-id="e66a6-341">Hello suivant de code montre comment tooretrieve une table entière.</span><span class="sxs-lookup"><span data-stu-id="e66a6-341">hello following code shows how tooretrieve an entire table.</span></span> <span data-ttu-id="e66a6-342">Étant donné que vous utilisez un tableau JSON, vous pouvez sélectivement récupérer uniquement certaines colonnes de la table hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-342">Since you are using a JSON Table, you can selectively retrieve only some of hello table's columns.</span></span>

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

<span data-ttu-id="e66a6-343">Hello même ensemble de filtrage, le filtrage et la pagination des méthodes qui sont disponibles pour le modèle de type hello sont disponibles pour les modèles non typé hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-343">hello same set of filtering, filtering and paging methods that are available for hello typed model are available for hello untyped model.</span></span>

## <span data-ttu-id="e66a6-344"><a name="offline-sync"></a>Implémenter la synchronisation hors connexion</span><span class="sxs-lookup"><span data-stu-id="e66a6-344"><a name="offline-sync"></a>Implement Offline Sync</span></span>

<span data-ttu-id="e66a6-345">Bonjour Azure Mobile Apps Client SDK implémente également une synchronisation hors connexion de données à l’aide un toostore de la base de données SQLite une copie des données de serveur hello localement.</span><span class="sxs-lookup"><span data-stu-id="e66a6-345">hello Azure Mobile Apps Client SDK also implements offline synchronization of data by using a SQLite database toostore a copy of hello server data locally.</span></span>  <span data-ttu-id="e66a6-346">Opérations effectuées sur une table en mode hors connexion ne nécessitent pas de connectivité mobile toowork.</span><span class="sxs-lookup"><span data-stu-id="e66a6-346">Operations performed on an offline table do not require mobile connectivity toowork.</span></span>  <span data-ttu-id="e66a6-347">Synchronisation hors connexion contribue à la résilience et les performances à des frais de hello d’une logique plus complexe pour la résolution de conflit.</span><span class="sxs-lookup"><span data-stu-id="e66a6-347">Offline sync aids in resilience and performance at hello expense of more complex logic for conflict resolution.</span></span>  <span data-ttu-id="e66a6-348">Bonjour Azure Mobile Apps Client SDK implémente hello suivant de fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="e66a6-348">hello Azure Mobile Apps Client SDK implements hello following features:</span></span>

* <span data-ttu-id="e66a6-349">Synchronisation incrémentielle : seuls les enregistrements nouveaux et mis à jour sont téléchargés, ce qui permet d’économiser de la bande passante et de la mémoire.</span><span class="sxs-lookup"><span data-stu-id="e66a6-349">Incremental Sync: Only updated and new records are downloaded, saving bandwidth and memory consumption.</span></span>
* <span data-ttu-id="e66a6-350">L’accès concurrentiel optimiste : Les opérations sont supposées toosucceed.</span><span class="sxs-lookup"><span data-stu-id="e66a6-350">Optimistic Concurrency: Operations are assumed toosucceed.</span></span>  <span data-ttu-id="e66a6-351">Résolution des conflits est différée jusqu'à ce que les mises à jour sont effectuées sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-351">Conflict Resolution is deferred until updates are performed on hello server.</span></span>
* <span data-ttu-id="e66a6-352">Résolution des conflits : hello que SDK détecte une modification en conflit a été effectuée sur le serveur de hello et fournit des raccordements utilisateur de hello tooalert.</span><span class="sxs-lookup"><span data-stu-id="e66a6-352">Conflict Resolution: hello SDK detects when a conflicting change has been made at hello server and provides hooks tooalert hello user.</span></span>
* <span data-ttu-id="e66a6-353">Suppression réversible : Enregistrements supprimés sont marquées comme supprimées, ce qui permet d’autres tooupdate périphériques leur cache hors connexion.</span><span class="sxs-lookup"><span data-stu-id="e66a6-353">Soft Delete: Deleted records are marked deleted, allowing other devices tooupdate their offline cache.</span></span>

### <a name="initialize-offline-sync"></a><span data-ttu-id="e66a6-354">Initialiser la synchronisation hors connexion</span><span class="sxs-lookup"><span data-stu-id="e66a6-354">Initialize Offline Sync</span></span>

<span data-ttu-id="e66a6-355">Chaque table hors connexion doit être défini dans le cache hors connexion hello avant des utiliser.</span><span class="sxs-lookup"><span data-stu-id="e66a6-355">Each offline table must be defined in hello offline cache before use.</span></span>  <span data-ttu-id="e66a6-356">Normalement, la définition de la table est effectuée immédiatement après la création de hello du client de hello :</span><span class="sxs-lookup"><span data-stu-id="e66a6-356">Normally, table definition is done immediately after hello creation of hello client:</span></span>

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a><span data-ttu-id="e66a6-357">Obtenir une référence de toohello Table de Cache hors connexion</span><span class="sxs-lookup"><span data-stu-id="e66a6-357">Obtain a reference toohello Offline Cache Table</span></span>

<span data-ttu-id="e66a6-358">Pour une table en ligne, vous utilisez `.getTable()`.</span><span class="sxs-lookup"><span data-stu-id="e66a6-358">For an online table, you use `.getTable()`.</span></span>  <span data-ttu-id="e66a6-359">Pour une table hors connexion, utilisez `.getSyncTable()` :</span><span class="sxs-lookup"><span data-stu-id="e66a6-359">For an offline table, use `.getSyncTable()`:</span></span>

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

<span data-ttu-id="e66a6-360">Tous les hello des méthodes qui sont disponibles pour les tables en ligne (y compris le filtrage, tri, la pagination, insertion de données, mise à jour des données et la suppression des données) fonctionnent aussi bien sur les tables en ligne et hors connexion.</span><span class="sxs-lookup"><span data-stu-id="e66a6-360">All hello methods that are available for online tables (including filtering, sorting, paging, inserting data, updating data, and deleting data) work equally well on online and offline tables.</span></span>

### <a name="synchronize-hello-local-offline-cache"></a><span data-ttu-id="e66a6-361">Synchroniser hello Cache Local en mode hors connexion</span><span class="sxs-lookup"><span data-stu-id="e66a6-361">Synchronize hello Local Offline Cache</span></span>

<span data-ttu-id="e66a6-362">La synchronisation est dans un contrôle hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="e66a6-362">Synchronization is within hello control of your app.</span></span>  <span data-ttu-id="e66a6-363">Voici un exemple de méthode de synchronisation :</span><span class="sxs-lookup"><span data-stu-id="e66a6-363">Here is an example synchronization method:</span></span>

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

<span data-ttu-id="e66a6-364">Si un nom de requête est fourni toohello `.pull(query, queryname)` (méthode), puis synchronisation incrémentielle est utilisée tooreturn uniquement les enregistrements qui ont été créés ou modifiés depuis l’extraction de hello dernier terminé avec succès.</span><span class="sxs-lookup"><span data-stu-id="e66a6-364">If a query name is provided toohello `.pull(query, queryname)` method, then incremental sync is used tooreturn only records that have been created or changed since hello last successfully completed pull.</span></span>

### <a name="handle-conflicts-during-offline-synchronization"></a><span data-ttu-id="e66a6-365">Gérer les conflits lors de la synchronisation hors connexion</span><span class="sxs-lookup"><span data-stu-id="e66a6-365">Handle Conflicts during Offline Synchronization</span></span>

<span data-ttu-id="e66a6-366">Si un conflit se produit pendant une opération `.push()`, une exception `MobileServiceConflictException` est levée.</span><span class="sxs-lookup"><span data-stu-id="e66a6-366">If a conflict happens during a `.push()` operation, a `MobileServiceConflictException` is thrown.</span></span>   <span data-ttu-id="e66a6-367">élément de serveur émis Hello est incorporé dans l’exception de hello et peuvent être récupéré par `.getItem()` sur l’exception de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-367">hello server-issued item is embedded in hello exception and can be retrieved by `.getItem()` on hello exception.</span></span>  <span data-ttu-id="e66a6-368">Ajuster push hello en appelant hello éléments suivants de l’objet de MobileServiceSyncContext hello :</span><span class="sxs-lookup"><span data-stu-id="e66a6-368">Adjust hello push by calling hello following items on hello MobileServiceSyncContext object:</span></span>

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

<span data-ttu-id="e66a6-369">Une fois que tous les conflits sont marquées comme vous le souhaitez, appelez `.push()` tooresolve à nouveau toutes les hello est en conflit.</span><span class="sxs-lookup"><span data-stu-id="e66a6-369">Once all conflicts are marked as you wish, call `.push()` again tooresolve all hello conflicts.</span></span>

## <span data-ttu-id="e66a6-370"><a name="custom-api"></a>Appeler une API personnalisée</span><span class="sxs-lookup"><span data-stu-id="e66a6-370"><a name="custom-api"></a>Call a custom API</span></span>

<span data-ttu-id="e66a6-371">Une API personnalisée vous permet de toodefine points de terminaison personnalisés qui exposent les fonctionnalités de serveur qui ne pas mapper tooan insérer, mettre à jour, supprimer ou opération de lecture.</span><span class="sxs-lookup"><span data-stu-id="e66a6-371">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="e66a6-372">En utilisant une API personnalisée, vous pouvez exercer davantage de contrôle sur la messagerie, notamment lire et définir des en-têtes de message HTTP et définir un format de corps de message autre que JSON.</span><span class="sxs-lookup"><span data-stu-id="e66a6-372">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="e66a6-373">À partir d’un client Android, vous appelez hello **invokeApi** méthode toocall hello API point de terminaison personnalisé.</span><span class="sxs-lookup"><span data-stu-id="e66a6-373">From an Android client, you call hello **invokeApi** method toocall hello custom API endpoint.</span></span> <span data-ttu-id="e66a6-374">Hello suivant montre comment toocall un point de terminaison API nommé **completeAll**, qui retourne une classe de collection nommée **MarkAllResult**.</span><span class="sxs-lookup"><span data-stu-id="e66a6-374">hello following example shows how toocall an API endpoint named **completeAll**, which returns a collection class named **MarkAllResult**.</span></span>

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

<span data-ttu-id="e66a6-375">Hello **invokeApi** méthode est appelée sur le client hello, qui envoie un message demande toohello une nouvelle API personnalisée.</span><span class="sxs-lookup"><span data-stu-id="e66a6-375">hello **invokeApi** method is called on hello client, which sends a POST request toohello new custom API.</span></span> <span data-ttu-id="e66a6-376">résultat de Hello retourné par l’API personnalisée hello s’affiche dans une boîte de dialogue de message, comme des erreurs.</span><span class="sxs-lookup"><span data-stu-id="e66a6-376">hello result returned by hello custom API is displayed in a message dialog, as are any errors.</span></span> <span data-ttu-id="e66a6-377">Autres versions de **invokeApi** vous permettent d’envoyer un objet dans le corps de la demande hello si vous le souhaitez, spécifier la méthode hello HTTP et envoyer des paramètres de requête avec la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-377">Other versions of **invokeApi** let you optionally send an object in hello request body, specify hello HTTP method, and send query parameters with hello request.</span></span> <span data-ttu-id="e66a6-378">Des versions non typées de la méthode **invokeApi** sont également fournies.</span><span class="sxs-lookup"><span data-stu-id="e66a6-378">Untyped versions of **invokeApi** are provided as well.</span></span>

## <span data-ttu-id="e66a6-379"><a name="authentication"></a>Ajouter une application de tooyour d’authentification</span><span class="sxs-lookup"><span data-stu-id="e66a6-379"><a name="authentication"></a>Add authentication tooyour app</span></span>

<span data-ttu-id="e66a6-380">Didacticiels déjà décrivent en détail comment tooadd ces fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="e66a6-380">Tutorials already describe in detail how tooadd these features.</span></span>

<span data-ttu-id="e66a6-381">App Service prend en charge [l’authentification des utilisateurs d’applications](app-service-mobile-android-get-started-users.md) via divers fournisseurs d’identité externes : Facebook, Google, compte Microsoft, Twitter et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e66a6-381">App Service supports [authenticating app users](app-service-mobile-android-get-started-users.md) using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="e66a6-382">Vous pouvez définir des autorisations sur l’accès aux toorestrict de tables pour des opérations spécifiques aux utilisateurs de tooonly authentifié.</span><span class="sxs-lookup"><span data-stu-id="e66a6-382">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="e66a6-383">Vous pouvez également utiliser l’identité hello des règles d’autorisation de tooimplement utilisateurs authentifiés dans votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e66a6-383">You can also use hello identity of authenticated users tooimplement authorization rules in your backend.</span></span>

<span data-ttu-id="e66a6-384">Deux flux d’authentification sont pris en charge : un flux **serveur** et un flux **client**.</span><span class="sxs-lookup"><span data-stu-id="e66a6-384">Two authentication flows are supported: a **server** flow and a **client** flow.</span></span> <span data-ttu-id="e66a6-385">flux de serveur Hello fournit expérience d’authentification la plus simple hello, car il repose sur l’interface web hello identité fournisseurs.</span><span class="sxs-lookup"><span data-stu-id="e66a6-385">hello server flow provides hello simplest authentication experience, as it relies on hello identity providers web interface.</span></span>  <span data-ttu-id="e66a6-386">Aucun SDK supplémentaires n’est l’authentification du serveur flux tooimplement requis.</span><span class="sxs-lookup"><span data-stu-id="e66a6-386">No additional SDKs are required tooimplement server flow authentication.</span></span> <span data-ttu-id="e66a6-387">L’authentification du serveur flux ne fournit pas d’une intégration complète dans les appareils mobiles hello et est recommandée uniquement pour la preuve de concept.</span><span class="sxs-lookup"><span data-stu-id="e66a6-387">Server flow authentication does not provide a deep integration into hello mobile device and is only recommended for proof of concept scenarios.</span></span>

<span data-ttu-id="e66a6-388">flux Hello du client permet une intégration plus étroite avec les fonctionnalités spécifiques au périphérique tels que l’authentification unique sur car elle s’appuie sur les kits de développement logiciel fournis par le fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-388">hello client flow allows for deeper integration with device-specific capabilities such as single sign-on as it relies on SDKs provided by hello identity provider.</span></span>  <span data-ttu-id="e66a6-389">Par exemple, vous pouvez intégrer hello SDK Facebook dans votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="e66a6-389">For example, you can integrate hello Facebook SDK into your mobile application.</span></span>  <span data-ttu-id="e66a6-390">les clients mobiles Hello échange dans l’application de Facebook hello et confirme l’authentification avant d’échanger tooyour arrière des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="e66a6-390">hello mobile client swaps into hello Facebook app and confirms your sign-on before swapping back tooyour mobile app.</span></span>

<span data-ttu-id="e66a6-391">Quatre étapes sont tooenable requis dans votre application :</span><span class="sxs-lookup"><span data-stu-id="e66a6-391">Four steps are required tooenable authentication in your app:</span></span>

* <span data-ttu-id="e66a6-392">inscription de votre application pour l’authentification auprès d’un fournisseur d’identité ;</span><span class="sxs-lookup"><span data-stu-id="e66a6-392">Register your app for authentication with an identity provider.</span></span>
* <span data-ttu-id="e66a6-393">configuration de votre backend App Service ;</span><span class="sxs-lookup"><span data-stu-id="e66a6-393">Configure your App Service backend.</span></span>
* <span data-ttu-id="e66a6-394">Restreindre les autorisations tooauthenticated aux utilisateurs uniquement sur hello principal de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="e66a6-394">Restrict table permissions tooauthenticated users only on hello App Service backend.</span></span>
* <span data-ttu-id="e66a6-395">Ajouter une application de tooyour code d’authentification.</span><span class="sxs-lookup"><span data-stu-id="e66a6-395">Add authentication code tooyour app.</span></span>

<span data-ttu-id="e66a6-396">Vous pouvez définir des autorisations sur l’accès aux toorestrict de tables pour des opérations spécifiques aux utilisateurs de tooonly authentifié.</span><span class="sxs-lookup"><span data-stu-id="e66a6-396">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="e66a6-397">Vous pouvez également utiliser hello SID d’un utilisateur authentifié de toomodify demandes.</span><span class="sxs-lookup"><span data-stu-id="e66a6-397">You can also use hello SID of an authenticated user toomodify requests.</span></span>  <span data-ttu-id="e66a6-398">Pour plus d’informations, consultez [prise en main d’authentification] et hello documentation de faire du Kit de développement logiciel serveur.</span><span class="sxs-lookup"><span data-stu-id="e66a6-398">For more information, review [Get started with authentication] and hello Server SDK HOWTO documentation.</span></span>

### <span data-ttu-id="e66a6-399"><a name="caching"></a>Authentification : flux serveur</span><span class="sxs-lookup"><span data-stu-id="e66a6-399"><a name="caching"></a>Authentication: Server Flow</span></span>

<span data-ttu-id="e66a6-400">Hello de code suivant démarre un processus de connexion de flux de serveur à l’aide du fournisseur de Google hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-400">hello following code starts a server flow login process using hello Google provider.</span></span>  <span data-ttu-id="e66a6-401">Configuration supplémentaire est nécessaire en raison des exigences de sécurité hello pour le fournisseur de Google hello :</span><span class="sxs-lookup"><span data-stu-id="e66a6-401">Additional configuration is required because of hello security requirements for hello Google provider:</span></span>

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

<span data-ttu-id="e66a6-402">En outre, ajoutez hello suivant classe d’activité principale méthode toohello :</span><span class="sxs-lookup"><span data-stu-id="e66a6-402">In addition, add hello following method toohello main Activity class:</span></span>

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check hello request code matches hello one we send in hello login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check hello error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

<span data-ttu-id="e66a6-403">Hello `GOOGLE_LOGIN_REQUEST_CODE` définis dans votre principal activité est utilisée pour hello `login()` (méthode) et à l’intérieur hello `onActivityResult()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="e66a6-403">hello `GOOGLE_LOGIN_REQUEST_CODE` defined in your main Activity is used for hello `login()` method and within hello `onActivityResult()` method.</span></span>  <span data-ttu-id="e66a6-404">Vous pouvez choisir n’importe quel nombre unique, tant que le même numéro hello est utilisé au sein de hello `login()` méthode et hello `onActivityResult()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="e66a6-404">You can choose any unique number, as long as hello same number is used within hello `login()` method and hello `onActivityResult()` method.</span></span>  <span data-ttu-id="e66a6-405">Si vous abstraire le code client hello dans une carte de service (comme indiqué précédemment), vous devez appeler les méthodes appropriées hello sur la carte de service hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-405">If you abstract hello client code into a service adapter (as shown earlier), you should call hello appropriate methods on hello service adapter.</span></span>

<span data-ttu-id="e66a6-406">Vous devez également le projet de hello tooconfigure pour customtabs.</span><span class="sxs-lookup"><span data-stu-id="e66a6-406">You also need tooconfigure hello project for customtabs.</span></span>  <span data-ttu-id="e66a6-407">Commencez par spécifier une URL de redirection.</span><span class="sxs-lookup"><span data-stu-id="e66a6-407">First specify a redirect-URL.</span></span>  <span data-ttu-id="e66a6-408">Ajouter hello suivant extrait trop`AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="e66a6-408">Add hello following snippet too`AndroidManifest.xml`:</span></span>

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

<span data-ttu-id="e66a6-409">Ajouter hello **redirectUriScheme** toohello `build.gradle` fichier de votre application :</span><span class="sxs-lookup"><span data-stu-id="e66a6-409">Add hello **redirectUriScheme** toohello `build.gradle` file for your application:</span></span>

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

<span data-ttu-id="e66a6-410">Enfin, ajoutez `com.android.support:customtabs:23.0.1` toohello liste de dépendances Bonjour `build.gradle` fichier :</span><span class="sxs-lookup"><span data-stu-id="e66a6-410">Finally, add `com.android.support:customtabs:23.0.1` toohello dependencies list in hello `build.gradle` file:</span></span>

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

<span data-ttu-id="e66a6-411">Obtenir les ID de hello de hello utilisateur connecté à partir d’un **MobileServiceUser** à l’aide de hello **getUserId** (méthode).</span><span class="sxs-lookup"><span data-stu-id="e66a6-411">Obtain hello ID of hello logged-in user from a **MobileServiceUser** using hello **getUserId** method.</span></span> <span data-ttu-id="e66a6-412">Pour obtenir un exemple de comment toouse perspectives toocall hello connexion asynchrone API, consultez [prise en main d’authentification].</span><span class="sxs-lookup"><span data-stu-id="e66a6-412">For an example of how toouse Futures toocall hello asynchronous login APIs, see [Get started with authentication].</span></span>

> [!WARNING]
> <span data-ttu-id="e66a6-413">Hello mentionné le modèle d’URL respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="e66a6-413">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="e66a6-414">Assurez-vous que toutes les occurrences de `{url_scheme_of_you_app}` respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="e66a6-414">Ensure that all occurrences of `{url_scheme_of_you_app}` match case.</span></span>

### <span data-ttu-id="e66a6-415"><a name="caching"></a>Mettre en cache des jetons d’authentification</span><span class="sxs-lookup"><span data-stu-id="e66a6-415"><a name="caching"></a>Cache authentication tokens</span></span>

<span data-ttu-id="e66a6-416">La mise en cache des jetons d’authentification nécessite que vous toostore hello ID d’utilisateur et le jeton d’authentification localement sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-416">Caching authentication tokens requires you toostore hello User ID and authentication token locally on hello device.</span></span> <span data-ttu-id="e66a6-417">Hello lors du prochain démarrage de l’application hello, vous vérifiez les cache hello, et si ces valeurs sont présentes, vous pouvez ignorer le journal hello dans la procédure et réalimenter client hello avec ces données.</span><span class="sxs-lookup"><span data-stu-id="e66a6-417">hello next time hello app starts, you check hello cache, and if these values are present, you can skip hello log in procedure and rehydrate hello client with this data.</span></span> <span data-ttu-id="e66a6-418">Toutefois, ces données sont sensibles, et il doit être stocké chiffrée parental en cas de téléphone de hello est volé.</span><span class="sxs-lookup"><span data-stu-id="e66a6-418">However this data is sensitive, and it should be stored encrypted for safety in case hello phone gets stolen.</span></span>  <span data-ttu-id="e66a6-419">Vous pouvez voir un exemple complet de la façon dont l’authentification toocache des jetons dans [mettre en Cache de la section des jetons d’authentification][7].</span><span class="sxs-lookup"><span data-stu-id="e66a6-419">You can see a complete example of how toocache authentication tokens in [Cache authentication tokens section][7].</span></span>

<span data-ttu-id="e66a6-420">Lorsque vous essayez de toouse un jeton expiré, vous recevez un *401 non autorisé* réponse.</span><span class="sxs-lookup"><span data-stu-id="e66a6-420">When you try toouse an expired token, you receive a *401 unauthorized* response.</span></span> <span data-ttu-id="e66a6-421">Vous pouvez gérer les erreurs d’authentification à l’aide de filtres.</span><span class="sxs-lookup"><span data-stu-id="e66a6-421">You can handle authentication errors using filters.</span></span>  <span data-ttu-id="e66a6-422">Filtres interceptent les demandes toohello principal de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="e66a6-422">Filters intercept requests toohello App Service backend.</span></span> <span data-ttu-id="e66a6-423">le code de filtrage Hello teste réponse hello pour une erreur 401, déclenche le processus de connexion hello et reprend ensuite la demande hello qui a généré hello 401.</span><span class="sxs-lookup"><span data-stu-id="e66a6-423">hello filter code tests hello response for a 401, triggers hello sign-in process, and then resumes hello request that generated hello 401.</span></span>

### <span data-ttu-id="e66a6-424"><a name="refresh"></a>Utiliser des jetons d’actualisation</span><span class="sxs-lookup"><span data-stu-id="e66a6-424"><a name="refresh"></a>Use Refresh Tokens</span></span>

<span data-ttu-id="e66a6-425">jeton Hello retourné par Azure App Service authentification et d’autorisation a une durée de vie définie d’une heure.</span><span class="sxs-lookup"><span data-stu-id="e66a6-425">hello token returned by Azure App Service Authentication and Authorization has a defined life time of one hour.</span></span>  <span data-ttu-id="e66a6-426">Après cette période, vous devez réauthentifier l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-426">After this period, you must reauthenticate hello user.</span></span>  <span data-ttu-id="e66a6-427">Si vous êtes à l’aide d’un jeton de longue durée que vous avez reçu via l’authentification de flux du client, puis vous pouvez authentifier avec l’authentification du Service application Azure et d’autorisation hello même jeton.</span><span class="sxs-lookup"><span data-stu-id="e66a6-427">If you are using a long-lived token that you have received via client-flow authentication, then you can reauthenticate with Azure App Service Authentication and Authorization using hello same token.</span></span>  <span data-ttu-id="e66a6-428">Un autre jeton Azure App Service est généré avec une nouvelle durée de vie.</span><span class="sxs-lookup"><span data-stu-id="e66a6-428">Another Azure App Service token is generated with a new lifetime.</span></span>

<span data-ttu-id="e66a6-429">Vous pouvez également inscrire hello fournisseur toouse jetons d’actualisation.</span><span class="sxs-lookup"><span data-stu-id="e66a6-429">You can also register hello provider toouse Refresh Tokens.</span></span>  <span data-ttu-id="e66a6-430">Un jeton d’actualisation n’est pas toujours disponible.</span><span class="sxs-lookup"><span data-stu-id="e66a6-430">A Refresh Token is not always available.</span></span>  <span data-ttu-id="e66a6-431">Une configuration supplémentaire est nécessaire :</span><span class="sxs-lookup"><span data-stu-id="e66a6-431">Additional configuration is required:</span></span>

* <span data-ttu-id="e66a6-432">Pour **Azure Active Directory**, configurer une clé secrète du client pour hello application Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="e66a6-432">For **Azure Active Directory**, configure a client secret for hello Azure Active Directory App.</span></span>  <span data-ttu-id="e66a6-433">Spécifier la clé secrète du client hello Bonjour Azure App Service lors de la configuration d’authentification Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e66a6-433">Specify hello client secret in hello Azure App Service when configuring Azure Active Directory Authentication.</span></span>  <span data-ttu-id="e66a6-434">Lorsque vous appelez `.login()`, transmettez `response_type=code id_token` en tant que paramètre :</span><span class="sxs-lookup"><span data-stu-id="e66a6-434">When calling `.login()`, pass `response_type=code id_token` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="e66a6-435">Pour **Google**, passez hello `access_type=offline` en tant que paramètre :</span><span class="sxs-lookup"><span data-stu-id="e66a6-435">For **Google**, pass hello `access_type=offline` as a parameter:</span></span>

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* <span data-ttu-id="e66a6-436">Pour **Account Microsoft**, sélectionnez hello `wl.offline_access` étendue.</span><span class="sxs-lookup"><span data-stu-id="e66a6-436">For **Microsoft Account**, select hello `wl.offline_access` scope.</span></span>

<span data-ttu-id="e66a6-437">toorefresh un jeton, appelez `.refreshUser()`:</span><span class="sxs-lookup"><span data-stu-id="e66a6-437">toorefresh a token, call `.refreshUser()`:</span></span>

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

<span data-ttu-id="e66a6-438">Comme meilleure pratique, créer un filtre qui détecte une réponse 401 à partir du serveur de hello et tente de jeton d’utilisateur toorefresh hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-438">As a best practice, create a filter that detects a 401 response from hello server and tries toorefresh hello user token.</span></span>

## <a name="log-in-with-client-flow-authentication"></a><span data-ttu-id="e66a6-439">Se connecter avec l’authentification de flux client</span><span class="sxs-lookup"><span data-stu-id="e66a6-439">Log in with Client-flow Authentication</span></span>

<span data-ttu-id="e66a6-440">processus général de Hello pour une connexion avec l’authentification de flux du client est la suivante :</span><span class="sxs-lookup"><span data-stu-id="e66a6-440">hello general process for logging in with client-flow authentication is as follows:</span></span>

* <span data-ttu-id="e66a6-441">Configurez l’authentification et l’autorisation Azure App Service comme vous le feriez pour l’authentification de flux client.</span><span class="sxs-lookup"><span data-stu-id="e66a6-441">Configure Azure App Service Authentication and Authorization as you would server-flow authentication.</span></span>
* <span data-ttu-id="e66a6-442">Intégrer le fournisseur d’authentification hello SDK pour l’authentification tooproduce un jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="e66a6-442">Integrate hello authentication provider SDK for authentication tooproduce an access token.</span></span>
* <span data-ttu-id="e66a6-443">Appelez hello `.login()` méthode comme suit :</span><span class="sxs-lookup"><span data-stu-id="e66a6-443">Call hello `.login()` method as follows:</span></span>

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

<span data-ttu-id="e66a6-444">Remplacez hello `onSuccess()` méthode avec tout code que vous souhaitez toouse sur une connexion réussie.</span><span class="sxs-lookup"><span data-stu-id="e66a6-444">Replace hello `onSuccess()` method with whatever code you wish toouse on a successful login.</span></span>  <span data-ttu-id="e66a6-445">Hello `{provider}` chaîne est un fournisseur valide : **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, ou **twitter**.</span><span class="sxs-lookup"><span data-stu-id="e66a6-445">hello `{provider}` string is a valid provider: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, or **twitter**.</span></span>  <span data-ttu-id="e66a6-446">Si vous avez implémenté l’authentification personnalisée, vous pouvez également utiliser balise de fournisseur d’authentification personnalisée hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-446">If you have implemented custom authentication, then you can also use hello custom authentication provider tag.</span></span>

### <span data-ttu-id="e66a6-447"><a name="adal"></a>Authentifier les utilisateurs avec hello Active Directory Authentication Library (ADAL)</span><span class="sxs-lookup"><span data-stu-id="e66a6-447"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library (ADAL)</span></span>

<span data-ttu-id="e66a6-448">Vous pouvez utiliser les utilisateurs de toosign hello Active Directory Authentication Library (ADAL) dans votre application à l’aide d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e66a6-448">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="e66a6-449">À l’aide d’une connexion de flux client est souvent préférable toousing hello `loginAsync()` méthodes qu’elle fournit un aspect d’expérience utilisateur plus natif et permet la personnalisation supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="e66a6-449">Using a client flow login is often preferable toousing hello `loginAsync()` methods as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="e66a6-450">Configurer le service principal de votre application mobile pour la connexion d’AAD par hello suivant [comment tooconfigure application de Service pour la connexion Active Directory] [ 22] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e66a6-450">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][22] tutorial.</span></span> <span data-ttu-id="e66a6-451">Assurez-vous qu’étape facultative toocomplete hello d’inscription d’une application cliente native.</span><span class="sxs-lookup"><span data-stu-id="e66a6-451">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="e66a6-452">Installez la bibliothèque ADAL en modifiant votre hello tooinclude de fichier build.gradle suivant des définitions :</span><span class="sxs-lookup"><span data-stu-id="e66a6-452">Install ADAL by modifying your build.gradle file tooinclude hello following definitions:</span></span>

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. <span data-ttu-id="e66a6-453">Ajoutez hello suite de l’application tooyour de code, la fabrication de hello suivant remplacements :</span><span class="sxs-lookup"><span data-stu-id="e66a6-453">Add hello following code tooyour application, making hello following replacements:</span></span>

* <span data-ttu-id="e66a6-454">Remplacez **INSERT-autorité-ici** avec nom hello du client hello dans lequel vous avez configuré votre application.</span><span class="sxs-lookup"><span data-stu-id="e66a6-454">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="e66a6-455">format de Hello doit être https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="e66a6-455">hello format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span>
* <span data-ttu-id="e66a6-456">Remplacez **INSERT-RESOURCE-ID-ici** avec l’ID de client hello pour le service principal de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="e66a6-456">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="e66a6-457">Vous pouvez obtenir l’ID de client hello de hello **avancé** onglet sous **paramètres Azure Active Directory** dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-457">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
* <span data-ttu-id="e66a6-458">Remplacez **INSERT-CLIENT-ID-ici** avec l’ID de client hello copié à partir de l’application cliente native de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-458">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
* <span data-ttu-id="e66a6-459">Remplacez **INSERT-REDIRECT-URI-ici** avec de votre site */.auth/login/done* point de terminaison, à l’aide du schéma HTTPS de hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-459">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="e66a6-460">Cette valeur doit être similaire trop*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="e66a6-460">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <span data-ttu-id="e66a6-461"><a name="filters"></a>Ajuster hello Communication Client-serveur</span><span class="sxs-lookup"><span data-stu-id="e66a6-461"><a name="filters"></a>Adjust hello Client-Server Communication</span></span>

<span data-ttu-id="e66a6-462">Hello connexion Client est normalement une connexion HTTP de base à l’aide de hello sous-jacent bibliothèque HTTP fourni avec hello du SDK Android.</span><span class="sxs-lookup"><span data-stu-id="e66a6-462">hello Client connection is normally a basic HTTP connection using hello underlying HTTP library supplied with hello Android SDK.</span></span>  <span data-ttu-id="e66a6-463">Il existe plusieurs raisons pour lesquelles vous souhaiteriez toochange qui :</span><span class="sxs-lookup"><span data-stu-id="e66a6-463">There are several reasons why you would want toochange that:</span></span>

* <span data-ttu-id="e66a6-464">Vous souhaitez toouse une autre HTTP bibliothèque tooadjust les délais d’attente.</span><span class="sxs-lookup"><span data-stu-id="e66a6-464">You wish toouse an alternate HTTP library tooadjust timeouts.</span></span>
* <span data-ttu-id="e66a6-465">Vous souhaitez tooprovide une barre de progression.</span><span class="sxs-lookup"><span data-stu-id="e66a6-465">You wish tooprovide a progress bar.</span></span>
* <span data-ttu-id="e66a6-466">Vous souhaitez tooadd une fonctionnalité de gestion toosupport API en-tête personnalisé.</span><span class="sxs-lookup"><span data-stu-id="e66a6-466">You wish tooadd a custom header toosupport API management functionality.</span></span>
* <span data-ttu-id="e66a6-467">Vous souhaitez toointercept une réponse indiquant un échec afin que vous pouvez implémenter la réauthentification.</span><span class="sxs-lookup"><span data-stu-id="e66a6-467">You wish toointercept a failed response so that you can implement reauthentication.</span></span>
* <span data-ttu-id="e66a6-468">Vous souhaitez toolog principales demandes tooan analytique service.</span><span class="sxs-lookup"><span data-stu-id="e66a6-468">You wish toolog backend requests tooan analytics service.</span></span>

### <a name="using-an-alternate-http-library"></a><span data-ttu-id="e66a6-469">Utilisation d’une autre bibliothèque HTTP</span><span class="sxs-lookup"><span data-stu-id="e66a6-469">Using an alternate HTTP Library</span></span>

<span data-ttu-id="e66a6-470">Appelez hello `.setAndroidHttpClientFactory()` méthode immédiatement après avoir créé votre référence de client.</span><span class="sxs-lookup"><span data-stu-id="e66a6-470">Call hello `.setAndroidHttpClientFactory()` method immediately after creating your client reference.</span></span>  <span data-ttu-id="e66a6-471">Par exemple, tooset hello connexion délai d’attente too60 secondes (au lieu de valeur par défaut de hello 10 secondes) :</span><span class="sxs-lookup"><span data-stu-id="e66a6-471">For example, tooset hello connection timeout too60 seconds (instead of hello default 10 seconds):</span></span>

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a><span data-ttu-id="e66a6-472">Implémenter un filtre de progression</span><span class="sxs-lookup"><span data-stu-id="e66a6-472">Implement a Progress Filter</span></span>

<span data-ttu-id="e66a6-473">Vous pouvez implémenter une interception de chaque demande en implémentant un élément `ServiceFilter`.</span><span class="sxs-lookup"><span data-stu-id="e66a6-473">You can implement an intercept of every request by implementing a `ServiceFilter`.</span></span>  <span data-ttu-id="e66a6-474">Par exemple, suivant de hello met à jour une barre de progression créés au préalable :</span><span class="sxs-lookup"><span data-stu-id="e66a6-474">For example, hello following updates a pre-created progress bar:</span></span>

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

<span data-ttu-id="e66a6-475">Vous pouvez attacher ce client toohello de filtre comme suit :</span><span class="sxs-lookup"><span data-stu-id="e66a6-475">You can attach this filter toohello client as follows:</span></span>

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a><span data-ttu-id="e66a6-476">Personnaliser des en-têtes de demande</span><span class="sxs-lookup"><span data-stu-id="e66a6-476">Customize Request Headers</span></span>

<span data-ttu-id="e66a6-477">Utilisez hello suivante `ServiceFilter` et joindre filtre hello Bonjour comme hello `ProgressFilter`:</span><span class="sxs-lookup"><span data-stu-id="e66a6-477">Use hello following `ServiceFilter` and attach hello filter in hello same way as hello `ProgressFilter`:</span></span>

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <span data-ttu-id="e66a6-478"><a name="conversions"></a>Configurer la sérialisation automatique</span><span class="sxs-lookup"><span data-stu-id="e66a6-478"><a name="conversions"></a>Configure Automatic Serialization</span></span>

<span data-ttu-id="e66a6-479">Vous pouvez spécifier une stratégie de conversion qui applique tooevery colonne à l’aide de hello [gson] [ 3] API.</span><span class="sxs-lookup"><span data-stu-id="e66a6-479">You can specify a conversion strategy that applies tooevery column by using hello [gson][3] API.</span></span> <span data-ttu-id="e66a6-480">bibliothèque du client Android Hello utilise [gson] [ 3] coulisses hello tooserialize Java objets tooJSON données avant l’envoi des données de hello tooAzure du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="e66a6-480">hello Android client library uses [gson][3] behind hello scenes tooserialize Java objects tooJSON data before hello data is sent tooAzure App Service.</span></span>  <span data-ttu-id="e66a6-481">Hello de code suivant utilise hello **setFieldNamingStrategy()** stratégie de méthode tooset hello.</span><span class="sxs-lookup"><span data-stu-id="e66a6-481">hello following code uses hello **setFieldNamingStrategy()** method tooset hello strategy.</span></span> <span data-ttu-id="e66a6-482">Cet exemple supprimera hello initiale (un « m »), puis en minuscules hello suivant caractères et, pour chaque nom de champ.</span><span class="sxs-lookup"><span data-stu-id="e66a6-482">This example will delete hello initial character (an "m"), and then lower-case hello next character, for every field name.</span></span> <span data-ttu-id="e66a6-483">Par exemple, il changera « mId » en « id ».</span><span class="sxs-lookup"><span data-stu-id="e66a6-483">For example, it would turn "mId" into "id."</span></span>  <span data-ttu-id="e66a6-484">Implémentez un Bonjour tooreduce de stratégie conversion besoin pour `SerializedName()` annotations sur la plupart des champs.</span><span class="sxs-lookup"><span data-stu-id="e66a6-484">Implement a conversion strategy tooreduce hello need for `SerializedName()` annotations on most fields.</span></span>

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

<span data-ttu-id="e66a6-485">Ce code doit être exécuté avant de créer une référence de client mobile à l’aide de hello **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="e66a6-485">This code must be executed before creating a mobile client reference using hello **MobileServiceClient**.</span></span>

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[prise en main d’authentification]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
