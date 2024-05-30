.. note::

    こんにちは、SunFounderのRaspberry Pi & Arduino & ESP32愛好家コミュニティへようこそ！Facebook上でRaspberry Pi、Arduino、ESP32についてもっと深く掘り下げ、他の愛好家と交流しましょう。

    **参加する理由は？**

    - **エキスパートサポート**：コミュニティやチームの助けを借りて、販売後の問題や技術的な課題を解決します。
    - **学び＆共有**：ヒントやチュートリアルを交換してスキルを向上させましょう。
    - **独占的なプレビュー**：新製品の発表や先行プレビューに早期アクセスしましょう。
    - **特別割引**：最新製品の独占割引をお楽しみください。
    - **祭りのプロモーションとギフト**：ギフトや祝日のプロモーションに参加しましょう。

    👉 私たちと一緒に探索し、創造する準備はできていますか？[|link_sf_facebook|]をクリックして今すぐ参加しましょう！

.. _set_up_pironman5:

5. Pironman 5のセットアップ
===================================

設定前の準備
-----------------------
電源を入れた後は、各種の電源LEDが点灯しているだけで、OLED画面（画面の乱れがある場合は、設定後に解決されるため無視してください）、RGB LED、RGBファン（側面の2つのファン）はまだ動作しません。これらは設定が必要です。

電源ボタンはRaspberry Pi 5の電源ボタンと同様の機能を持ちます。

 **シャットダウン** 

    * Raspberry Pi  **Bookworm Desktop** システムを使用している場合、電源ボタンを素早く2回押すとシャットダウンします。
    * Raspberry Pi  **Bookworm Lite** システムを使用している場合、電源ボタンを1回押すとシャットダウンが開始されます。
    * 強制シャットダウンを行うには、電源ボタンを押し続けます。

 **電源オン** 

    * Raspberry Piボードがシャットダウンされているが、まだ電源が供給されている場合、1回押すとシャットダウン状態から電源がオンになります。

.. note::

    シャットダウンボタンをサポートしていないシステムを使用している場合、5秒間押し続けると強制シャットダウンが行われ、1回押してシャットダウン状態から電源をオンにできます。


GPIO電源を無効にするためのシャットダウンの設定
------------------------------------------------------------
Raspberry PiのGPIOで電源供給されるOLED画面やRGBファンがシャットダウン後も動作し続けないようにするために、GPIO電源無効化の設定が必要です。

* 次のコマンドを使用して ``EEPROM`` 設定ファイルを手動で編集します：

  .. code-block:: shell

    sudo rpi-eeprom-config -e

* ファイル内の ``POWER_OFF_ON_HALT`` 設定を ``1`` に変更します。例えば：

  .. code-block:: shell

    BOOT_UART=1
    POWER_OFF_ON_HALT=1
    BOOT_ORDER=0xf41

* 変更を保存するには、「Ctrl + X」、「Y」、「Enter」を押します。


``pironman5`` モジュールのダウンロードとインストール
-----------------------------------------------------------

.. note::

  Liteシステムの場合、最初に ``git``、 ``python3``、 ``pip3``、 ``setuptools`` などのツールをインストールしてください。
  
  .. code-block:: shell
  
    sudo apt-get update
    sudo apt-get install git -y
    sudo apt-get install python3 python3-pip python3-setuptools -y

GitHubからコードをダウンロードし、 ``pironman5`` モジュールをインストールします。

.. code-block:: shell

  cd ~
  git clone https://github.com/sunfounder/pironman5.git
  cd ~/pironman5
  sudo python3 install.py

インストールが成功した後、インストールを有効にするためにシステムの再起動が必要です。画面の再起動プロンプトに従ってください。

再起動後、 ``pironman5.service`` が自動的に開始されます。以下は、 |link_pironman5| の主な設定内容です：

  * OLED画面には、CPU、RAM、ディスク使用量、CPU温度、Raspberry PiのIPアドレスが表示されます。
  * 4つのWS2812 RGB LEDが青色のブリージングモードで点灯します。

``systemctl`` ツールを使用して、 ``pironman5.service`` の ``start``、 ``stop``、 ``restart``、または ``status`` を確認できます。

.. code-block:: shell

  sudo systemctl restart pironman5.service

* ``restart``: Pironman 5の設定変更を適用するために使用します。
* ``start/stop``: ``pironman5.service`` を有効または無効にします。
* ``status``: ``systemctl`` ツールを使用して ``pironman5`` プログラムの動作状態を確認します。

基本設定の表示
-----------------------------------

``pironman5`` モジュールはPironmanの基本設定を提供し、以下のコマンドで確認できます。

.. code-block:: shell

  pironman5 -c

標準的な設定は以下の通りです：

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

これらの設定を必要に応じてカスタマイズしてください。

使い方については、 ``pironman5`` または ``pironman5 -h`` を使用してください。

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

  ``pironman5.service`` の状態を変更するたびに、以下のコマンドを使用して設定変更を有効にする必要があります。

  .. code-block:: shell

    sudo systemctl restart pironman5.service


* または、プログラムが生成したログファイルを調査します。

  .. code-block:: shell

    cat /opt/pironman5/log

.. note::

  * 次に、ダッシュボードから |link_pironman5| のコンポーネントを表示および制御できます。詳細については :ref:`view_control_dashboard` を参照してください。
  * コマンドを使用したい場合は、 :ref:`view_control_commands` を参照してください。

