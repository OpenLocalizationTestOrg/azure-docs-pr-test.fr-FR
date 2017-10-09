---
title: "aaaAzure AD v2 Android prise en main - le programme d’installation | Documents Microsoft"
description: "Cet article explique comment une application Android peut obtenir un jeton d’accès et appeler une ou plusieurs API Microsoft Graph qui nécessitent des jetons d’accès à partir du point de terminaison Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: df2670d6d35b7a9a81158d4d7eb190540ca9c695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Configuration de votre projet

> Vous préférez toodownload de projet Android Studio de cet exemple à la place ? [Télécharger un projet](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip) et ignorer toohello [étape de Configuration](#create-an-application-express) exemple de code hello tooconfigure avant l’exécution.


### <a name="create-a-new-project"></a>Création d'un projet 
1.  Ouvrez Android Studio, puis accédez à : `File` > `New` > `New Project`
2.  Donnez un nom à votre application et cliquez sur `Next`
3.  Assurez-vous que tooselect *21 d’API ou plus récente (Android 5.0)* et cliquez sur`Next`
4.  Conservez `Empty Activity`, cliquez sur `Next`, puis sur `Finish`


### <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Ajouter un projet de tooyour hello bibliothèque d’authentification Microsoft (MSAL)
1.  Dans Android Studio, accédez à : `Gradle Scripts` > `build.gradle (Module: app)`
2.  Copie et suit hello de coller du code sous `Dependencies`:

```ruby  
compile ('com.microsoft.identity.client:msal:0.1.+') {
    exclude group: 'com.android.support', module: 'appcompat-v7'
}
compile 'com.android.volley:volley:1.0.0'
```

<!--start-collapse-->
### <a name="about-this-package"></a>À propos de ce package

package Hello ci-dessus installe hello bibliothèque d’authentification Microsoft (MSAL). MSAL gère l’acquisition, la mise en cache et l’actualisation utilisateur jetons utilisés tooaccess API protégé par le point de terminaison Azure Active Directory v2.
<!--end-collapse-->

## <a name="create-your-applications-ui"></a>Créer l’interface utilisateur de votre application

1.  Ouvrez : `activity_main.xml` sous `res` > `layout`
2.  Modifier la disposition hello activité à partir de `android.support.constraint.ConstraintLayout` ou autres trop`LinearLayout`
3.  Ajouter `android:orientation="vertical"` propriété trop`LinearLayout` nœud
4.  Copie et suit hello de coller du code dans hello `LinearLayout` nœud, en remplaçant le contenu actuel hello :

```xml
<TextView
    android:text="Welcome, "
    android:textColor="#3f3f3f"
    android:textSize="50px"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginLeft="10dp"
    android:layout_marginTop="15dp"
    android:id="@+id/welcome"
    android:visibility="invisible"/>

<Button
    android:id="@+id/callGraph"
    android:text="Call Microsoft Graph"
    android:textColor="#FFFFFF"
    android:background="#00a1f1"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="200dp"
    android:textAllCaps="false" />

<TextView
    android:text="Getting Graph Data..."
    android:textColor="#3f3f3f"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginLeft="5dp"
    android:id="@+id/graphData"
    android:visibility="invisible"/>

<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="0dip"
    android:layout_weight="1"
    android:gravity="center|bottom"
    android:orientation="vertical" >

    <Button
        android:text="Sign Out"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="15dp"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:textAllCaps="false"
        android:id="@+id/clearCache"
        android:visibility="invisible" />
</LinearLayout>
```

