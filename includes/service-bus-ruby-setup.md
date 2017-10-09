## <a name="create-a-ruby-application"></a><span data-ttu-id="cd415-101">Création d'une application Ruby</span><span class="sxs-lookup"><span data-stu-id="cd415-101">Create a Ruby application</span></span>
<span data-ttu-id="cd415-102">Pour obtenir des instructions, consultez le guide [Création d’une application Ruby sur Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="cd415-102">For instructions, see [Create a Ruby Application on Azure](../articles/virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="cd415-103">Configurer votre tooUse application Service Bus</span><span class="sxs-lookup"><span data-stu-id="cd415-103">Configure Your application tooUse Service Bus</span></span>
<span data-ttu-id="cd415-104">toouse Service Bus, télécharger et utiliser package hello Azure Ruby, qui inclut un ensemble de bibliothèques de commodité qui communiquent avec les services REST de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="cd415-104">toouse Service Bus, download and use hello Azure Ruby package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="cd415-105">Utiliser le package hello tooobtain RubyGems</span><span class="sxs-lookup"><span data-stu-id="cd415-105">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="cd415-106">Ouvrez une interface de ligne de commande, telle que **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="cd415-106">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="cd415-107">Tapez « marque installer azure » dans les dépendances et le marque hello tooinstall hello commande fenêtre.</span><span class="sxs-lookup"><span data-stu-id="cd415-107">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="cd415-108">Importer un package hello</span><span class="sxs-lookup"><span data-stu-id="cd415-108">Import hello package</span></span>
<span data-ttu-id="cd415-109">À l’aide de votre éditeur de texte favori, ajoutez hello suivant en haut de toohello de hello Ruby fichier dans lequel vous avez l’intention de toouse stockage :</span><span class="sxs-lookup"><span data-stu-id="cd415-109">Using your favorite text editor, add hello following toohello top of hello Ruby file in which you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="cd415-110">Configuration d’une connexion Service Bus</span><span class="sxs-lookup"><span data-stu-id="cd415-110">Set up a Service Bus connection</span></span>
<span data-ttu-id="cd415-111">Les valeurs hello tooset d’espace de noms, nom de hello de code de suivant de hello utilisation clé, clé, signataire et hôte :</span><span class="sxs-lookup"><span data-stu-id="cd415-111">Use hello following code tooset hello values of namespace, name of hello key, key, signer and host:</span></span>

```ruby
Azure.configure do |config|
  config.sb_namespace = '<your azure service bus namespace>'
  config.sb_sas_key_name = '<your azure service bus access keyname>'
  config.sb_sas_key = '<your azure service bus access key>'
end
signer = Azure::ServiceBus::Auth::SharedAccessSigner.new
sb_host = "https://#{Azure.sb_namespace}.servicebus.windows.net"
```

<span data-ttu-id="cd415-112">La valeur hello espace de noms valeur toohello que vous avez créée au lieu de l’URL complète de hello.</span><span class="sxs-lookup"><span data-stu-id="cd415-112">Set hello namespace value toohello value you created rather than hello entire URL.</span></span> <span data-ttu-id="cd415-113">Par exemple, utilisez **« votreespacedenomsexemple »** et non « votreespacedenomsexemple.servicebus.windows.net ».</span><span class="sxs-lookup"><span data-stu-id="cd415-113">For example, use **"yourexamplenamespace"**, not "yourexamplenamespace.servicebus.windows.net".</span></span>
