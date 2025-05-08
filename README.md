#!/bin/bash

# Set the full path to your RPM file (DO NOT delete or modify this)
RPM_FILE="StarburstODBC-32bit-2.2.0.1002.el8.i686.rpm"

# Target directory where the .so file should go
DEST_DIR="/efs/starburst/odbc_drivers/so"

# Create destination directory if it doesn't exist
mkdir -p "$DEST_DIR"

# Create temporary working directory
TMP_DIR=$(mktemp -d)

# Go to the temp directory
cd "$TMP_DIR" || exit 1

# Extract only the .so file without touching other paths
rpm2cpio "/full/path/to/$RPM_FILE" | \
cpio -idmv './opt/starburst/starburstodbc/lib/32/StarburstODBC_sb32.so'

# Move only the .so file to your destination
mv ./opt/starburst/starburstodbc/lib/32/StarburstODBC_sb32.so "$DEST_DIR/"

# Go back and clean the temp folder
cd ~
rm -rf "$TMP_DIR"

# Final message
echo "✔️  StarburstODBC_sb32.so copied to $DEST_DIR"
