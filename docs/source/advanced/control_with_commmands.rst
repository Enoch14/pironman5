.. _view_control_commands:

コマンドによる表示と制御
=======================================
Pironman 5からのデータを表示し、ダッシュボードを通じて様々なデバイスを制御することに加え、コマンドを使用してそれらを制御することもできます。


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


* ``pironman5`` プログラムの状態を ``systemctl`` ツールを使用して確認します。

  .. code-block:: shell

    sudo systemctl status pironman5.service

* または、プログラムが生成したログファイルを調査します。

  .. code-block:: shell

    cat /opt/pironman5/log


RGB LEDの制御
----------------------
このボードには4つのWS2812 RGB LEDが搭載されており、カスタマイズ可能な制御が可能です。ユーザーはLEDをオンまたはオフにしたり、色を変更したり、明るさを調整したり、RGB LEDの表示モードを切り替えたり、変更の速度を設定したりできます。

.. note::

  ``pironman5.service`` の状態を変更するたびに、設定変更を有効にするために次のコマンドを使用する必要があります。

  .. code-block:: shell

    sudo systemctl restart pironman5.service

* RGB LEDのオン/オフ状態を変更するには、 ``true`` でRGB LEDをオンにし、 ``false`` でオフにします。

.. code-block:: shell

  pironman5 -re true

* 色を変更するには、希望の16進数カラーコードを入力します。例えば ``fe1a1a`` です。

.. code-block:: shell

  pironman5 -rc fe1a1a

* RGB LEDの明るさを変更する（範囲: 0〜100%）:

.. code-block:: shell

  pironman5 -rb 100

* RGB LED表示モードを切り替えるには、次のオプションから選択します: ``solid/breathing/flow/flow_reverse/rainbow/rainbow_reverse/hue_cycle``:

.. note::

  RGB LED表示モードを ``rainbow``、 ``rainbow_reverse``、または ``hue_cycle`` に設定した場合、 ``pironman5 -rc`` を使用して色を設定することはできません。

.. code-block:: shell

  pironman5 -rs breathing

* 変更速度を修正する（範囲: 0〜100%）:

.. code-block:: shell

  pironman5 -rp 80

* 初期設定では4つのRGB LEDが含まれています。追加のLEDを接続し、LEDの数を更新するには:

.. code-block:: shell

  pironman5 -rl 12

RGBファンの制御
---------------------
IO拡張ボードは、最大2つの5V非PWMファンをサポートしています。これらのファンは一緒に制御されます。

.. note::

  ``pironman5.service`` の状態を変更するたびに、設定変更を有効にするために次のコマンドを使用する必要があります。

  .. code-block:: shell

    sudo systemctl restart pironman5.service

* RGBファンの動作モードを設定するコマンドを使用できます。これらのモードはRGBファンが作動する条件を決定します。

例えば、 **1: パフォーマンス** モードに設定すると、RGBファンは50°Cで動作します。

.. code-block:: shell

  sudo pironman5 -gm 3

* **4: 静か**: RGBファンは70°Cで動作します。
* **3: バランス**: RGBファンは67.5°Cで動作します。
* **2: クール**: RGBファンは60°Cで動作します。
* **1: パフォーマンス**: RGBファンは50°Cで動作します。
* **0: 常時オン**: RGBファンは常に動作します。

* Raspberry Piの異なるピンにRGBファンの制御ピンを接続する場合、以下のコマンドを使用してピン番号を変更できます。

.. code-block:: shell

  sudo pironman5 -gp 18

OLEDスクリーンの確認
-----------------------------------

 ``pironman5`` ライブラリをインストールすると、OLEDスクリーンにはCPU、RAM、ディスク使用量、CPU温度、およびRaspberry PiのIPアドレスが表示され、再起動するたびにこれが表示されます。

OLEDスクリーンに何も表示されない場合は、まずOLEDのFPCケーブルが正しく接続されているかを確認する必要があります。

次に、以下のコマンドを使用してプログラムログを確認し、問題の原因を調べることができます。

.. code-block:: shell

  cat /var/log/pironman5/

または、OLEDのi2cアドレス0x3Cが認識されているかどうかを確認します：

.. code-block:: shell

  i2cdetect -y 1

赤外線レシーバのチェック
---------------------------------------

IRレシーバを利用するには、その接続を確認し、必要なモジュールをインストールします：

* 接続をテストします：

  .. code-block:: shell

    sudo ls /dev | grep lirc

* ``lirc`` モジュールをインストールします：

  .. code-block:: shell

    sudo apt-get install lirc -y

* 以下のコマンドを実行してIRレシーバをテストします。

  .. code-block:: shell

    mode2 -d /dev/lirc0

* コマンドを実行した後、リモコンのボタンを押すと、そのボタンのコードが表示されます。

