FAQ
============

OLED画面が表示されない？
----------------------------------

OLED画面が表示されない、または正しく表示されない場合、以下の手順に従って問題をトラブルシューティングしてください。

OLED画面のFPCケーブルが正しく接続されているか確認してください。

#. 次のコマンドを使用してプログラムの実行ログを表示し、エラーメッセージがないか確認します。

    .. code-block:: shell

        cat /opt/pironman5/log

#. または、次のコマンドを使用してOLEDのi2cアドレス0x3Cが認識されているか確認します：
    
    .. code-block:: shell
        
        sudo i2cdetect -y 1

#. 最初の2つの手順で問題が見つからない場合は、pironman5サービスを再起動して問題が解決するか確認します。

    .. code-block:: shell

        sudo systemctl restart pironman5.service

.. _openssh_powershell:

Powershellを使ってOpenSSHをインストールする
----------------------------------------------------

``ssh <username>@<hostname>.local`` （または ``ssh <username>@<IP address>`` ）を使用してRaspberry Piに接続しようとしたとき、次のエラーメッセージが表示される場合があります。

    .. code-block::

        ssh: The term 'ssh' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the
        spelling of the name, or if a path was included, verify that the path is correct and try again.

これは、コンピューターのシステムが古く、 `OpenSSH <https://learn.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse?tabs=gui>`_ が事前にインストールされていないことを意味します。以下の手順に従って手動でインストールしてください。

#. Windowsデスクトップの検索ボックスに ``powershell`` と入力し、 ``Windows PowerShell`` を右クリックして、表示されるメニューから ``管理者として実行`` を選択します。

    .. image:: img/powershell_ssh.png
        :align: center

#. 次のコマンドを使用して ``OpenSSH.Client`` をインストールします。

    .. code-block::

        Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

#. インストール後、次の出力が返されます。

    .. code-block::

        Path          :
        Online        : True
        RestartNeeded : False

#. 次のコマンドを使用してインストールを確認します。

    .. code-block::

        Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'

#. これで ``OpenSSH.Client`` が正常にインストールされたことがわかります。

    .. code-block::

        Name  : OpenSSH.Client~~~~0.0.1.0
        State : Installed

        Name  : OpenSSH.Server~~~~0.0.1.0
        State : NotPresent

    .. warning:: 
        上記のプロンプトが表示されない場合、Windowsシステムがまだ古すぎることを意味します。 |link_putty| のようなサードパーティのSSHツールをインストールすることをお勧めします。

#. PowerShellを再起動し、再度管理者として実行します。この時点で ``ssh`` コマンドを使用してRaspberry Piにログインできるようになり、先に設定したパスワードの入力を求められます。

    .. image:: img/powershell_login.png

