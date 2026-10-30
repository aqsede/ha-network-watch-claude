# ha-network-watch-claude
Claude made
# Network Watch – setup (about 15 minutes)

## 1. Add the files
Use the **File editor** or **Studio Code Server** add-on.

- `packages/network_watch.yaml` -> `/config/packages/network_watch.yaml`
- `dashboards/network_watch.yaml` -> `/config/dashboards/network_watch.yaml`

Add to `/config/configuration.yaml` (merge if you already have a `homeassistant:` or `lovelace:` block):

```yaml
homeassistant:
  packages: !include_dir_named packages

lovelace:
  dashboards:
    network-watch:
      mode: yaml
      title: Network Watch
      icon: mdi:shield-home
      show_in_sidebar: true
      filename: dashboards/network_watch.yaml
```

In `network_watch.yaml`, replace `notify.mobile_app_YOUR_PHONE` (2 places) with your phone's notify action.

## 2. Add two integrations (Settings -> Devices & services -> Add integration)
1. **Local To-do** -> name it exactly `Device Book` (entity must be `todo.device_book`).
2. **Nmap Tracker**
   - Hosts to scan: your LAN, e.g. `192.168.1.0/24` (same first 3 numbers as Home Assistant's IP)
   - Exclude: Home Assistant's own IP
   - Scan interval about 60 s; "minutes before marking away" about 3 (option names vary slightly by version)

## 3. Check config and restart
Developer tools -> YAML -> Check configuration -> Restart.

## 4. First-time enrollment (pick one)
**Careful way:** Network Watch -> Enroll. Pick a device from the dropdown, type a name, press TRUST. Repeat.
Tip: to find which entry is which phone, turn its Wi-Fi off and on and watch the dropdown.

**Fast way:** change the Wi-Fi password, reconnect only your own devices, then press
"Trust EVERYTHING connected right now". Rename them later from the device list on the Enroll tab.

## 5. From then on
A new device sends a push with: **That's mine** / **Name it** / **Not mine**.
Guest mode silences the push (the alert still appears in the HA sidebar).
