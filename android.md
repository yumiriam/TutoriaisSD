# Installing the ADT Plugin for Eclipse

1. Help > Install New Software
1. In the Available Software dialog, click Add...
1. In the Add Site dialog that appears, enter a name for the remote site
1. In the "Location" field, enter this URL:
	
	https://dl-ssl.google.com/android/eclipse/

	Note: If you have trouble acquiring the plugin, you can try using "http" in the URL, instead of "https" (https is preferred for security reasons).
1. Click OK.
1. In the Available Software view, select "Developer Tools", which will automatically select the nested tools Android DDMS and Android Development Tools.
1. Click Next.
1. In the Install Details dialog, the Android DDMS and Android Development Tools features are listed.
1. Click Next to read and accept the license agreement and install any dependencies, then click Finish.
1. Restart Eclipse.

# Configuring the ADT Plugin

1. Modify your ADT preferences in Eclipse to point to the Android SDK directory:
1. Window > Preferences...	
1. Select "Android"
1. Click Browse... and locate your downloaded SDK directory. 

	Download it here: http://developer.android.com/sdk/index.html
	[/home/miriam/android-sdk-linux]
1. Click Apply, then OK.

# Calling WS

http://www.ibm.com/developerworks/br/library/ws-android/index.html

## About complex types

http://code.google.com/p/ksoap2-android/wiki/CodingTipsAndTricks#sending/receiving_array_of_complex_types_or_primitives

## About file transfer

http://kkmishraksopa.blogspot.com.br/2011/01/serialize-byte-array-using-ksoap.html

## Some other informations may be necessary:

	envelope.dotNet = false;
	envelope.implicitTypes= true;
