1. Create a folder structure for .deb packaging
    mkdir -p fourchannel_deb/usr/local/bin
    mkdir -p fourchannel_deb/DEBIAN

2. Copy the PyInstaller output
    cp -r /home/sai/Desktop/rasperripi_mini/four_channel/dist/four_channel fourchannel_deb/usr/local/bin/fourchannel

3. Create the control file
    Package: fourchannel
    Version: 1.0
    Section: base
    Priority: optional
    Architecture: arm64
    Maintainer: sai <gaugelogic.report@gmail.com>
    Description: Multi-channel system application


4. Make your executable scriptable
    sudo nano fourchannel_deb/usr/local/bin/fourchannel-launch

    #!/bin/bash
    /usr/local/bin/fourchannel/your_app_executable

    sudo chmod +x fourchannel_deb/usr/local/bin/fourchannel-launch



5. Create a directory for .desktop files inside your deb folder:

    mkdir -p fourchannel_deb/usr/share/applications

    nano fourchannel_deb/usr/share/applications/fourchannel.desktop



[Desktop Entry]
Name=FourChannel
Exec=/usr/local/bin/fourchannel-launch
Icon=/usr/local/bin/four_channel/sai.png
Type=Application
Terminal=false
Categories=Utility;



6. Build the .deb file
    dpkg-deb --build fourchannel_deb


7. Test it on another Raspberry Pi
    sudo dpkg -i fourchannel_deb.deb



`DESKTOP SHORTYCUT CREATE:`

cp /usr/share/applications/fourchannel.desktop ~/Desktop/
chmod +x ~/Desktop/fourchannel.desktop


`DELETE COMMAND FOR INSTALLED APPS:`

sudo rm -r /usr/local/bin/fourchannel-launch


`REPLACE THE CURRENT DB WITH YOUR BACKUP`:

cp /home/sai/Downloads/backup_20250429_112908/db_backup_20250429_112908.sqlite3 /home/sai/Desktop/rasperripi_mini/four_channel/db.sqlite3

`Ensure correct permissions:`

chmod 664 /home/sai/Desktop/rasperripi_mini/four_channel/db.sqlite3
chown sai:sai /home/sai/Desktop/rasperripi_mini/four_channel/db.sqlite3




