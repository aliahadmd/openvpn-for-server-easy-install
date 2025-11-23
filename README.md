## Initial Setup:

# 1. Initialize the OpenVPN configuration
docker compose run --rm openvpn ovpn_genconfig -u udp://ipaddr:9999

# 2. Generate the PKI (you'll be prompted to set a passphrase)
docker compose run --rm openvpn ovpn_initpki

# 3. Start the OpenVPN server
docker compose up -d



====================================

## Create a client certificate:
# Replace CLIENT_NAME with your desired client name
docker compose run --rm openvpn easyrsa build-client-full CLIENT_NAME nopass

# Export the client configuration
docker compose run --rm openvpn ovpn_getclient CLIENT_NAME > CLIENT_NAME.ovpn


====================
The configuration uses:

Port 9999 for UDP traffic (standard OpenVPN)
Port 9998 for TCP traffic (fallback option)
Your server IP: ipaddr
Data persisted in ./openvpn-data directory
Once running, clients can connect using the generated .ovpn file.
