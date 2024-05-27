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

.. note::

  * 次に、ダッシュボードから |link_pironman5| のコンポーネントを表示および制御できます。詳細については :ref:`view_control_dashboard` を参照してください。
  * コマンドを使用したい場合は、 :ref:`view_control_commands` を参照してください。

