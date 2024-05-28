.. note::

    Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

    **Warum beitreten?**

    - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
    - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

    👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

.. _view_control_commands:

Anzeigen und Steuern mit Befehlen
=======================================
Zusätzlich zur Ansicht von Daten des |link_pironman5| und zur Steuerung verschiedener Geräte über das Dashboard, können Sie auch Befehle zur Steuerung verwenden.

Grundkonfigurationen anzeigen
-----------------------------------

Das Modul ``pironman5`` bietet Grundkonfigurationen für den Pironman, die Sie mit dem folgenden Befehl überprüfen können.

.. code-block:: shell

  pironman5 -c

Die Standardkonfigurationen erscheinen wie folgt:

.. code-block:: 

  {
      "auto": {
          "rgb_color": "#0a1aff",
          "rgb_brightness": 50,
          "rgb_style": "breathing",
          "rgb_speed": 50,
          "rgb_enable": true,
          "rgb_led_count": 4,
          "temperature_unit": "C",
          "gpio_fan_mode": 2,
          "gpio_fan_pin": 6
      }
  }

Passen Sie diese Konfigurationen Ihren Bedürfnissen an.

Verwenden Sie ``pironman5`` oder ``pironman5 -h`` für Anweisungen.

.. code-block::

  usage: pironman5-service [-h] [-c] [-rc [RGB_COLOR]] [-rb [RGB_BRIGHTNESS]]
                          [-rs [{solid,breathing,flow,flow_reverse,rainbow,rainbow_reverse,hue_cycle}]] [-rp [RGB_SPEED]]
                          [-re [RGB_ENABLE]] [-rl [RGB_LED_COUNT]] [-u [{C,F}]] [-gm [GPIO_FAN_MODE]] [-gp [GPIO_FAN_PIN]]
                          [{start,stop}]

  Pironman5

  positional arguments:
    {start,stop}          Command

  options:
    -h, --help            show this help message and exit
    -c, --config          Show config
    -rc [RGB_COLOR], --rgb-color [RGB_COLOR]
                          RGB color in hex format with or without # (e.g. #FF0000 or 00aabb)
    -rb [RGB_BRIGHTNESS], --rgb-brightness [RGB_BRIGHTNESS]
                          RGB brightness 0-100
    -rs [{solid,breathing,flow,flow_reverse,rainbow,rainbow_reverse,hue_cycle}], --rgb-style [{solid,breathing,flow,flow_reverse,rainbow,rainbow_reverse,hue_cycle}]
                          RGB style
    -rp [RGB_SPEED], --rgb-speed [RGB_SPEED]
                          RGB speed 0-100
    -re [RGB_ENABLE], --rgb-enable [RGB_ENABLE]
                          RGB enable True/False
    -rl [RGB_LED_COUNT], --rgb-led-count [RGB_LED_COUNT]
                          RGB LED count int
    -u [{C,F}], --temperature-unit [{C,F}]
                          Temperature unit
    -gm [GPIO_FAN_MODE], --gpio-fan-mode [GPIO_FAN_MODE]
                          GPIO fan mode, 0: Always On, 1: Performance, 2: Cool, 3: Balanced, 4: Quiet
    -gp [GPIO_FAN_PIN], --gpio-fan-pin [GPIO_FAN_PIN]
                          GPIO fan pin

.. note::

  Jedes Mal, wenn Sie den Status von ``pironman5.service`` ändern, müssen Sie den folgenden Befehl verwenden, um die Konfigurationsänderungen wirksam zu machen.

  .. code-block:: shell

    sudo systemctl restart pironman5.service

* Überprüfen Sie den Status des ``pironman5``-Programms mit dem Tool ``systemctl``.

  .. code-block:: shell

    sudo systemctl status pironman5.service

* Alternativ können Sie die vom Programm generierten Logdateien überprüfen.

  .. code-block:: shell

    cat /opt/pironman5/log

RGB-LEDs steuern
----------------------
Die Platine verfügt über 4 WS2812 RGB-LEDs, die individuell gesteuert werden können. Benutzer können sie ein- oder ausschalten, die Farbe ändern, die Helligkeit anpassen, die Anzeigemodi der RGB-LEDs wechseln und die Geschwindigkeit der Änderungen einstellen.

.. note::

  Jedes Mal, wenn Sie den Status von ``pironman5.service`` ändern, müssen Sie den folgenden Befehl verwenden, um die Konfigurationsänderungen wirksam zu machen.

  .. code-block:: shell

    sudo systemctl restart pironman5.service

* Um den Ein- und Ausschaltzustand der RGB-LEDs zu ändern, verwenden Sie ``true`` zum Einschalten der RGB-LEDs und ``false`` zum Ausschalten.

.. code-block:: shell

  pironman5 -re true

* Um ihre Farbe zu ändern, geben Sie die gewünschten hexadezimalen Farbwerte ein, wie z.B. ``fe1a1a``.

.. code-block:: shell

  pironman5 -rc fe1a1a

* Um die Helligkeit der RGB-LEDs zu ändern (Bereich: 0 ~ 100%):

.. code-block:: shell

  pironman5 -rb 100

* Um die Anzeigemodi der RGB-LEDs zu wechseln, wählen Sie aus den Optionen: ``solid/breathing/flow/flow_reverse/rainbow/rainbow_reverse/hue_cycle``:

.. note::

  Wenn Sie den Anzeigemodus der RGB-LEDs auf ``rainbow``, ``rainbow_reverse`` oder ``hue_cycle`` setzen, können Sie die Farbe nicht mit ``pironman5 -rc`` ändern.

.. code-block:: shell

  pironman5 -rs breathing

* Um die Geschwindigkeit der Änderungen anzupassen (Bereich: 0 ~ 100%):

.. code-block:: shell

  pironman5 -rp 80

* Die Standardkonfiguration umfasst 4 RGB-LEDs. Schließen Sie zusätzliche LEDs an und aktualisieren Sie die Anzahl mit:

.. code-block:: shell

  pironman5 -rl 12

RGB-Lüfter steuern
-----------------------
Die IO-Erweiterungsplatine unterstützt bis zu zwei 5V nicht-PWM-Lüfter. Beide Lüfter werden zusammen gesteuert.

.. note::

  Jedes Mal, wenn Sie den Status von ``pironman5.service`` ändern, müssen Sie den folgenden Befehl verwenden, um die Konfigurationsänderungen wirksam zu machen.

  .. code-block:: shell

    sudo systemctl restart pironman5.service

* Sie können den Betriebsmodus der beiden RGB-Lüfter konfigurieren. Diese Modi bestimmen die Bedingungen, unter denen die RGB-Lüfter aktiviert werden.

Beispielsweise aktivieren sich die RGB-Lüfter im Modus **1: Performance** bei 50°C.

.. code-block:: shell

  sudo pironman5 -gm 3

* **4: Quiet**: Die RGB-Lüfter aktivieren sich bei 70°C.
* **3: Balanced**: Die RGB-Lüfter aktivieren sich bei 67,5°C.
* **2: Cool**: Die RGB-Lüfter aktivieren sich bei 60°C.
* **1: Performance**: Die RGB-Lüfter aktivieren sich bei 50°C.
* **0: Always On**: Die RGB-Lüfter sind immer eingeschaltet.

* Wenn Sie den Steuerpin des RGB-Lüfters an verschiedene Pins des Raspberry Pi anschließen, können Sie die Pin-Nummer mit dem folgenden Befehl ändern.

.. code-block:: shell

  sudo pironman5 -gp 18

OLED-Bildschirm überprüfen
-----------------------------------

Wenn Sie die Bibliothek ``pironman5`` installiert haben, zeigt der OLED-Bildschirm die CPU-, RAM- und Speichernutzung, die CPU-Temperatur und die IP-Adresse des Raspberry Pi an und zeigt dies jedes Mal nach dem Neustart an.

Wenn Ihr OLED-Bildschirm keinen Inhalt anzeigt, überprüfen Sie zunächst, ob das FPC-Kabel des OLED richtig angeschlossen ist.

Dann können Sie das Programmlog überprüfen, um das Problem mit dem folgenden Befehl zu erkennen.

.. code-block:: shell

  cat /var/log/pironman5/

Oder überprüfen Sie, ob die i2c-Adresse 0x3C des OLED erkannt wird:

.. code-block:: shell

  i2cdetect -y 1

Infrarot-Empfänger überprüfen
---------------------------------------

Um den IR-Empfänger zu nutzen, überprüfen Sie die Verbindung und installieren Sie das erforderliche Modul:

* Testen Sie die Verbindung:

  .. code-block:: shell

    sudo ls /dev | grep lirc

* Installieren Sie das Modul ``lirc``:

  .. code-block:: shell

    sudo apt-get install lirc -y

* Testen Sie nun den IR-Empfänger, indem Sie den folgenden Befehl ausführen.

  .. code-block:: shell

    mode2 -d /dev/lirc0

* Nach dem Ausführen des Befehls drücken Sie eine Taste auf der Fernbedienung, und der Code dieser Taste wird angezeigt.
