# Installation & Usage

## How to use

1.  **Install the add-on:** Go to the Add-on Store in Home Assistant and search for OpenSoho.
2.  **Configure (optional):** You can provide an `ssh_key` in the configuration if you want OpenSoho to use a specific private key to connect to your routers.
3.  **Start the add-on:** Click the "Start" button.
4.  **Open Web UI:** Click "Open Web UI" to access the OpenSoho dashboard via Ingress.
5.  **Create Superuser:** On the first run, the dashboard will provide a link to create your initial superuser account.

## Shared Secret

The add-on automatically generates a shared secret for device registration, which is stored in `/data/.shared_secret`. You will need this secret to configure your OpenWrt devices.

## SSH Access

The add-on can manage SSH keys in `/data/id_rsa`. If you provide an `ssh_key` in the configuration, it will be saved there. Otherwise, OpenSoho may generate its own keys in the `/data` directory.

## Persistence

All configuration and the PocketBase database are stored in the `/data` directory of the add-on, ensuring persistence across restarts and updates.
