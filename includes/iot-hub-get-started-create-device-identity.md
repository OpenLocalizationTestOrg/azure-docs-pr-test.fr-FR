## <a name="create-a-device-identity"></a><span data-ttu-id="99cff-101">Création d’une identité d’appareil</span><span class="sxs-lookup"><span data-stu-id="99cff-101">Create a device identity</span></span>

<span data-ttu-id="99cff-102">Dans cette section, vous utilisez un outil Node.js appelé [iothub-explorer] [ iot-hub-explorer] toocreate une identité d’appareil pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="99cff-102">In this section, you use a Node.js tool called [iothub-explorer][iot-hub-explorer] toocreate a device identity for this tutorial.</span></span> <span data-ttu-id="99cff-103">Les ID d’appareil respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="99cff-103">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="99cff-104">Exécutez hello qui suit dans votre environnement de ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="99cff-104">Run hello following in your command-line environment:</span></span>

    `npm install -g iothub-explorer@latest`

1. <span data-ttu-id="99cff-105">Ensuite, exécutez hello suivant concentrateur de commande toologin tooyour.</span><span class="sxs-lookup"><span data-stu-id="99cff-105">Then, run hello following command toologin tooyour hub.</span></span> <span data-ttu-id="99cff-106">Substitution `{iot hub connection string}` avec hello chaîne de connexion de IoT Hub vous avez copiés précédemment :</span><span class="sxs-lookup"><span data-stu-id="99cff-106">Substitute `{iot hub connection string}` with hello IoT Hub connection string you previously copied:</span></span>

    `iothub-explorer login "{iot hub connection string}"`

1. <span data-ttu-id="99cff-107">Enfin, créez une nouvelle identité d’appareil appelée `myDeviceId` avec la commande hello :</span><span class="sxs-lookup"><span data-stu-id="99cff-107">Finally, create a new device identity called `myDeviceId` with hello command:</span></span>

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

<span data-ttu-id="99cff-108">Notez la chaîne de connexion de périphérique hello à partir du résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="99cff-108">Make a note of hello device connection string from hello result.</span></span> <span data-ttu-id="99cff-109">Cette chaîne de connexion de périphérique est utilisée par l’application d’appareil hello tooyour tooconnect IoT Hub en tant que périphérique.</span><span class="sxs-lookup"><span data-stu-id="99cff-109">This device connection string is used by hello device app tooconnect tooyour IoT Hub as a device.</span></span>

![][img-identity]

<span data-ttu-id="99cff-110">Consultez trop[prise en main de IoT Hub] [ lnk-getstarted] tooprogrammatically créer des identités de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="99cff-110">Refer too[Getting started with IoT Hub][lnk-getstarted] tooprogrammatically create device identities.</span></span>

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
