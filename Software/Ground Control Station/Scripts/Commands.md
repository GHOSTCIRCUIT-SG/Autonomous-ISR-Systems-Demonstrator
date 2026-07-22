TOMTOM Commands
Activate environment
```bash
source ~/tomtom-venv/bin/activate
```
Install Python dependencies
```bash
python -m pip install --upgrade "pytak[with-crypto]" pymavlink aiohttp
```
Static marker test
```bash
cd ~/tomtom-bridge
source ~/tomtom-venv/bin/activate
python send_test.py
```
ATAK marker: `TOMTOM TEST`
Coordinates: `26.3344, 127.8056`
PX4 SITL
```bash
cd ~/PX4-Autopilot
source ~/tomtom-venv/bin/activate
make px4_sitl gz_x500
```
Manual MAVLink bridge
```bash
cd ~/tomtom-bridge
source ~/tomtom-venv/bin/activate
python mavlink_bridge.py
```
Service management
```bash
sudo systemctl status tomtom-mavlink-bridge
journalctl -u tomtom-mavlink-bridge -f
sudo systemctl restart tomtom-mavlink-bridge
sudo systemctl stop tomtom-mavlink-bridge
sudo systemctl start tomtom-mavlink-bridge
sudo systemctl disable --now tomtom-mavlink-bridge
sudo systemctl enable --now tomtom-mavlink-bridge
```
OpenTAKServer and NGINX
```bash
sudo systemctl status opentakserver
sudo systemctl restart opentakserver
sudo nginx -t
sudo systemctl restart nginx
```
Current router forwards
TCP 443 -> 192.168.50.187:443
TCP 8089 -> 192.168.50.187:8089
TCP 8446 -> 192.168.50.187:8446
TCP 8443 -> 192.168.50.187:8443
Changing to a real flight controller
Edit this line in `mavlink_bridge.py`:
```python
MAVLINK_ENDPOINT = "udpin:0.0.0.0:14540"
```
For USB serial, change it to the detected device, such as:
```python
MAVLINK_ENDPOINT = "/dev/ttyACM0"
```
Then add the required baud rate in `mavutil.mavlink_connection()`, for example:
```python
connection = mavutil.mavlink_connection(
    MAVLINK_ENDPOINT,
    baud=115200,
    autoreconnect=True,
)
```
Restart the service after any edit:
```bash
sudo systemctl restart tomtom-mavlink-bridge
journalctl -u tomtom-mavlink-bridge -f
```
