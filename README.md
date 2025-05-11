📥 Installation# Aztec-Node
1st. Install curl and wget first
command -v curl >/dev/null 2>&1 || apt-get update && apt-get install -y curl; command -v wget >/dev/null 2>&1 || apt-get install -y wget

2nd. Execute either of the following commands to run your Aztec node
[ -f "aztec.sh" ] && rm aztec.sh; curl -sSL -o aztec.sh https://raw.githubusercontent.com/zunxbt/aztec-sequencer-node/main/aztec.sh && chmod +x aztec.sh && ./aztec.sh

3rd.You can use this command to check logs of your node
sudo docker logs -f --tail 100 $(docker ps -q --filter ancestor=aztecprotocol/aztec:latest | head -n 1)

4th.After running node, you should wait at least 10 to 20 mins before your run these commands
Use this command to get block-number
curl -s -X POST -H 'Content-Type: application/json' -d '{"jsonrpc":"2.0","method":"node_getL2Tips","params":[],"id":67}' http://localhost:8080 | jq -r '.result.proven.number'

5th. After running this code, you will get a block number like this : 66666

Use that block number in the places of block-number in the below command to get proof
curl -s -X POST -H 'Content-Type: application/json' -d '{"jsonrpc":"2.0","method":"node_getArchiveSiblingPath","params":["block-number","block-number"],"id":67}' http://localhost:8080 | jq -r ".result"

6th.Now join Azrec Discord- https://discord.com/invite/aztec
Use the following command to get Apprentice role
/operator start
It will ask the address , block-number and proof , Enter all of them one by one and you will get Apprentice instantly

egister as Validator
Warning

You may see an error like ValidatorQuotaFilledUntil when trying to register as a validator, which means the daily quota has been reached—convert the provided Unix timestamp to local time to know when you can try again to register as Validator.

Replace SEPOLIA-RPC-URL , YOUR-PRIVATE-KEY , YOUR-VALIDATOR-ADDRESS with actual value and then execute this command
aztec add-l1-validator \
  --l1-rpc-urls SEPOLIA-RPC-URL \
  --private-key YOUR-PRIVATE-KEY \
  --attester YOUR-VALIDATOR-ADDRESS \
  --proposer-eoa YOUR-VALIDATOR-ADDRESS \
  --staking-asset-handler 0xF739D03e98e23A7B65940848aBA8921fF3bAc4b2 \
  --l1-chain-id 11155111
