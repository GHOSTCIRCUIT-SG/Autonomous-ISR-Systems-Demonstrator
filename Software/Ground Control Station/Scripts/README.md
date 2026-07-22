TOMTOM OpenTAK + MAVLink Integration
This package preserves the working code and setup used for:
PX4 / MAVLink -> Python bridge -> OpenTAKServer -> ATAK
Included files
`mavlink_bridge.py`: live MAVLink-to-CoT bridge
`send_test.py`: fixed-marker TAK connection test
`bridge.ini.template`: PyTAK TLS configuration template
`tomtom-mavlink-bridge.service`: automatic systemd service
`install_service.sh`: service installer
`COMMANDS.md`: setup, operation, and troubleshooting commands
Current working paths
Project: `/home/serena/tomtom-bridge`
Python environment: `/home/serena/tomtom-venv`
OpenTAK host: `tak.tomtomtak.com`
TAK TLS port: `8089`
MAVLink input: `udpin:0.0.0.0:14540`
Security
No account password is included.
The current proof-of-concept configuration disables TAK TLS hostname and certificate verification. Replace the port-8089 certificate with one valid for `tak.tomtomtak.com`, then remove those bypass settings.
