# OpenVPN-Client-Android
<p>This is about how to set up the OpenVPN client on your Android phone with step-by-step instructions.</p>

<h2>Android</h2>

<p><br>Step 1: Find following 3 files on your OpenVPN server and copy to your Android phone</p>

<p>[[MORE]]</p>

<pre>
/etc/easy-rsa/easyrsa3/pki/ca.crt
/etc/easy-rsa/easyrsa3/pki/issued/android.crt
/etc/easy-rsa/easyrsa3/pki/private/android.key
</pre>

<p><br>Step 2: Create an OpenVPN client config file e.g.<b>android.ovpn</b> on your Android phone. Following is an example.</p>

<pre>
# Specify that we are a client and that we
# will be pulling certain config file directives
# from the server.
client


# Use the same setting as you are using on
# the server.
# On most systems, the VPN will not function
# unless you partially or fully disable
# the firewall for the TUN/TAP interface.
dev tun

# The hostname/IP and port of the server.
# You can have multiple remote entries
# to load balance between the servers.
remote ec2-1-2-3-4.x.compute.amazonaws.com 1194 udp

# Keep trying indefinitely to resolve the
# host name of the OpenVPN server.  Very useful
# on machines which are not permanently connected
# to the internet such as laptops.
resolv-retry infinite

# Most clients don't need to bind to
# a specific local port number.
nobind

# Try to preserve some state across restarts.
persist-key
persist-tun

# SSL/TLS parms.
# See the server config file for more
# description.  It's best to use
# a separate .crt/.key file pair
# for each client.  A single ca
# file can be used for all clients.
ca ca.crt
cert android.crt
key android.key

# Enable compression on the VPN link.
# Don't enable this unless it is also
# enabled in the server config file.
;comp-lzo

# Set log file verbosity.
verb 3

# Silence repeating messages
;mute 20
</pre>

<p><br>Step 3: Put ca.crt, android.crt, android.key and android.ovpn in the same folder on Android phone, i.e. /ovpn</p>

<p><br>Step 4: Install <b>OpenVPN Connect by OpenVPN</b> from Google Play</p>

<p><br>Step 5: Launch OpenVPN Connect on your Android phone and import <b>android.ovpn</b> by “Import Profile from SD Card”</p>

<p><br>Step 6: Enjoy safer Internet on your Android phone!</p>


<p><br><br>Are you also looking for the instructions for the server? No worries. Check this out - <a href="https://github.com/fredmeng/OpenVPN-Server" target="_blank">Build your private OpenVPN server on Amazon AWS</a>. </p>
