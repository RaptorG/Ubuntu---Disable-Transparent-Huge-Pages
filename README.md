# Ubuntu---Disable-Transparent-Huge-Pages

# Create an SYSTEMD configuration file

vi /etc/systemd/system/disable-thp.service

# Paste the following

[Unit]
Description=Disable Transparent Huge Pages (THP)
DefaultDependencies=no
After=sysinit.target local-fs.target
[Service]
Type=oneshot
ExecStart=/bin/sh -c 'echo never | tee /sys/kernel/mm/transparent_hugepage/enabled > /dev/null'
[Install]
WantedBy=basic.target

# Reload the services configuration

systemctl daemon-reload

# Start the created service

systemctl start disable-thp

# Verify if the Transparent Huge Pages were disabled

cat /sys/kernel/mm/transparent_hugepage/enabled

# Command output.

always madvise [never]

# Enable the created service during boot

systemctl enable disable-thp

# Reboot the computer

reboot
