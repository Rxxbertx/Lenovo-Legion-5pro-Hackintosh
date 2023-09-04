<div id="header" align="center">
  <img src="https://github.com/Rxxbertx/Lenovo-Legion-5pro-Hackintosh/blob/main/images/lenovoApple.png" width="150"/>
  
  Hackintosh LENOVO LEGION 5 PRO AMD 6TH GEN
==========================================

  <img src="https://github.com/Rxxbertx/Lenovo-Legion-5pro-Hackintosh/blob/main/images/mac.png" width="650"/>

![Static Badge](https://img.shields.io/badge/macOS-BigSur-blue)
![Static Badge](https://img.shields.io/badge/OpenCore-0.9.4-green)
![GitHub issues](https://img.shields.io/github/issues/Rxxbertx/Lenovo-Legion-5pro-Hackintosh)



</div>



HARDWARE
--------



| Component    |                       |
|---------------|-----------------------------------|
| CPU           | AMD Ryzen 7 5800h (8 cores 16 threads) |
| dGPU          | NVIDIA RTX 3070 8GB               |
| iGPU          | AMD Vega RX10                    |
| RAM           | 16GB 3200mhz DDR4                 |
| SSD           | CRUCIAL P5 PLUS nvme              |
| USB           | 3.2  XHC0 XHC1   |
| AUDIO         | Realtek ALC 287 48khz                   |
| ETHERNET      | Realtek RTL8111E                  |
| WIFI + BT     | Intel AX210 NGW                   |
| DISPLAY       | CSO 165HZ IPS HDR                 |
| CAMERA        | 720p Sonix                        |
| TECLADO       | USB ITE 8910                      |
| TRACKPAD      | I2C HID                           |
| BATERIA       | 80Wh                              |


* * *

<div align=center>
  
   **SELECT LANGUAGUE**
   
</div>



<details close>
 <summary> 
 <p align="center"> ESPAÑOL 🇪🇸 (HAZ CLICK)</p>


   
 </summary>



<a name="ESP"></a>


**NO ENCONTRARAS NINGUNA EFI PARA DESCARGAR** , TE PUEDO AYUDAR A REALIZAR LA TUYA (mas abajo tienes una seccion de [AYUDA](#ayuda) ), gracias


***

## Índice

- [**¿QUÉ FUNCIONA Y QUÉ NO?**](#qué-funciona-y-qué-no)
  - [General](#general)
  - [Multimedia](#multimedia)
  - [Funciones](#funciones)

- [**SSDT UTILIZADOS**](#ssdt-usados)

- [**KEXTS UTILIZADOS**](#kexts-usados)

- [**SMBIOS UTILIZADO**](#smbios-usado)

- [**OPCIONES BIOS**](#opciones-bios)

- [**AYUDA**](#ayuda)

- [**CRÉDITOS**](#créditos)



***
***




¿QUÉ FUNCIONA Y QUÉ NO?
-----------------------
<a name="qué-funciona-y-qué-no"></a>
### GENERAL
<a name="general"></a>
| Componente               | Compatibilidad |
|--------------------------|----------------|
| CPU                      | ✅              |
| iGPU                     | ✅              |
| DGPU                     | ❌              |
| RAM                      | ✅              |
| ETHERNET                 | ✅              |
| USB                      | ✅              |
| DISPLAY                  | HDR Mode ✅<br>60-165hz ✅  |
| BATERIA                  | ✅              |
| TECLADO y teclas de FN   | ✅              |
| TRACKPAD                 | ✅              |


### MULTIMEDIA
<a name="multimedia"></a>
| Componente              | Compatibilidad              |
|-------------------------|-----------------------------|
| HDMI, TIPO C (DP)       | ❌ (PORQUE ESTAN CONECTADOS A LA DGPU) |
| AUDIO                   | ✅                           |
| MICROFONO               | ❌                           |
| CAMERA                  | ✅                           |


### FUNCIONES
<a name="funciones"></a>
| Función                        | Compatibilidad                              |
|--------------------------------|---------------------------------------------|
| LUZ TECLADO                    | ✅                                           |
| LUZ LOGOTIPO                   | ✅                                           |
| APAGAR/REINCIAR                | ✅                                           |
| SUSPENDER                         | ❌ (se esta trabajando en una solucion)      |
| DISPLAY: CONTROL DE BRILLO     | HDR Mode ✅<br>Normal Mode ❌                |
| AIRDROP                        | ✅, SOLO DE ANDROID A MAC ([WARPSHARE](https://github.com/moseoridev/WarpShare)) |

si quieres que pruebe mas funciones, abre una ISSUE preguntado acerca de la funcion y la probaré..

* * *

SSDT USADOS
-----------
<a name="ssdt-usados"></a>
| SSDT                                  | Descripción                                                                                                                                                    |
|------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [SSDT-EC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)               | Crea un dispositivo Embedded Controller falso para que macOS funcione correctamente, pero no desactiva el EC original, ya que los portátiles lo necesitan para el estado de la batería, las teclas FN, etc. |
| [SSDT-PLUG-ALT](https://dortania.github.io/Getting-Started-With-ACPI/Universal/plug.html)           | Establece la propiedad plugin-type a 1 en el primer núcleo de CPU, habilitando X86PlatformPlugin, que permite (Intel) CPU Power Management y AGPM (Apple GPU Power Management). También redefine los procesadores con objetos Processor en lugar de objetos Device si es necesario, ya que macOS no soporta el nuevo estándar. |
| [SSDT-PNLF](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/backlight.html)            | Crea un dispositivo PNLF falso con un _UID seleccionable por el usuario (básicamente el perfil que utiliza) para permitir el control nativo del brillo en portátiles. |
| [SSDT-ALS0](https://chefkissinc.github.io/Extras/SSDTs/SSDT-ALS0.aml)                              | Simula la presencia del sensor de luz ambiental es necesaria para el funcionamiento del brillo en laptops. |
| [SSDT-SMBUS-MCHC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/smbus.html)         | Sirve para la comunicación con la fuente de alimentación para las instrucciones ON/OFF y más. La funcionalidad exacta y las interfaces de hardware varían según los proveedores. |
| [SSDT-XOSI](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/trackpad.html)             | Hace creer que estamos usando Windows, permitiendo que cualquier periférico bloqueado detrás de no macOS esté activo en macOS. |
| [SSDT-NODGPU***](https://t.me/JonnyEx)     | Es un ssdt especial creado por [@ExtremeXT](https://github.com/ExtremeXT) para la desactivacion de la dGPU, hay laptops que en el metodo off tienen codigo que llama al dispositivo EC, con este ssdt se evita ese codigo, añadiendolo en el metodo _REG, de esta manera se puede desactivar la dgpu de manera correcta sin fallos, tambien se usa el metodo Bumbleeblee. |
| [SSDT-USBX](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)              | Crea un dispositivo USBX que contiene las propiedades de alimentación USB necesarias para funcionar correctamente. Esto también requiere un dispositivo EC válido. |


\*\*\* Para adaptar este ssdt a tu sistema escribeme al telegram y te ayudare, referencia: [tonymacx86](https://www.tonymacx86.com/threads/guide-disabling-discrete-graphics-in-dual-gpu-laptops.163772/)

* * *

KEXTS USADOS (Advertencia: Algunos de estos Kexts son solo para macOS BigSur, para otras versiones de mac necesitaras otros kext y otras configuraciones)
---------------------------------------------------------------------------------------------------------------------------------------------------------
<a name="kexts-usados"></a>
| KEXT                                            | Descripción                                                                                         |
|----------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| [NootedRed](https://github.com/NootInc/NootedRed)  | Proporciona aceleración gráfica para iGPU AMD Vega.                                                  |
| [AirportItlwm](https://github.com/OpenIntelWireless/itlwm) | Admite la mayoría de las tarjetas Intel Wi-Fi. AirportItlwm utiliza la pila Wi-Fi de macOS.   |
| [AMDTscSync](https://github.com/naveenkrdy/AmdTscSync)   | Sincroniza el contador de marca de tiempo (TSC): generalmente solo es útil para APU AMD que serían tremendamente lentas sin él. |
| [AppleALC](https://github.com/acidanthera/AppleALC)     | Parchea la pila de audio de Apple ( AppleHDA/ AppleGFXHDA) para permitir códecs de audio y audio HDMI no compatibles.   |
| [BrightnessKeys](https://github.com/acidanthera/BrightnessKeys) | Brinda soporte para notificaciones de cambio de brillo ACPI (que generalmente provienen de las teclas de función (FN) del teclado). |
| [ECEnabler](https://github.com/1Revenger1/ECEnabler)    | Permite que macOS lea campos EC de más de 8 bits, eliminando la necesidad de dividirlos manualmente. |
| [FeatureUnlock](https://github.com/acidanthera/FeatureUnlock) | Extensión de Lilu Kernel para habilitar: Sidecar, NightShift, AirPlay to Mac, Universal Control, Continuity Camera. |
| [GenericUSBXHCI](https://github.com/RattletraPM/GUX-RyzenXHCIFix) | Soluciona el problema de USB3 encontrado en algunos hackintosh basados en APU Ryzen. |
| [IntelBluetoothFirmware](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) | Admite la mayoría de las tarjetas Intel Wi-Fi. En macOS 11 y versiones anteriores, debes usar los 3 kexts incluidos. En macOS 12+ necesitas usar IntelBluetoothFirmware, IntelBTPatcher y BlueToolFixup. |
| [IntelBluetoothInjector (BigSur -)](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) | Se encuentra dentro de IntelBluetoothFirmware, solo para BigSur y menos de BigSur. |
| [IntelBTPatcher](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) | Se encuentra dentro de IntelBluetoothFirmware. |
| [Lilu](https://github.com/acidanthera/Lilu)          | Realiza parches arbitrarios de kext, bibliotecas y programas dentro de macOS. |
| [NVMeFix](https://github.com/acidanthera/NVMeFix)      | Parchea la pila NVMe (IONVMeFamily) para admitir la transición de estado de energía autónoma (APST) y para solucionar problemas de pánico del kernel por tiempo de espera en algunos controladores NVMe. |
| [RealtekRTL8111](https://github.com/Mieze/RTL8111_driver_for_OS_X) | Controlador RTL8111 (1GBe Realtek), portado desde Linux. |
| [RestrictEvents](https://github.com/acidanthera/RestrictEvents) | Corrige el nombre de la CPU en About This Mac y las advertencias de memoria y PCI en MacPro7,1 SMBIOS. También permite obligar a VMM a corregir actualizaciones OTA en T2 SMBIOS en macOS Sonoma+, entre otras características. |
| [SMCBatteryManager](https://github.com/acidanthera/VirtualSMC) | Supervisa el estado de la batería de la computadora portátil. |
| [SMCLightSensor](https://github.com/acidanthera/VirtualSMC) | Agrega compatibilidad con el sensor de luz ambiental ACPI. |
| [USBMap](https://github.com/USBToolBox/tool)          | (En mi caso UsbToolBox no funciona, usen la opción nativa de USBToolBox para no tener que usar el kext USBToolBox). |
| [VirtualSMC](https://github.com/acidanthera/VirtualSMC)  | Emula el SMC de Apple. |
| [VoodooI2C (AMD)](https://chefkissinc.github.io/Extras/Kexts/VoodooI2C.zip) | Controlador para dispositivos de entrada I2C. La que está vinculada es una versión preliminar con soporte adicional para controladores AMD I2C. |
| VoodooI2CHID | Esta dentro de VoodooI2C. |
| [YogaSMC](https://github.com/zhen-zen/YogaSMC)        | Permite soporte a funciones especiales de Lenovo, modo Conservación Batería, USB siempre activo... |
| [AppleIntelMCEReporter (Monterey +)](https://chefkissinc.github.io/Extras/Kexts/AppleMCEReporterDisabler.zip) | Desactiva AppleIntelMCEReporter el pánico en los sistemas AMD e incluso en algunos sistemas Intel. |

* * *

### SMBIOS Usado
<a name="smbios-usado"></a>

    MacBookPro16,3


* * *

OPCIONES BIOS
----
<a name="opciones-bios"></a>

    Secure Boot : Disabled
    VRAM igpu: 2GB
    Graphics : Dynamic


* * *


AYUDA
-----
<a name="ayuda"></a>
<div id="help" align="center">


Si necesitas ayudas en el proceso de creacion de tu EFI **no dudes en escribirme** por telegram (haz clic en la imagen) 

[<img src="https://i0.wp.com/img.talkandroid.com/uploads/2015/05/telegram_app_icon.png" alt="Telegram" width="90" height="90">](https://t.me/JonnyEx)



**Se parte de ChefKissInc** una comunidad donde hacen posible que todas las laptop AMD puedan usar MAC (haz clic en la imagen)

[<img src="https://i0.wp.com/img.talkandroid.com/uploads/2015/05/telegram_app_icon.png" alt="Telegram" width="90" height="90">](https://t.me/+Bx3MO9Hq8whhNzk9)

  
</div>


* * *

CREDITOS
--------
<a name="creditos"></a>
[@ChefKissInc](https://github.com/ChefKissInc) Muchas gracias por la ayuda y hacer todo esto posible, con vosotros se inicia una nueva era para AMD

[@Acidanthera](https://github.com/acidanthera) Gracias por multiples kext y gracias por Opencore

[@OpenIntelWireless](https://github.com/OpenIntelWireless) Gracias por el soporte a las tarjetas INTEL

[@WarpShare](https://github.com/moseoridev/WarpShare) Muchas gracias por hacer posible Airdrop entre Android y Mac

[@ExtremeXT](https://github.com/ExtremeXT) Muchas gracias por tu paciencia y por toda tu ayuda, eres un genio

[@adhocfra](https://github.com/adhocfra) Gracias amigo


</details>


<details open>
 <summary> 
 <p align="center"> ENGLISH 🇺🇸 (CLICK) </p>

   
 </summary>

<a name="ENG"></a>

**YOU WON'T FIND ANY EFI TO DOWNLOAD**, I CAN HELP YOU CREATE YOUR OWN (see [HELP](#help) section below), thank you.

***
## Table of Contents

- [**WHAT WORKS AND WHAT DOESN'T?**](#what-works-and-what-doesnt)
  - [General](#general)
  - [Multimedia](#multimedia)
  - [Functions](#functions)

- [**USED SSDTs**](#used-ssdts)

- [**USED KEXTS**](#used-kexts)

- [**USED SMBIOS**](#used-smbios)
  
- [**BIOS OPTIONS**](#bios-options)

- [**HELP**](#help)

- [**CREDITS**](#credits)


***
***

WHAT WORKS AND WHAT DOESN'T?
---------------------------
<a name="#what-works-and-what-doesnt"></a>
### GENERAL
<a name="general"></a>
| Component                | Compatibility |
|--------------------------|---------------|
| CPU                      | ✅             |
| iGPU                     | ✅             |
| DGPU                     | ❌             |
| RAM                      | ✅             |
| ETHERNET                 | ✅             |
| WIFI + BT                 | ✅             |
| USB                      | ✅             |
| DISPLAY                  | HDR Mode ✅<br>60-165hz ✅ |
| BATTERY                  | ✅             |
| KEYBOARD and FN keys     | ✅             |
| TRACKPAD                 | ✅             |

### MULTIMEDIA
<a name="multlimedia"></a>

| Component               | Compatibility                   |
|-------------------------|----------------------------------|
| HDMI, TYPE C (DP)       | ❌ (BECAUSE THEY'RE CONNECTED TO DGPU) |
| AUDIO                   | ✅                              |
| MICROPHONE              | ❌                              |
| CAMERA                  | ✅                              |

### FUNCTIONS
<a name="functions"></a>
| Function                 | Compatibility                              |
|--------------------------|---------------------------------------------|
| KEYBOARD BACKLIGHT       | ✅                                           |
| LOGO BACKLIGHT           | ✅                                           |
| SHUTDOWN/RESTART         | ✅                                           |
| SLEEP                    | ❌ (work in progress)                      |
| DISPLAY: BRIGHTNESS CONTROL | HDR Mode ✅<br>Normal Mode ❌             |
| AIRDROP                  | ✅, ANDROID TO MAC ONLY ([WARPSHARE](https://github.com/moseoridev/WarpShare)) |
| iServices (AppStore,Facetime...) | ✅|

If you want me to test more functions, open an ISSUE asking about the function, and I will test it.

* * *

USED SSDTs
-----------
<a name="used-ssdts"></a>
| SSDT                                  | Description                                                                                                                                      |
|--------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| [SSDT-EC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)           | Creates a fake Embedded Controller device for macOS to work correctly but does not disable the original EC, as laptops need it for battery status, FN keys, etc. |
| [SSDT-PLUG-ALT](https://dortania.github.io/Getting-Started-With-ACPI/Universal/plug.html)       | Sets the plugin-type property to 1 on the first CPU core, enabling X86PlatformPlugin, which allows (Intel) CPU Power Management and AGPM (Apple GPU Power Management). It also redefines processors with Processor objects instead of Device objects if necessary since macOS does not support the new standard. |
| [SSDT-PNLF](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/backlight.html)        | Creates a fake PNLF device with a user-selectable _UID (basically the profile it uses) to allow native brightness control on laptops. |
| [SSDT-ALS0](https://chefkissinc.github.io/Extras/SSDTs/SSDT-ALS0.aml)                          | Simulates the presence of the ambient light sensor, necessary for brightness operation on laptops. |
| [SSDT-SMBUS-MCHC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/smbus.html)     | Used for communication with the power source for ON/OFF instructions and more. Exact functionality and hardware interfaces vary by providers. |
| [SSDT-XOSI](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/trackpad.html)         | Makes macOS believe we are using Windows, allowing any peripherals locked behind non-macOS to be active in macOS. |
| [SSDT-NODGPU***](https://t.me/JonnyEx) | This is a special SSDT created by [@ExtremeXT](https://github.com/ExtremeXT) for dGPU disabling. Some laptops have code in the off method that calls the EC device. This SSDT avoids that code by adding it to the _REG method, thus allowing proper dGPU disabling without issues. The Bumbleeblee method is also used. |
| [SSDT-USBX](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)        | Creates a USBX device containing the necessary USB power properties to work correctly. This also requires a valid EC device. |


\*\*\* To adapt this SSDT to your system, write to me on Telegram, and I will help you. Reference: [tonymacx86](https://www.tonymacx86.com/threads/guide-disabling-discrete-graphics-in-dual-gpu-laptops.163772/)

* * *

USED KEXTS (Warning: Some of these Kexts are only for macOS Big Sur, for other macOS versions, you will need different Kexts and configurations)
---------------------------------------------------------------------------------------------------------------------------------------------------------
<a name="used-kexts"></a>
| KEXT                                       | Description                                                                                          |
|--------------------------------------------|------------------------------------------------------------------------------------------------------|
| [NootedRed](https://github.com/NootInc/NootedRed) | Provides graphics acceleration for AMD Vega iGPU.                                                  |
| [AirportItlwm](https://github.com/OpenIntelWireless/itlwm) | Supports most Intel Wi-Fi cards. AirportItlwm uses the macOS Wi-Fi stack.               |
| [AMDTscSync](https://github.com/naveenkrdy/AmdTscSync)   | Synchronizes the Timestamp Counter (TSC), generally only useful for AMD APU, which would be extremely slow without it. |
| [AppleALC](https://github.com/acidanthera/AppleALC)     | Patches the Apple audio stack (AppleHDA/AppleGFXHDA) to allow unsupported audio codecs and HDMI audio.   |
| [BrightnessKeys](https://github.com/acidanthera/BrightnessKeys) | Provides support for ACPI brightness change notifications (usually coming from keyboard function (FN) keys). |
| [ECEnabler](https://github.com/1Revenger1/ECEnabler)    | Allows macOS to read EC fields over 8 bits, eliminating the need to split them manually. |
| [FeatureUnlock](https://github.com/acidanthera/FeatureUnlock) | Lilu Kernel extension to enable Sidecar, NightShift, AirPlay to Mac, Universal Control, Continuity Camera. |
| [GenericUSBXHCI](https://github.com/RattletraPM/GUX-RyzenXHCIFix) | Fixes USB3 issue found in some Ryzen-based hackintoshes. |
| [IntelBluetoothFirmware](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) | Supports most Intel Wi-Fi cards. On macOS 11 and earlier, you need to use all 3 included Kexts. On macOS 12+, you need to use IntelBluetoothFirmware, IntelBTPatcher, and BlueToolFixup. |
| [IntelBluetoothInjector (BigSur -)](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) | Found inside IntelBluetoothFirmware, only for Big Sur and below. |
| [IntelBTPatcher](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) | Found inside IntelBluetoothFirmware. |
| [Lilu](https://github.com/acidanthera/Lilu)          | Performs arbitrary kext, library, and program patching within macOS. |
| [NVMeFix](https://github.com/acidanthera/NVMeFix)      | Patches the NVMe stack (IONVMeFamily) to support Autonomous Power State Transition (APST) and fix kernel panic issues in some NVMe drivers. |
| [RealtekRTL8111](https://github.com/Mieze/RTL8111_driver_for_OS_X) | Realtek RTL8111 (1GbE Realtek) driver, ported from Linux. |
| [RestrictEvents](https://github.com/acidanthera/RestrictEvents) | Corrects CPU name in About This Mac and memory and PCI warnings in MacPro7,1 SMBIOS. Also allows forcing VMM to correct OTA updates on T2 SMBIOS on macOS Sonoma+, among other features. |
| [SMCBatteryManager](https://github.com/acidanthera/VirtualSMC) | Monitors laptop battery status. |
| [SMCLightSensor](https://github.com/acidanthera/VirtualSMC) | Adds ACPI ambient light sensor support. |
| [USBMap](https://github.com/USBToolBox/tool)          | (In my case, UsbToolBox doesn't work, use the built-in USBMap option to avoid using the USBToolBox Kext). |
| [VirtualSMC](https://github.com/acidanthera/VirtualSMC)  | Emulates Apple SMC. |
| [VoodooI2C (AMD)](https://chefkissinc.github.io/Extras/Kexts/VoodooI2C.zip) | Driver for I2C input devices. The linked one is a preliminary version with additional support for AMD I2C controllers. |
| VoodooI2CHID | Found within VoodooI2C. |
| [YogaSMC](https://github.com/zhen-zen/YogaSMC)        | Provides support for Lenovo special functions, Battery Conservation Mode, Always On USB... |
| [AppleIntelMCEReporter (Monterey +)](https://chefkissinc.github.io/Extras/Kexts/AppleMCEReporterDisabler.zip) | Disables AppleIntelMCEReporter panics on AMD systems and even some Intel systems. |

* * *

### USED SMBIOS
<a name="used-smbios"></a>

    MacBookPro16,3

* * *

 BIOS OPTIONS
 ----
<a name="bios-options"></a>

    Secure Boot : Disabled
    VRAM igpu: 2GB
    Graphics : Dynamic


* * *



HELP
----
<a name="help"></a>

<div id="help" align="center">

If you need help with your EFI creation process, **don't hesitate to reach out to me** on Telegram (click the image below):

[<img src="https://i0.wp.com/img.talkandroid.com/uploads/2015/05/telegram_app_icon.png" alt="Telegram" width="90" height="90">](https://t.me/JonnyEx)

**Join ChefKissInc**, a community where we make it possible for all AMD laptops to use macOS (click the image below):

[<img src="https://i0.wp.com/img.talkandroid.com/uploads/2015/05/telegram_app_icon.png" alt="Telegram" width="90" height="90">](https://t.me/+Bx3MO9Hq8whhNzk9)

</div>

* * *

CREDITS
-------
<a name="credits"></a>

[@ChefKissInc](https://github.com/ChefKissInc) Many thanks for your help and making all this possible; with you, a new era for AMD begins.

[@Acidanthera](https://github.com/acidanthera) Thanks for multiple Kexts and thanks for Opencore.

[@OpenIntelWireless](https://github.com/OpenIntelWireless) Thanks for supporting Intel Wi-Fi cards.

[@WarpShare](https://github.com/moseoridev/WarpShare) Many thanks for making Airdrop possible between Android and Mac.

[@ExtremeXT](https://github.com/ExtremeXT) Thank you very much for your patience and all your help; you are a genius.

[@adhocfra](https://github.com/adhocfra) Thanks, friend.


</details>


PHOTOS
---

<div id="PH" align="center">

<img src="https://github.com/Rxxbertx/Lenovo-Legion-5pro-Hackintosh/blob/main/images/macinfo.png"/>

<img src="https://github.com/Rxxbertx/Lenovo-Legion-5pro-Hackintosh/blob/main/images/macusb.png"/>

<img src="https://github.com/Rxxbertx/Lenovo-Legion-5pro-Hackintosh/blob/main/images/peinfo.png"/>

<img src="https://github.com/Rxxbertx/Lenovo-Legion-5pro-Hackintosh/blob/main/images/displayinfo.png"/>

<img src="https://github.com/Rxxbertx/Lenovo-Legion-5pro-Hackintosh/blob/main/images/cpubench.png"/>

<img src="https://github.com/Rxxbertx/Lenovo-Legion-5pro-Hackintosh/blob/main/images/gpubench.png"/>

</div>
