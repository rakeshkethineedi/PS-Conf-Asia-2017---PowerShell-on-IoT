# PS Conf Aisa 2017 - PowerShell on IoT
This repo contains the resources I used during my session on using PowerShell on IoT, at the Powershell Conference Asia 2017.

Raspberry Pi setup using Windows 10 IoT core reference - https://developer.microsoft.com/en-us/windows/iot/getstarted

Connection Setup
Once your Windows 10 IoT core is installed on the Raspberry Pi as per the PPT, copy the PowerPiLib.dll on to the Raspberry Pi.
Connect the positive side of your LED to GPIO 5 pin or Physical pin 29.
and the negative side to the ground (GND) pin or Physical pin 1.
For setup, load the PowerPiLib.dll in WinIoT powershell console (accessed via Powershell Remoting).
PowerPiLib.dll is generated from the C# solution. Code is placed in powerpi-master folder.

DEMO Powershell commands
#To initiate Powershell remoting, use the below commands
net start WinRM
Set-Item WSMan:\localhost\client\TrustedHosts -Value <raspberry pi hostname or ip address>
Enter-PSSession –ComputerName <hostname> -Credential <username>
#Password prompt will appear. Enter the password.

#Loading the DLL
Add-Type -Path .\PowerPiLib.dll
$ioValue = New-Object PowerPiLib.GpioValue
$ioHelper = New-Object PowerPiLib.GpioHelper

#To turn off LED:
$ioHelper.Pin = $ioValue::High

#To turn on LED:
$ioHelper.Pin = $ioValue::Low 

#To blink every 1 second
while($true)
{
    $ioHelper.Pin = @{$true=$ioValue::Low;$false=$ioValue::High}[$ioHelper.Pin -eq $ioValue::High]  
    start-sleep -m 1000
}



IotStartup list – Lists the apps that will start at the startup
IotStartup list headed – Lists headed apps
IotStartup list headless – Lists headless apps
IotStartup remove – Removes headed and headless apps
IotStartup remove headed [MyApp] removes headed applications that match pattern MyApp
IotStartup Help

ScreenCapture c:\folder\screencap.jpg

Change password
net user Administrator [new password]

Exit-PSSession

Enter-PSSession with new credentials

Set computer name
setcomputername <new-name>

Restart computer to let the change take effect - shutdown /r /t 0

GetAdapterInfo




