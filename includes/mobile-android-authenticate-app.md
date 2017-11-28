
1. <span data-ttu-id="75dd5-101">Ouvrez le projet dans Android Studio.</span><span class="sxs-lookup"><span data-stu-id="75dd5-101">Open the project in Android Studio.</span></span>

2. <span data-ttu-id="75dd5-102">Dans l’**Explorateur de projets** d’Android Studio, ouvrez le fichier ToDoActivity.java, puis ajoutez les instructions d’importation suivantes :</span><span class="sxs-lookup"><span data-stu-id="75dd5-102">In **Project Explorer** in Android Studio, open the ToDoActivity.java file and add the following import statements:</span></span>

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. <span data-ttu-id="75dd5-103">Ajoutez la méthode suivante à la classe **ToDoActivity** :</span><span class="sxs-lookup"><span data-stu-id="75dd5-103">Add the following method to the **ToDoActivity** class:</span></span>

        // You can choose any unique number here to differentiate auth providers from each other. Note this is the same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using the Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check the request code matches the one we send in the login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check the error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    <span data-ttu-id="75dd5-104">Ce code crée une méthode pour gérer le processus d’authentification Google.</span><span class="sxs-lookup"><span data-stu-id="75dd5-104">This code creates a method to handle the Google authentication process.</span></span> <span data-ttu-id="75dd5-105">Une boîte de dialogue affiche l’identificateur de l’utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="75dd5-105">A dialog displays the ID of the authenticated user.</span></span> <span data-ttu-id="75dd5-106">Vous pouvez agir uniquement si l’authentification a réussi.</span><span class="sxs-lookup"><span data-stu-id="75dd5-106">You can only proceed on a successful authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="75dd5-107">Si vous utilisez un autre fournisseur d’identité que Google, remplacez la valeur transférée à la méthode **login** par l’une des valeurs suivantes : _MicrosoftAccount_, _Facebook_, _Twitter_ ou _windowsazureactivedirectory_.</span><span class="sxs-lookup"><span data-stu-id="75dd5-107">If you are using an identity provider other than Google, change the value passed to the **login** method to one of the following values: _MicrosoftAccount_, _Facebook_, _Twitter_, or _windowsazureactivedirectory_.</span></span>

4. <span data-ttu-id="75dd5-108">Dans la méthode **onCreate**, ajoutez la ligne de code suivante après le code qui permet d’instancier l’objet `MobileServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="75dd5-108">In the **onCreate** method, add the following line of code after the code that instantiates the `MobileServiceClient` object.</span></span>

        authenticate();

    <span data-ttu-id="75dd5-109">Cet appel lance le processus d'authentification.</span><span class="sxs-lookup"><span data-stu-id="75dd5-109">This call starts the authentication process.</span></span>

5. <span data-ttu-id="75dd5-110">Déplacez le code restant après `authenticate();` dans la méthode **onCreate** vers une nouvelle méthode **createTable** :</span><span class="sxs-lookup"><span data-stu-id="75dd5-110">Move the remaining code after `authenticate();` in the **onCreate** method to a new **createTable** method:</span></span>

        private void createTable() {

            // Get the table instance to use.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter to bind the items with the view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load the items from Azure.
            refreshItemsFromTable();
        }

6. <span data-ttu-id="75dd5-111">Pour garantir la redirection souhaitée, ajoutez l’extrait de code suivant de _RedirectUrlActivity_ à _AndroidManifest.xml_ :</span><span class="sxs-lookup"><span data-stu-id="75dd5-111">To ensure redirection works as expected, add the following snippet of _RedirectUrlActivity_ to _AndroidManifest.xml_:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. <span data-ttu-id="75dd5-112">Ajoutez redirectUriScheme au _build.gradle_ de votre application Android.</span><span class="sxs-lookup"><span data-stu-id="75dd5-112">Add redirectUriScheme to _build.gradle_ of your Android application.</span></span>

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

8. <span data-ttu-id="75dd5-113">Ajoutez com.android.support:customtabs:23.0.1 aux dépendances de votre build.gradle :</span><span class="sxs-lookup"><span data-stu-id="75dd5-113">Add com.android.support:customtabs:23.0.1 to the dependencies in your build.gradle:</span></span>

      <span data-ttu-id="75dd5-114">dependencies {        // ...        compile ’com.android.support:customtabs:23.0.1’    }</span><span class="sxs-lookup"><span data-stu-id="75dd5-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span></span>

9. <span data-ttu-id="75dd5-115">Dans le menu **Exécuter**, cliquez sur **Exécuter l’application** pour démarrer l’application, puis connectez-vous avec le fournisseur d’identité choisi.</span><span class="sxs-lookup"><span data-stu-id="75dd5-115">From the **Run** menu, click **Run app** to start the app and sign in with your chosen identity provider.</span></span>

> [!WARNING]
> <span data-ttu-id="75dd5-116">Le schéma d’URL mentionné respecte la casse.</span><span class="sxs-lookup"><span data-stu-id="75dd5-116">The URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="75dd5-117">Assurez-vous que toutes les occurrences de `{url_scheme_of_you_app}` utilisent la même casse.</span><span class="sxs-lookup"><span data-stu-id="75dd5-117">Ensure that all occurrences of `{url_scheme_of_you_app}` use the same case.</span></span>

<span data-ttu-id="75dd5-118">Une fois que vous êtes connecté, l’application doit s’exécuter sans erreur et vous devez être en mesure d’interroger le service principal et de mettre à jour les données.</span><span class="sxs-lookup"><span data-stu-id="75dd5-118">When you are successfully signed in, the app should run without errors, and you should be able to query the back-end service and make updates to data.</span></span>
