# Steps to Run an Etherify Node

#### Step 1: Set Up a Directory and Download Files

1. Create a new folder where you want to store your Etherify node files.
2. Download the Etherify Node Client and the genesis file (`etherify.json`) and place them in this folder.

#### Step 2: Initialize the Genesis Block and Define the Directory

Run the following command to initialize the genesis block and specify the data directory:

```bash
./geth --datadir data init etherify.json
```

This command initializes the data folder (`data`) using the genesis file (`etherify.json`).

#### Step 3: Start the Node in Fullsync Mode

To start your node, use the `geth` command with the `console` flag to enable interaction:

```bash
./geth --datadir ./data --networkid 1505 --port 22202 --http --http.addr 0.0.0.0 --http.port 8545 --http.api personal,eth,net,web3,miner --http.corsdomain "*" --syncmode "full" console
```

This starts the node in full synchronization mode and provides access to an interactive console.

#### Step 4: Add Peers for Network Synchronization

To begin syncing with the network, add peers using the `admin.addPeer` command:

```javascript
admin.addPeer(
	"enode://f63dda6960c7fe758552fb9e25283445dd0f5726db56eab6a3dd9560230b357d50e33c449da632ce977b42f48b9159e09355e567862a266f5c2532148727cc52@139.180.145.179:22202"
);

admin.addPeer(
	"enode://0cba91a27b0b4ec4ef77cfca9b5d6edd89d10f241b175be903ccbb0e70d4889e01579200583627408e6c05b19209fd71bfca36baddeb0d702750bb728b88fd7a@140.82.8.255:22202"
);
```

Adding these peers will connect your node to the network and initiate synchronization.

#### Step 5: Run or Restart the Node

After adding peers, you may keep the node running or restart it without the `console` flag for non-interactive operation.

To enable mining, use the `--mine` flag with additional mining parameters:

```bash
./geth --datadir ./data --networkid 1505 --port 22202 --http --http.addr 0.0.0.0 --http.port 8545 --http.api personal,eth,net,web3,miner --http.corsdomain "*" --syncmode "full" --mine --miner.threads=1 --miner.etherbase 0xYourEthereumAddress
```

Replace `0xYourEthereumAddress` with your own Ethereum address to receive mining rewards.

---

### Additional Information

#### Port Configuration for Running an Etherify Node

The port settings can be customized to match your network configuration and security preferences.

-   **P2P Port (`--port`)**: Used for peer-to-peer networking. In this example, it’s set to `22202`, but any open port not in conflict with other services on your system can be used. Ensure your firewall permits the chosen port.
-   **HTTP Port (`--http.port`)**: Enables HTTP-based communication with the node’s API, defaulting to `8545` but customizable to any valid port number. Configure firewall settings accordingly to prevent unauthorized access.
-   **WebSocket Port (`--ws.port`)**: Used for real-time WebSocket communication. It often defaults to `8546` but can be modified to any open port. Ensure the port is allowed in the firewall for WebSocket use.

To adjust the ports, use the following syntax:

```bash
--port <your_desired_port> --http.port <your_http_port> --ws.port <your_ws_port>
```

Choosing unique ports outside common ranges can help improve security, though ensure these ports are allowed for connectivity with the Etherify network.

-   **API Exposure**: Adjust the `--http.api` and `--ws.api` options based on your API exposure needs.
-   **Security Considerations**: Configure your firewall and HTTP settings to secure your node, particularly on open networks.

---

### Troubleshooting

-   **Genesis File Error**: Verify that the genesis file path is correct during initialization.
-   **Connection Issues**: Ensure your firewall settings allow the necessary ports for peer-to-peer connectivity.

---

Enjoy running your Etherify node! For further assistance, feel free to open an issue in the official repository.

