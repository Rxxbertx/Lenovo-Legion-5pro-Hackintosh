<div id="header" align="center">
  <img src="https://media.giphy.com/media/M9gbBd9nbDrOTu1Mqx/giphy.gif" width="100"/>
  
  Hackintosh LENOVO LEGION 5 PRO AMD 6TH GEN
==========================================
<h1>
  Hola
  <img src="https://media.giphy.com/media/hvRJCLFzcasrR4ia7z/giphy.gif" width="30px"/>
</h1>
Espero que te sirva de ayuda (mas abajo tienes una seccion de ayuda), gracias

**Version instalada**: macOS BigSur

</div>



HARDWARE
--------



| Componente    | Descripción                        |
|---------------|-----------------------------------|
| CPU           | AMD Ryzen 7 5800h (8 cores 16 threads) |
| dGPU          | NVIDIA RTX 3070 8GB               |
| iGPU          | AMD RX Vega 10                    |
| RAM           | 16GB 3200mhz DDR4                 |
| SSD           | CRUCIAL P5 PLUS nvme              |
| USB           | 3.2 DOS CONTROLADORES XHC0 XHC1   |
| AUDIO         | Realtek ALC 2XX                   |
| ETHERNET      | Realtek RTL8111E                  |
| WIFI + BT     | Intel AX210 NGW                   |
| DISPLAY       | CSO 165HZ IPS HDR                 |
| CAMERA        | 720p Sonix                        |
| TECLADO       | USB ITE 8910                      |
| TRACKPAD      | I2C HID                           |
| BATERIA       | 80Wh                              |


* * *

¿QUE FUNCIONA Y QUE NO?
-----------------------

### GENERAL

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
| Componente              | Compatibilidad              |
|-------------------------|-----------------------------|
| HDMI, TIPO C (DP)       | ❌ (PORQUE ESTAN CONECTADOS A LA DGPU) |
| AUDIO                   | ✅                           |
| MICROFONO               | ❌                           |
| CAMERA                  | ✅                           |


### FUNCIONES

| Función                        | Compatibilidad                              |
|--------------------------------|---------------------------------------------|
| LUZ TECLADO                    | ✅                                           |
| LUZ LOGOTIPO                   | ✅                                           |
| APAGAR/REINCIAR                | ✅                                           |
| DORMIR                         | ❌ (se esta trabajando en una solucion)      |
| DISPLAY: CONTROL DE BRILLO     | HDR Mode ✅<br>Normal Mode ❌                |
| AIRDROP                        | ✅, SOLO DE ANDROID A MAC ([WARPSHARE](https://github.com/moseoridev/WarpShare)) |

si quieres que pruebe mas funciones, abre una ISSUE preguntado acerca de la funcion y la probaré..

* * *

SSDT USADOS
-----------

| SSDT                                  | Descripción                                                                                                                                                    |
|------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [SSDT-EC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)               | Crea un dispositivo Embedded Controller falso para que macOS funcione correctamente, pero no desactiva el EC original, ya que los portátiles lo necesitan para el estado de la batería, las teclas FN, etc. |
| [SSDT-PLUG-ALT](https://dortania.github.io/Getting-Started-With-ACPI/Universal/plug.html)           | Establece la propiedad plugin-type a 1 en el primer núcleo de CPU, habilitando X86PlatformPlugin, que permite (Intel) CPU Power Management y AGPM (Apple GPU Power Management). También redefine los procesadores con objetos Processor en lugar de objetos Device si es necesario, ya que macOS no soporta el nuevo estándar. |
| [SSDT-PNLF](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/backlight.html)            | Crea un dispositivo PNLF falso con un _UID seleccionable por el usuario (básicamente el perfil que utiliza) para permitir el control nativo del brillo en portátiles. |
| [SSDT-ALS0](https://chefkissinc.github.io/Extras/SSDTs/SSDT-ALS0.aml)                              | Simula la presencia del sensor de luz ambiental es necesaria para el funcionamiento del brillo en laptops. |
| [SSDT-SMBUS-MCHC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/smbus.html)         | Sirve para la comunicación con la fuente de alimentación para las instrucciones ON/OFF y más. La funcionalidad exacta y las interfaces de hardware varían según los proveedores. |
| [SSDT-XOSI](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/trackpad.html)             | Hace creer que estamos usando Windows, permitiendo que cualquier periférico bloqueado detrás de no macOS esté activo en macOS. |
| [SSDT-NODGPU***](https://t.me/JonnyEx)     | Es un ssdt especial creado por @ExtremeXT para la desactivacion de la dGPU, hay laptops que en el metodo off tienen codigo que llama al dispositivo EC, con este ssdt se evita ese codigo, añadiendolo en el metodo _REG, de esta manera se puede desactivar la dgpu de manera correcta sin fallos, tambien se usa el metodo Bumbleeblee. |
| [SSDT-USBX](https://dortania.github.io/Getting-Started-With-ACPI/Universal/ec-fix.html)              | Crea un dispositivo USBX que contiene las propiedades de alimentación USB necesarias para funcionar correctamente. Esto también requiere un dispositivo EC válido. |


\*\*\* Para adaptar este ssdt a tu sistema escribeme al telegram y te ayudare, referencia: [tonymacx86](https://www.tonymacx86.com/threads/guide-disabling-discrete-graphics-in-dual-gpu-laptops.163772/)

* * *

KEXTS USADOS (Advertencia: Algunos de estos Kexts son solo para macOS BigSur, para otras versiones de mac necesitaras otros kext y otras configuraciones)
---------------------------------------------------------------------------------------------------------------------------------------------------------

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

MacBookPro16,3

* * *

AYUDA
-----

Si necesitas ayudas en el proceso de creacion de tu EFI no dudes en escribirme por telegram (haz clic en la imagen) o [aqui](https://t.me/JonnyEx)  
Se parte de ChefKissInc una comunidad donde hacen posible que todas las laptop AMD puedan usar MAC (haz click en la imagen) o [aqui](https://t.me/+Bx3MO9Hq8whhNzk9)

* * *

CREDITOS
--------

[@ChefKissInc](https://github.com/ChefKissInc) Muchas gracias por la ayuda y hacer todo esto posible, con vosotros se inicia una nueva era para AMD

[@Acidanthera](https://github.com/acidanthera) Gracias por multiples kext y gracias por Opencore

[@OpenIntelWireless](https://github.com/OpenIntelWireless) Gracias por el soporte a las tarjetas INTEL

[@WarpShare](https://github.com/moseoridev/WarpShare) Muchas gracias por hacer posible Airdrop entre Android y Mac

[@ExtremeXT](https://github.com/ExtremeXT) Muchas gracias por tu paciencia y por toda tu ayuda, eres un genio

[@adhocfra](https://github.com/adhocfra) Gracias amigo
