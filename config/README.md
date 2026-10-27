# Node-RED flow

`flows.json` in this folder is currently a **placeholder**: it contains only the client config node, not the full flow. The flow that was built is documented node by node in [docs/01](../docs/01-setup-and-tools.md#node-red-flow) and shown in [images/node-red-flow.png](../images/node-red-flow.png).

## Adding the real export

1. Open Node-RED (`http://localhost:1880`).
2. Menu **☰ → Export**, select **all flows** (or the "Flow 1" tab), choose **JSON**, then **Download**.
3. Replace `config/flows.json` in this repo with the downloaded file (GitHub: **Add file → Upload files**).

## Importing

Menu **☰ → Import**, paste or select `flows.json`, then **Import** and **Deploy**. `node-red-contrib-modbus` must already be installed.
