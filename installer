#!/bin/bash

clear
echo "======================================"
echo "       ZK-MC3 DAEMON INSTALLER"
echo "======================================"
echo ""

echo "Extracting daemon..."
unzip zkdaemon.zip
cd zkdaemon || exit 1

echo ""
echo "======================================"
echo " Configure your ZK-MC3 Daemon"
echo "======================================"
echo ""
echo "Edit config.json and add:"
echo "  - token"
echo "  - panelurl"
echo "  - nodename"
echo ""
echo "When you have finished editing config.json,"
echo "type YES to continue."
echo ""

read -p "Type YES to continue: " CONFIRM

if [[ "$CONFIRM" != "yes" && "$CONFIRM" != "YES" ]]; then
    echo ""
    echo "Installation cancelled."
    exit 0
fi

echo ""
echo "Installing required packages..."
sudo apt update && sudo apt install -y openjdk-17-jdk nodejs npm

if [ $? -ne 0 ]; then
    echo ""
    echo "Package installation failed."
    exit 1
fi

echo ""
echo "======================================"
echo "       TOKEN CONFIGURATION"
echo "======================================"
echo ""
read -r -s -p "Paste your full token: " TOKEN
echo ""

if [ -z "$TOKEN" ]; then
    echo "Error: Token cannot be empty."
    exit 1
fi

# Safely update token in config.json
if command -v jq >/dev/null 2>&1; then
    tmp=$(mktemp)
    jq --arg token "$TOKEN" '.token = $token' config.json > "$tmp" &&
        mv "$tmp" config.json
else
    echo ""
    echo "jq is not installed, so the token could not be"
    echo "automatically written to config.json."
    echo "Please add the token manually."
    exit 1
fi

echo ""
echo "======================================"
echo "       ZK-MC3 DAEMON READY"
echo "======================================"
echo ""
echo "Daemon installation completed successfully."
echo "======================================"
