.. note::

    Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

    **Warum beitreten?**

    - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
    - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

    👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

USB-HDMI-Adapter
==========================================

.. image:: img/hdmi_adapter.jpeg

Dieses USB-HDMI-Adapterboard ist speziell für den Raspberry Pi 5 entwickelt worden. Seine Hauptfunktion besteht darin, die USB- und HDMI-Anschlüsse neu zu positionieren, um sie mit der USB-Schnittstellenseite des Raspberry Pi in Einklang zu bringen und so die Zugänglichkeit und das Kabelmanagement zu verbessern.

Zusätzlich wird der HDMI-Anschluss in eine Standard-HDMI-Typ-A-Schnittstelle umgewandelt, was eine breitere Kompatibilität bietet.

**Zusätzliche Stromversorgung für NVMe**

Das Board verfügt über einen 5V-Stromanschluss speziell für die NVMe-PIP-Stromversorgung. Zusammen mit einem Erweiterungsstecker kann es an die zusätzliche Stromschnittstelle des NVMe angeschlossen werden, um zusätzliche Energie zu liefern.

**1220RTC Batteriehalter**

Ein 1220RTC-Batteriehalter ist für die bequeme Installation einer RTC-Batterie integriert. Er wird über ein umgekehrtes SH1.0 2P-Kabel mit der RTC-Schnittstelle des Raspberry Pi verbunden.

Der Batteriehalter ist sowohl mit CR1220- als auch mit ML1220-Batterien kompatibel. Wenn Sie eine ML1220-Batterie (Lithium-Mangan-Dioxid-Batterie) verwenden, kann das Aufladen direkt am Raspberry Pi konfiguriert werden. Beachten Sie, dass die CR1220 nicht wiederaufladbar ist.

**Aktivierung des Trickle-Charging**

.. warning::

  Wenn Sie eine CR1220-Batterie verwenden, aktivieren Sie das Trickle-Charging nicht, da dies die Batterie irreparabel beschädigen und die Platine gefährden kann.

Standardmäßig ist die Trickle-Charging-Funktion für die Batterie deaktiviert. Die ``sysfs``-Dateien zeigen die aktuelle Trickle-Charging-Spannung und -Grenzen an:

.. code-block:: shell

    pi@raspberrypi:~ $ cat /sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage
    0
    pi@raspberrypi:~ $ cat /sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage_max
    4400000
    pi@raspberrypi:~ $ cat /sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage_min
    1300000

Um das Trickle-Charging zu aktivieren, fügen Sie ``rtc_bbat_vchg`` zu ``/boot/firmware/config.txt`` hinzu:

  * Öffnen Sie die Datei ``/boot/firmware/config.txt``.
  
    .. code-block:: shell
    
      sudo nano /boot/firmware/config.txt
      
  * Fügen Sie ``rtc_bbat_vchg`` zu ``/boot/firmware/config.txt`` hinzu.
  
    .. code-block:: shell
    
      dtparam=rtc_bbat_vchg=3000000
  
Nach dem Neustart zeigt das System Folgendes an:

.. code-block:: shell

    pi@raspberrypi:~ $ cat /sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage
    3000000
    pi@raspberrypi:~ $ cat /sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage_max
    4400000
    pi@raspberrypi:~ $ cat /sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage_min
    1300000

Dies bestätigt, dass die Batterie nun im Trickle-Charging-Modus ist. Um diese Funktion zu deaktivieren, entfernen Sie einfach die ``dtparam``-Zeile aus der ``config.txt``.
