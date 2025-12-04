# Docker XPRA Display for RViz2
Browser-based RViz2 using XPRA HTML5. Works on Windows/macOS/Linux without X11 or VNC clients.

## Quick Test

```bash
docker compose -f docker-compose.run-without-config.yml up
```

Open **http://localhost:14500/**

## Production Use

Copy files to your project:
```bash
cp -r rviz-xpra/ /your/project/
cp docker-compose.prod_xpra.yml /your/project/
```

Edit `docker-compose.prod_xpra.yml`:

1. **Service name** — change `your_ros_service` to your service name
2. **RViz config path** — update volume mount to your config directory:
   ```yaml
   volumes:
     - fleet_rviz_config:/your/path/to/rviz/config
   ```
3. **Config filename** — change `your_config.rviz` in the command:
   ```yaml
   --start-child='rviz2 -d /fleet_config/your_config.rviz'
   ```
4. **ROS settings** — match your `ROS_DOMAIN_ID` and `network_mode`

Run:
```bash
docker compose -f docker-compose.prod.yml -f docker-compose.prod_xpra.yml up
```

Access: **http://localhost:14500/**

## Notes

- Config persists in `rviz_config` volume
- XPRA exits when RViz closes
- Uses named volume to share config between containers
- Port 14500 ignored if using `network_mode: host`

---

**Credits:** This documentation and code were developed with assistance from Anthropic's Claude Sonnet 4.5 model via GitHub Copilot.
