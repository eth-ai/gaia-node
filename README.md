# Gaia Node

This repo contains all the information, requirements, and knowledge base for the Gaia Node. One can follow this repo and run the same Gaia Node on their own machine.

## Knowledge Base

We have used the official [Ethereum documentation](https://ethereum.org/en/developers/docs/) as a knowledge base. There's a lot of information that can be extracted from those docs and make the knowledge base complex. Thus, we used GPT-4 to create a knowledge base in a Q&A format which you can find [here](/eth-qa.txt).

In order to run the Gaia Node and use this particular knowledge base, you need to follow the steps below:

1. Run the following command to install the latest version of the Gaia Node (it will be better to have cuda-enabled GPU for faster processing, in order to check whether your GPU is cuda enabled or not, run `nvcc --version` & `nvidia-smi`):

```bash
curl -sSfL 'https://github.com/GaiaNet-AI/gaianet-node/releases/latest/download/install.sh' | bash
```

2. Next, set up the environment path. Just read the instructions after it logs out of your node id, there you will find the required command to do that. It will look something like this `source/users/<your-user-name>/.bashrc`.

3. Now we have to initialize the Gaia node using `gaianet init`, make sure that the default model that will be installed is `Llama 3.2` as per the current release. To initialize a different model, choose one from [here](https://github.com/GaiaNet-AI/node-configs/tree/main) and run the command provided in its README. It will look something like this:

```bash
gaianet init --config https://raw.githubusercontent.com/GaiaNet-AI/node-configs/main/llama-3.1-8b-instruct/config.json
```

4. Now here you have to update your config file with the knowledge base and the system prompt you want to use. Well, you can make other changes as well, but for now, we will only focus on the knowledge base and the system prompt. To do that, run the following command:

```bash
gaianet config --snapshot https://huggingface.co/datasets/NoMercy0034/Ethereum_QA/resolve/main/default-3824708441112748-2025-02-04-20-02-58.snapshot.tar.gz --system-prompt "You are a helpful assistant who answers questions about Ethereum Ecosystem in short and concise manner.."
```

The system prompt provides background and personality to the node. You can change it as you've asked.

5. Finally, start the Gaia node using the following command:

```bash
gaianet start
```

A successful start prints a public URL for the node. Opening a browser to that URL will display the node information and allow you to chat with the AI agent on the node.
