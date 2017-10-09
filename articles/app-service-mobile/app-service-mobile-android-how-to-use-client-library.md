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
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a>Comment toouse hello Azure Mobile Apps SDK pour Android

Ce guide vous explique comment toouse hello client Android SDK pour applications mobiles tooimplement les scénarios courants, tels que :

* Interrogation des données (insertion, mise à jour et suppression).
* Authentification.
* Gestion des erreurs.
* Personnalisation de client de hello.

Ce guide se concentre sur hello côté client SDK Android.  toolearn savoir plus sur hello des kits de développement logiciel côté serveur pour les applications mobiles, consultez [fonctionne avec le serveur principal .NET SDK] [ 10] ou [comment toouse hello Node.js principal SDK] [ 11].

## <a name="reference-documentation"></a>Documentation de référence

Vous pouvez trouver hello [référence de l’API de Javadocs] [ 12] pour la bibliothèque de client Android hello sur GitHub.

## <a name="supported-platforms"></a>Plateformes prises en charge

Hello Azure Mobile Apps SDK pour Android prend en charge les niveaux d’API 19 et 24 (KitKat via la commande) pour le téléphone et tablette facteurs de forme.  L’authentification, utilise en particulier, d’informations d’identification de toogather approche commune web framework.  L’authentification de flux serveur ne fonctionne pas avec les appareils compacts comme les montres.

## <a name="setup-and-prerequisites"></a>Configuration et conditions préalables

Hello complète [démarrage rapide des applications mobiles](app-service-mobile-android-get-started.md) didacticiel.  Cette tâche garantit que toutes les conditions préalables au développement d’Azure Mobile Apps ont été remplies.  Hello démarrage rapide vous aide également à configurer votre compte et de créer votre première principal de l’application Mobile.

Si vous décidez de toocomplete pas le didacticiel de démarrage rapide hello, procédez hello tâches suivantes :

* [créer un service principal de l’application Mobile] [ 13] toouse avec votre application Android.
* Dans Android Studio, [mise à jour hello Gradle les fichiers de build](#gradle-build).
* [activer les autorisations Internet](#enable-internet).

### <a name="gradle-build"></a>Hello Gradle générer fichier de mise à jour

Modifiez les deux fichiers **build.gradle** :

1. Ajouter ce code toohello *projet* niveau **build.gradle** fichier hello *buildscript* balise :

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. Ajouter ce code toohello *Module application* niveau **build.gradle** fichier hello *dépendances* balise :

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    Actuellement la version la plus récente hello est 3.3.0. les versions Hello pris en charge sont répertoriées [sur bintray][14].

### <a name="enable-internet"></a>activer les autorisations Internet.

tooaccess Azure, votre application doit avoir d’autorisations INTERNET hello activée. S’il n’est pas déjà activé, ajouter hello suivant la ligne de code tooyour **AndroidManifest.xml** fichier :

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a>Créer une connexion cliente

Les applications mobiles Azure fournit quatre fonctions tooyour des applications mobiles :

* Accès aux données et synchronisation hors connexion avec un service Azure Mobile Apps.
* Appeler les API personnalisées écrites avec hello Azure Mobile Apps Server SDK.
* Authentification avec l’authentification et l’autorisation Azure App Service.
* Inscription de notifications Push avec Notification Hubs.

Pour chacune de ces fonctions, vous devez créer un objet `MobileServiceClient` au préalable.  Seul un objet `MobileServiceClient` doit être créé au sein de votre client mobile (autrement dit, il doit être un modèle de Singleton).  toocreate un `MobileServiceClient` objet :

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

Hello `<MobileAppUrl>` est une chaîne ou un objet de l’URL qui pointe backend mobile de tooyour.  Si vous utilisez Azure App Service toohost votre serveur principal mobile, puis assurez-vous utiliser hello sécurisé `https://` version de l’URL de hello.

client de Hello requiert également accès toohello activité ou contexte - hello `this` paramètre dans l’exemple de hello.  Hello MobileServiceClient construction doit se produire dans hello `onCreate()` méthode Hello activité référencée Bonjour `AndroidManifest.xml` fichier.

Nous vous recommandons d’extraire la communication du serveur dans sa propre classe (modèle singleton).  Dans ce cas, vous devez passer hello activité au sein de hello constructeur tooappropriately configurer le service de hello.  Par exemple :

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

Vous pouvez maintenant appeler `AzureServiceAdapter.Initialize(this);` Bonjour `onCreate()` méthode de votre activité principale.  Toutes les autres méthodes nécessitant le client d’accès toohello utilisent `AzureServiceAdapter.getInstance();` tooobtain une carte de service référence toohello.

## <a name="data-operations"></a>Opérations de données

core Hello Hello Azure Mobile Apps SDK est toodata d’accès tooprovide stockée dans SQL Azure sur le serveur principal de l’application Mobile hello.  Vous pouvez accéder à ces données à l’aide de classes fortement typées (recommandé) ou de requêtes non typées (déconseillé).  bloc Hello de cette section porte sur l’utilisation des classes fortement typées.

### <a name="define-client-data-classes"></a>Définir des classes de données client

tooaccess des données à partir des tables de SQL Azure, définir des classes de données de client qui correspondent toohello des tables dans le service principal de l’application Mobile hello. Exemples de cette rubrique supposent une table nommée **MyDataTable**, qui a hello suivant des colonnes :

* id
* text
* terminé

Hello correspondant objet côté client typé réside dans un fichier appelé **MyDataTable.java**:

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

Incluez des méthodes getter et setter pour chaque champ que vous ajoutez.  Si votre table SQL Azure contient plus de colonnes, vous devez ajouter la classe toothis champs correspondante de hello.  Par exemple, si hello DTO (objet de transfert de données) a une colonne d’entiers priorité, puis vous pouvez ajouter ce champ, ainsi que ses méthodes getter et setter :

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

toolearn toocreate des tables supplémentaires dans votre service principal Mobile Apps, voir [Comment : définir un contrôleur de table] [ 15] (principal .NET) ou [définissent des Tables à l’aide d’un schéma dynamique] [ 16] (Node.js principal).

Une table de serveur principal les applications mobiles Azure définit cinq champs spéciaux, dont quatre sont tooclients disponibles :

* `String id`: hello ID global unique pour l’enregistrement de hello.  Comme meilleure pratique, rendre hello id hello chaîne représentant un [UUID] [ 17] objet.
* `DateTimeOffset updatedAt`: hello date/heure de dernière mise à jour de hello.  champ d’updatedAt Hello est définie par le serveur de hello et ne doit jamais être définie par votre code client.
* `DateTimeOffset createdAt`: hello date/heure de cet objet hello a été créé.  champ de créédans Hello est définie par le serveur de hello et ne doit jamais être définie par votre code client.
* `byte[] version`: Version de hello normalement représenté sous forme de chaîne, est également définie par le serveur de hello.
* `boolean deleted`: Indique que l’enregistrement de hello a été supprimé mais ne pas encore été purgé.  N’utilisez pas `deleted` en tant que propriété dans votre classe.

Hello `id` champ est obligatoire.  Hello `updatedAt` champ et `version` sont utilisés pour la synchronisation hors connexion (pour la résolution de conflit et de synchronisation incrémentielle respectivement).  Hello `createdAt` champ est un champ de référence et n’est pas utilisé par le client de hello.  les noms de Hello sont des noms de « entre simultanée » des propriétés de hello et ne sont pas réglables.  Toutefois, vous pouvez créer un mappage entre les hello noms « entre simultanée » à l’aide de hello [gson] [ 3] bibliothèque.  Par exemple :

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

### <a name="create-a-table-reference"></a>Créer une référence de table

tooaccess une table, commencez par créer un [MobileServiceTable] [ 8] objet en appelant hello **getTable** méthode sur hello [MobileServiceClient][9].  Cette méthode comporte deux surcharges :

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

Bonjour, suivant le code, **mClient** est un objet de MobileServiceClient tooyour référence.  la première surcharge de Hello est utilisée où nom de la classe hello et le nom de la table hello même hello et hello un sert Bonjour démarrage rapide :

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

Hello deuxième surcharge est utilisée lorsque le nom de la table hello est différent du nom de classe hello : hello premier paramètre est nom de la table hello.

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <a name="query"></a>Interroger une table de serveur principal

Commencez par obtenir une référence de table.  Ensuite, exécutez une requête sur la référence de table hello.  Une requête est une combinaison des éléments suivants :

* Une [clause de filtre](#filtering) `.where()`.
* Une [clause de classement](#sorting) `.orderBy()`.
* Une [clause de sélection de champ](#selection) `.select()`.
* Un élément `.skip()` et `.top()` pour les [résultats paginés](#paging).

les clauses Hello doivent être présentés dans hello précédant l’ordre.

### <a name="filter"></a> Filtrage des résultats

Hello la forme générale d’une requête est :

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

Hello exemple précédent retourne tous les résultats (haut toohello taille de page maximale définie par le serveur de hello).  Hello `.execute()` méthode s’exécute les requêtes hello sur hello principal.  requête Hello est converti tooan [OData v3] [ 19] requête avant transmission toohello Mobile Apps principal.  À la réception, principal des applications mobiles hello convertit les requêtes hello dans une instruction SQL avant de l’exécuter sur l’instance de SQL Azure hello.  Étant donné que l’activité réseau prend du temps, hello `.execute()` méthode retourne un [ `ListenableFuture<E>` ] [ 18].

### <a name="filtering"></a>Filtrer les données renvoyées

Hello après l’exécution de la requête retourne tous les éléments à partir de hello **ToDoItem** table dans laquelle **complète** est égal à **false**.

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

**mToDoTable** est hello toohello service mobile table de référence que nous avons créé précédemment.

Définir un filtre à l’aide de hello **où** appel de méthode sur la référence de table hello. Hello **où** méthode est suivie par une **champ** méthode suivie par une méthode qui spécifie le prédicat de logique hello. Méthodes de prédicat possibles : **eq** (égal à), **ne** (différent de), **gt** (supérieur à), **ge** (supérieur ou égal à), **lt** (inférieur à), **le** (inférieur ou égal à). Ces méthodes vous permettent de comparer le nombre et les valeurs de toospecific des champs de chaîne.

Vous pouvez activer des filtres sur les dates. Hello méthodes suivantes vous permettent de comparer le champ de date complète hello ou des parties de date de hello : **année**, **mois**, **jour**, **heure**, **minute**, et **deuxième**. Hello exemple suivant ajoute un filtre pour les éléments dont *date d’échéance* est égal à 2013.

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

Hello méthodes suivantes prennent en charge des filtres complexes sur des champs de chaîne : **startsWith**, **endsWith**, **concat**, **sous-chaîne**, **indexOf**, **remplacer**, **toLower**, **toUpper**, **trim**, et  **longueur**. Hello suivant l’exemple de filtre de lignes de la table où hello *texte* colonne commence par « PRI0 ».

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

Hello suivant les méthodes d’opérateur est pris en charge sur les champs numériques : **ajouter**, **sub**, **mul**, **div**, **mod**, **floor**, **plafond**, et **arrondir**. Hello suivant l’exemple de filtre de lignes de la table où hello **durée** est un nombre pair.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

Vous pouvez combiner les prédicats avec les méthodes logiques **and**, **or** et **not**. Bonjour à l’exemple suivant combine deux Hello précédant les exemples.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

Regrouper et imbriquer des opérateurs logiques :

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

Pour plus d’informations détaillées de discussion et des exemples de filtrage, consultez [exploration richesse hello du modèle de requête cliente Android hello][20].

### <a name="sorting"></a>Trier les données renvoyées

Hello de code suivant retourne tous les éléments d’une table de **ToDoItems** triée par ordre croissant par hello *texte* champ. *mToDoTable* est hello toohello principal table de référence que vous avez créé précédemment :

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

Hello du premier paramètre de hello **orderBy** méthode est un nom de toohello égal de chaîne du champ hello sur le toosort. deuxième paramètre de Hello utilise hello **QueryOrder** toospecify d’énumération si toosort par ordre croissant ou décroissant.  Si vous filtrez à l’aide de hello ***où*** (méthode), hello ***où*** méthode doit être appelée avant hello ***orderBy*** (méthode).

### <a name="selection"></a>Sélectionner des colonnes spécifiques

Hello de code suivant illustre comment tooreturn tous les éléments d’une table de **ToDoItems**, mais n’affiche que hello **complète** et **texte** champs. **mToDoTable** est hello toohello principal table de référence que nous avons créé précédemment.

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

fonction de Hello paramètres toohello select sont des noms de chaîne hello hello du colonnes de table que vous souhaitez tooreturn.  Hello **sélectionnez** méthode doit toofollow des méthodes, telles que **où** et **orderBy**. Elle peut être suivie de méthodes de pagination telles que **skip** et **top**.

### <a name="paging"></a>Renvoyer les données de pages

Les données sont **TOUJOURS** renvoyées dans les pages.  nombre maximal de Hello d’enregistrements renvoyés est définie par le serveur de hello.  Si le client de hello demande plus d’enregistrements, serveur de hello retourne le nombre maximal de hello d’enregistrements.  Par défaut, la taille de page maximale de hello sur le serveur hello est 50 enregistrements.

Hello premier exemple montre comment tooselect hello supérieur cinq éléments à partir d’une table. requête de Hello retourne des éléments de hello dans une table de **ToDoItems**. **mToDoTable** est hello toohello principal table de référence que vous avez créé précédemment :

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

Voici une requête qu’ignore hello cinq premiers éléments, puis retourne hello cinq suivant :

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

Si vous le souhaitez tooget tous les enregistrements dans une table, implémentent tooiterate du code sur toutes les pages :

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

Une demande pour tous les enregistrements à l’aide de cette méthode crée un minimum de deux requêtes toohello Mobile Apps principal.

> [!TIP]
> En choisissant l’option taille de page de droite hello est un équilibre entre l’utilisation de la mémoire pendant la demande de hello, l’utilisation de la bande passante et retard dans la réception des données de salutation complètement.  la valeur par défaut de Hello (50 enregistrements) est adaptée à tous les appareils.  Si vous utilisez exclusivement sur les périphériques de mémoire supérieure, augmenter jusqu'à too500.  Nous avons constaté que taille de la page hello augmenter au-delà de 500 enregistre les résultats dans des délais inacceptables et les problèmes de mémoire de grande taille.

### <a name="chaining"></a>Procédure de concaténation de méthodes de requête

les méthodes Hello utilisées lors de l’interrogation des tables du serveur principal peuvent être concaténées. Chaînage des propriétés de la requête de méthodes vous permet de tooselect des colonnes spécifiques de lignes filtrées triées et réserve paginées. Vous pouvez créer des filtres logiques complexes.  Chaque méthode de requête retourne un objet de requête. série de hello tooend de méthodes et de requête d’exécution réellement hello, appel hello **exécuter** (méthode). Par exemple :

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

Hello chaînés requête méthodes doivent être classées comme suit :

1. Filtrage des méthodes (**where**).
2. Tri des méthodes (**orderBy**).
3. Sélection des méthodes (**select**).
4. pagination des méthodes (**skip** et **top**).

## <a name="binding"></a>Lier l’interface utilisateur de données toohello

La liaison des données nécessite trois composants :

* source de données Hello
* disposition de l’écran Hello
* adaptateur Hello que ties hello deux ensemble.

Dans notre exemple de code, nous retournent des données de hello à partir de la table de Mobile applications SQL Azure hello **ToDoItem** dans un tableau. Cette activité est un cas de figure très courant pour les applications de données.  Requêtes de base de données retournent souvent une collection de lignes qui hello client obtient dans une liste ou un tableau. Dans cet exemple, le tableau de hello est source de données hello.  code de Hello spécifie une disposition de l’écran qui définit la vue hello de données hello qui s’affiche sur l’appareil de hello.  Hello deux sont liés avec un adaptateur, dans ce code est une extension de hello **ArrayAdapter&lt;ToDoItem&gt;**  classe.

#### <a name="layout"></a>Définir hello mise en page

mise en page Hello est définie par plusieurs extraits de code XML. Étant donné une mise en page existante, hello suivant code représente hello **ListView** nous souhaitons toopopulate avec nos données de serveur.

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

Bonjour précédant le code, hello *listitem* attribut spécifie l’id hello de disposition hello pour une ligne spécifique dans la liste de hello. Ce code spécifie une case à cocher et son texte associé et est instancié une fois pour chaque élément de liste de hello. Cette mise en page ne s’affiche pas hello **id** champ et une mise en page plus complexe seraient spécifier des champs supplémentaires dans l’affichage de hello. Ce code est Bonjour **row_list_to_do.xml** fichier.

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

#### <a name="adapter"></a>Définir l’adaptateur hello
Étant donné que la source de données hello de notre vue est un tableau de **ToDoItem**, nous sous-classe notre adaptateur à partir d’un **ArrayAdapter&lt;ToDoItem&gt;**  classe. Cette sous-classe génère une vue pour chaque **ToDoItem** à l’aide de hello **row_list_to_do** mise en page.  Dans notre code, nous définissons hello suivant de classe est une extension de hello **ArrayAdapter&lt;E&gt;**  classe :

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

Remplacer les adaptateurs hello **getView** (méthode). Par exemple :

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

Nous créons une instance de cette classe dans notre activité, comme suit :

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

Hello deuxième paramètre toohello ToDoItemAdapter constructeur est une disposition de toohello de référence. Nous pouvons maintenant d’instancier hello **ListView** et affecter hello adaptateur toohello **ListView**.

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <a name="use-adapter"></a>Utilisez hello adaptateur tooBind toohello l’interface utilisateur

Vous êtes maintenant prêt toouse la liaison de données. Hello de code suivant montre comment tooget des éléments dans la table de hello et de remplissages hello adaptateur local avec hello articles retourné.

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

Appeler l’adaptateur hello chaque fois que vous modifiez hello **ToDoItem** table. Comme les modifications se font enregistrement par enregistrement, vous ne gérez qu’une seule ligne, et non une collection. Lorsque vous insérez un élément, appelez hello **ajouter** méthode sur hello adaptateur ; lors de la suppression, appelez hello **supprimer** (méthode).

Vous trouverez un exemple complet dans hello [projet de démarrage rapide Android][21].

## <a name="inserting"></a>Insérer des données dans le back-end hello

Instancier une instance de hello *ToDoItem* classe et définissez ses propriétés.

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

Utilisez ensuite **insert()** tooinsert un objet :

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

Hello retourné correspond à des entités données hello insérées dans la table principale de hello, ID de hello inclus et d’autres valeurs (par exemple hello `createdAt`, `updatedAt`, et `version` champs) définie sur hello principal.

Les tables Mobile Apps nécessitent une colonne de clé primaire nommée **id**. Cette colonne doit être une chaîne. valeur par défaut de Hello hello colonne d’ID est un GUID.  Vous pouvez fournir d’autres valeurs uniques, telles que des adresses de messagerie ou des noms d’utilisateurs. Lorsqu’une valeur d’ID de chaîne n’est pas fournie pour un enregistrement inséré, hello principal génère un nouveau GUID.

Fournissent des valeurs d’ID de chaîne hello suivant avantages :

* ID peuvent être générés sans passer d’une base de données toohello aller-retour.
* Les enregistrements sont toomerge plus facile à partir de différentes tables ou bases de données.
* Les valeurs d’ID s’intègrent mieux à la logique d’une application.

Les valeurs d’ID de chaîne sont **obligatoires** pour la prise en charge de la synchronisation hors connexion.  Vous ne pouvez pas modifier un Id une fois qu’il est stocké dans la base de données principale hello.

## <a name="updating"></a>Mettre à jour des données dans une application mobile

tooupdate des données dans une table, passez hello nouvel objet toohello **update()** (méthode).

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

Dans cet exemple, *élément* est une ligne de tooa référence Bonjour *ToDoItem* table, ce qui a été tooit de certaines modifications apportées.  ligne Hello avec hello même **id** est mis à jour.

## <a name="deleting"></a>Supprimer des données dans une application mobile

Hello suivant de code montre comment toodelete des données à partir d’une table en spécifiant hello objet de données.

```java
mToDoTable
    .delete(item);
```

Vous pouvez également supprimer un élément en spécifiant hello **id** champ hello ligne toodelete.

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <a name="lookup"></a>Rechercher un élément spécifique par ID

Rechercher un élément avec un spécifique **id** champ hello **lookUp()** méthode :

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <a name="untyped"></a>Procédure : utilisation de données non typées

modèle de programmation non typé Hello donne exacte contrôler la sérialisation JSON.  Il existe quelques scénarios courants où vous pouvez toouse un modèle de programmation non typé. Par exemple, si votre table principale contient de nombreuses colonnes et que vous ne devez tooreference un sous-ensemble de colonnes de hello.  modèle de type Hello nécessite toodefine toutes les colonnes hello définis dans le back-end des applications mobiles hello dans votre classe de données.  La plupart des appels d’API pour accéder aux données de hello est similaire toohello tapé des appels de programmation. Hello principale différence est que dans le modèle non typée de hello vous appelez des méthodes sur hello **MobileServiceJsonTable** objet au lieu de hello **MobileServiceTable** objet.

### <a name="json_instance"></a>Créer une instance de table non typée

Toohello similaire tapé le modèle, vous commencez par obtenir une référence de table, mais dans ce cas, il est un **MobileServicesJsonTable** objet. Obtenir la référence de hello en appelant hello **getTable** méthode sur une instance du client de hello :

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

Une fois que vous avez créé une instance de hello **MobileServiceJsonTable**, il a hello virtuellement même API disponible en tant que modèle de programmation typée hello. Dans certains cas, les méthodes hello prennent un paramètre non typé au lieu d’un paramètre typé.

### <a name="json_insert"></a>Insérer une table non typée
Hello suivant de code montre comment toodo une instruction insert. première étape Hello est toocreate un [JsonObject][1], qui fait partie de hello [gson] [ 3] bibliothèque.

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

Ensuite, utilisez **insert()** objet non typé de tooinsert hello dans la table de hello.

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

Si vous devez tooget hello ID objet de hello inséré, utilisez hello **getAsJsonPrimitive()** (méthode).

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <a name="json_delete"></a>Supprimer d’une table non typée
Hello de code suivant montre comment toodelete une instance, hello dans ce cas, la même instance d’un **JsonObject** qui a été créé avant de hello *insérer* exemple. code de Hello est hello même chose avec hello tapé du cas, mais la méthode hello possède une signature différente, car elle fait référence à un **JsonObject**.

```java
mToDoTable
    .delete(insertedItem);
```

Vous pouvez aussi directement supprimer une instance avec son ID :

```java
mToDoTable.delete(ID);
```

### <a name="json_get"></a>Renvoyer toutes les lignes d’une table non typée
Hello suivant de code montre comment tooretrieve une table entière. Étant donné que vous utilisez un tableau JSON, vous pouvez sélectivement récupérer uniquement certaines colonnes de la table hello.

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

Hello même ensemble de filtrage, le filtrage et la pagination des méthodes qui sont disponibles pour le modèle de type hello sont disponibles pour les modèles non typé hello.

## <a name="offline-sync"></a>Implémenter la synchronisation hors connexion

Bonjour Azure Mobile Apps Client SDK implémente également une synchronisation hors connexion de données à l’aide un toostore de la base de données SQLite une copie des données de serveur hello localement.  Opérations effectuées sur une table en mode hors connexion ne nécessitent pas de connectivité mobile toowork.  Synchronisation hors connexion contribue à la résilience et les performances à des frais de hello d’une logique plus complexe pour la résolution de conflit.  Bonjour Azure Mobile Apps Client SDK implémente hello suivant de fonctionnalités :

* Synchronisation incrémentielle : seuls les enregistrements nouveaux et mis à jour sont téléchargés, ce qui permet d’économiser de la bande passante et de la mémoire.
* L’accès concurrentiel optimiste : Les opérations sont supposées toosucceed.  Résolution des conflits est différée jusqu'à ce que les mises à jour sont effectuées sur le serveur de hello.
* Résolution des conflits : hello que SDK détecte une modification en conflit a été effectuée sur le serveur de hello et fournit des raccordements utilisateur de hello tooalert.
* Suppression réversible : Enregistrements supprimés sont marquées comme supprimées, ce qui permet d’autres tooupdate périphériques leur cache hors connexion.

### <a name="initialize-offline-sync"></a>Initialiser la synchronisation hors connexion

Chaque table hors connexion doit être défini dans le cache hors connexion hello avant des utiliser.  Normalement, la définition de la table est effectuée immédiatement après la création de hello du client de hello :

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

### <a name="obtain-a-reference-toohello-offline-cache-table"></a>Obtenir une référence de toohello Table de Cache hors connexion

Pour une table en ligne, vous utilisez `.getTable()`.  Pour une table hors connexion, utilisez `.getSyncTable()` :

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

Tous les hello des méthodes qui sont disponibles pour les tables en ligne (y compris le filtrage, tri, la pagination, insertion de données, mise à jour des données et la suppression des données) fonctionnent aussi bien sur les tables en ligne et hors connexion.

### <a name="synchronize-hello-local-offline-cache"></a>Synchroniser hello Cache Local en mode hors connexion

La synchronisation est dans un contrôle hello de votre application.  Voici un exemple de méthode de synchronisation :

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

Si un nom de requête est fourni toohello `.pull(query, queryname)` (méthode), puis synchronisation incrémentielle est utilisée tooreturn uniquement les enregistrements qui ont été créés ou modifiés depuis l’extraction de hello dernier terminé avec succès.

### <a name="handle-conflicts-during-offline-synchronization"></a>Gérer les conflits lors de la synchronisation hors connexion

Si un conflit se produit pendant une opération `.push()`, une exception `MobileServiceConflictException` est levée.   élément de serveur émis Hello est incorporé dans l’exception de hello et peuvent être récupéré par `.getItem()` sur l’exception de hello.  Ajuster push hello en appelant hello éléments suivants de l’objet de MobileServiceSyncContext hello :

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

Une fois que tous les conflits sont marquées comme vous le souhaitez, appelez `.push()` tooresolve à nouveau toutes les hello est en conflit.

## <a name="custom-api"></a>Appeler une API personnalisée

Une API personnalisée vous permet de toodefine points de terminaison personnalisés qui exposent les fonctionnalités de serveur qui ne pas mapper tooan insérer, mettre à jour, supprimer ou opération de lecture. En utilisant une API personnalisée, vous pouvez exercer davantage de contrôle sur la messagerie, notamment lire et définir des en-têtes de message HTTP et définir un format de corps de message autre que JSON.

À partir d’un client Android, vous appelez hello **invokeApi** méthode toocall hello API point de terminaison personnalisé. Hello suivant montre comment toocall un point de terminaison API nommé **completeAll**, qui retourne une classe de collection nommée **MarkAllResult**.

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

Hello **invokeApi** méthode est appelée sur le client hello, qui envoie un message demande toohello une nouvelle API personnalisée. résultat de Hello retourné par l’API personnalisée hello s’affiche dans une boîte de dialogue de message, comme des erreurs. Autres versions de **invokeApi** vous permettent d’envoyer un objet dans le corps de la demande hello si vous le souhaitez, spécifier la méthode hello HTTP et envoyer des paramètres de requête avec la demande de hello. Des versions non typées de la méthode **invokeApi** sont également fournies.

## <a name="authentication"></a>Ajouter une application de tooyour d’authentification

Didacticiels déjà décrivent en détail comment tooadd ces fonctionnalités.

App Service prend en charge [l’authentification des utilisateurs d’applications](app-service-mobile-android-get-started-users.md) via divers fournisseurs d’identité externes : Facebook, Google, compte Microsoft, Twitter et Azure Active Directory. Vous pouvez définir des autorisations sur l’accès aux toorestrict de tables pour des opérations spécifiques aux utilisateurs de tooonly authentifié. Vous pouvez également utiliser l’identité hello des règles d’autorisation de tooimplement utilisateurs authentifiés dans votre serveur principal.

Deux flux d’authentification sont pris en charge : un flux **serveur** et un flux **client**. flux de serveur Hello fournit expérience d’authentification la plus simple hello, car il repose sur l’interface web hello identité fournisseurs.  Aucun SDK supplémentaires n’est l’authentification du serveur flux tooimplement requis. L’authentification du serveur flux ne fournit pas d’une intégration complète dans les appareils mobiles hello et est recommandée uniquement pour la preuve de concept.

flux Hello du client permet une intégration plus étroite avec les fonctionnalités spécifiques au périphérique tels que l’authentification unique sur car elle s’appuie sur les kits de développement logiciel fournis par le fournisseur d’identité hello.  Par exemple, vous pouvez intégrer hello SDK Facebook dans votre application mobile.  les clients mobiles Hello échange dans l’application de Facebook hello et confirme l’authentification avant d’échanger tooyour arrière des applications mobiles.

Quatre étapes sont tooenable requis dans votre application :

* inscription de votre application pour l’authentification auprès d’un fournisseur d’identité ;
* configuration de votre backend App Service ;
* Restreindre les autorisations tooauthenticated aux utilisateurs uniquement sur hello principal de Service d’applications.
* Ajouter une application de tooyour code d’authentification.

Vous pouvez définir des autorisations sur l’accès aux toorestrict de tables pour des opérations spécifiques aux utilisateurs de tooonly authentifié. Vous pouvez également utiliser hello SID d’un utilisateur authentifié de toomodify demandes.  Pour plus d’informations, consultez [prise en main d’authentification] et hello documentation de faire du Kit de développement logiciel serveur.

### <a name="caching"></a>Authentification : flux serveur

Hello de code suivant démarre un processus de connexion de flux de serveur à l’aide du fournisseur de Google hello.  Configuration supplémentaire est nécessaire en raison des exigences de sécurité hello pour le fournisseur de Google hello :

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

En outre, ajoutez hello suivant classe d’activité principale méthode toohello :

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

Hello `GOOGLE_LOGIN_REQUEST_CODE` définis dans votre principal activité est utilisée pour hello `login()` (méthode) et à l’intérieur hello `onActivityResult()` (méthode).  Vous pouvez choisir n’importe quel nombre unique, tant que le même numéro hello est utilisé au sein de hello `login()` méthode et hello `onActivityResult()` (méthode).  Si vous abstraire le code client hello dans une carte de service (comme indiqué précédemment), vous devez appeler les méthodes appropriées hello sur la carte de service hello.

Vous devez également le projet de hello tooconfigure pour customtabs.  Commencez par spécifier une URL de redirection.  Ajouter hello suivant extrait trop`AndroidManifest.xml`:

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

Ajouter hello **redirectUriScheme** toohello `build.gradle` fichier de votre application :

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

Enfin, ajoutez `com.android.support:customtabs:23.0.1` toohello liste de dépendances Bonjour `build.gradle` fichier :

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

Obtenir les ID de hello de hello utilisateur connecté à partir d’un **MobileServiceUser** à l’aide de hello **getUserId** (méthode). Pour obtenir un exemple de comment toouse perspectives toocall hello connexion asynchrone API, consultez [prise en main d’authentification].

> [!WARNING]
> Hello mentionné le modèle d’URL respecte la casse.  Assurez-vous que toutes les occurrences de `{url_scheme_of_you_app}` respectent la casse.

### <a name="caching"></a>Mettre en cache des jetons d’authentification

La mise en cache des jetons d’authentification nécessite que vous toostore hello ID d’utilisateur et le jeton d’authentification localement sur l’appareil de hello. Hello lors du prochain démarrage de l’application hello, vous vérifiez les cache hello, et si ces valeurs sont présentes, vous pouvez ignorer le journal hello dans la procédure et réalimenter client hello avec ces données. Toutefois, ces données sont sensibles, et il doit être stocké chiffrée parental en cas de téléphone de hello est volé.  Vous pouvez voir un exemple complet de la façon dont l’authentification toocache des jetons dans [mettre en Cache de la section des jetons d’authentification][7].

Lorsque vous essayez de toouse un jeton expiré, vous recevez un *401 non autorisé* réponse. Vous pouvez gérer les erreurs d’authentification à l’aide de filtres.  Filtres interceptent les demandes toohello principal de Service d’applications. le code de filtrage Hello teste réponse hello pour une erreur 401, déclenche le processus de connexion hello et reprend ensuite la demande hello qui a généré hello 401.

### <a name="refresh"></a>Utiliser des jetons d’actualisation

jeton Hello retourné par Azure App Service authentification et d’autorisation a une durée de vie définie d’une heure.  Après cette période, vous devez réauthentifier l’utilisateur de hello.  Si vous êtes à l’aide d’un jeton de longue durée que vous avez reçu via l’authentification de flux du client, puis vous pouvez authentifier avec l’authentification du Service application Azure et d’autorisation hello même jeton.  Un autre jeton Azure App Service est généré avec une nouvelle durée de vie.

Vous pouvez également inscrire hello fournisseur toouse jetons d’actualisation.  Un jeton d’actualisation n’est pas toujours disponible.  Une configuration supplémentaire est nécessaire :

* Pour **Azure Active Directory**, configurer une clé secrète du client pour hello application Active Directory de Azure.  Spécifier la clé secrète du client hello Bonjour Azure App Service lors de la configuration d’authentification Azure Active Directory.  Lorsque vous appelez `.login()`, transmettez `response_type=code id_token` en tant que paramètre :

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Pour **Google**, passez hello `access_type=offline` en tant que paramètre :

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Pour **Account Microsoft**, sélectionnez hello `wl.offline_access` étendue.

toorefresh un jeton, appelez `.refreshUser()`:

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

Comme meilleure pratique, créer un filtre qui détecte une réponse 401 à partir du serveur de hello et tente de jeton d’utilisateur toorefresh hello.

## <a name="log-in-with-client-flow-authentication"></a>Se connecter avec l’authentification de flux client

processus général de Hello pour une connexion avec l’authentification de flux du client est la suivante :

* Configurez l’authentification et l’autorisation Azure App Service comme vous le feriez pour l’authentification de flux client.
* Intégrer le fournisseur d’authentification hello SDK pour l’authentification tooproduce un jeton d’accès.
* Appelez hello `.login()` méthode comme suit :

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

Remplacez hello `onSuccess()` méthode avec tout code que vous souhaitez toouse sur une connexion réussie.  Hello `{provider}` chaîne est un fournisseur valide : **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, ou **twitter**.  Si vous avez implémenté l’authentification personnalisée, vous pouvez également utiliser balise de fournisseur d’authentification personnalisée hello.

### <a name="adal"></a>Authentifier les utilisateurs avec hello Active Directory Authentication Library (ADAL)

Vous pouvez utiliser les utilisateurs de toosign hello Active Directory Authentication Library (ADAL) dans votre application à l’aide d’Azure Active Directory. À l’aide d’une connexion de flux client est souvent préférable toousing hello `loginAsync()` méthodes qu’elle fournit un aspect d’expérience utilisateur plus natif et permet la personnalisation supplémentaire.

1. Configurer le service principal de votre application mobile pour la connexion d’AAD par hello suivant [comment tooconfigure application de Service pour la connexion Active Directory] [ 22] didacticiel. Assurez-vous qu’étape facultative toocomplete hello d’inscription d’une application cliente native.
2. Installez la bibliothèque ADAL en modifiant votre hello tooinclude de fichier build.gradle suivant des définitions :

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

1. Ajoutez hello suite de l’application tooyour de code, la fabrication de hello suivant remplacements :

* Remplacez **INSERT-autorité-ici** avec nom hello du client hello dans lequel vous avez configuré votre application. format de Hello doit être https://login.microsoftonline.com/contoso.onmicrosoft.com.
* Remplacez **INSERT-RESOURCE-ID-ici** avec l’ID de client hello pour le service principal de votre application mobile. Vous pouvez obtenir l’ID de client hello de hello **avancé** onglet sous **paramètres Azure Active Directory** dans le portail de hello.
* Remplacez **INSERT-CLIENT-ID-ici** avec l’ID de client hello copié à partir de l’application cliente native de hello.
* Remplacez **INSERT-REDIRECT-URI-ici** avec de votre site */.auth/login/done* point de terminaison, à l’aide du schéma HTTPS de hello. Cette valeur doit être similaire trop*https://contoso.azurewebsites.net/.auth/login/done*.

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

## <a name="filters"></a>Ajuster hello Communication Client-serveur

Hello connexion Client est normalement une connexion HTTP de base à l’aide de hello sous-jacent bibliothèque HTTP fourni avec hello du SDK Android.  Il existe plusieurs raisons pour lesquelles vous souhaiteriez toochange qui :

* Vous souhaitez toouse une autre HTTP bibliothèque tooadjust les délais d’attente.
* Vous souhaitez tooprovide une barre de progression.
* Vous souhaitez tooadd une fonctionnalité de gestion toosupport API en-tête personnalisé.
* Vous souhaitez toointercept une réponse indiquant un échec afin que vous pouvez implémenter la réauthentification.
* Vous souhaitez toolog principales demandes tooan analytique service.

### <a name="using-an-alternate-http-library"></a>Utilisation d’une autre bibliothèque HTTP

Appelez hello `.setAndroidHttpClientFactory()` méthode immédiatement après avoir créé votre référence de client.  Par exemple, tooset hello connexion délai d’attente too60 secondes (au lieu de valeur par défaut de hello 10 secondes) :

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

### <a name="implement-a-progress-filter"></a>Implémenter un filtre de progression

Vous pouvez implémenter une interception de chaque demande en implémentant un élément `ServiceFilter`.  Par exemple, suivant de hello met à jour une barre de progression créés au préalable :

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

Vous pouvez attacher ce client toohello de filtre comme suit :

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a>Personnaliser des en-têtes de demande

Utilisez hello suivante `ServiceFilter` et joindre filtre hello Bonjour comme hello `ProgressFilter`:

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

### <a name="conversions"></a>Configurer la sérialisation automatique

Vous pouvez spécifier une stratégie de conversion qui applique tooevery colonne à l’aide de hello [gson] [ 3] API. bibliothèque du client Android Hello utilise [gson] [ 3] coulisses hello tooserialize Java objets tooJSON données avant l’envoi des données de hello tooAzure du Service d’applications.  Hello de code suivant utilise hello **setFieldNamingStrategy()** stratégie de méthode tooset hello. Cet exemple supprimera hello initiale (un « m »), puis en minuscules hello suivant caractères et, pour chaque nom de champ. Par exemple, il changera « mId » en « id ».  Implémentez un Bonjour tooreduce de stratégie conversion besoin pour `SerializedName()` annotations sur la plupart des champs.

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

Ce code doit être exécuté avant de créer une référence de client mobile à l’aide de hello **MobileServiceClient**.

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
