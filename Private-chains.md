Parity supports private chain and private network configuration via [chain specification](https://github.com/ethereum/wiki/wiki/Ethereum-Chain-Spec-Format) files provided with `--chain`. The best way to create such a configuration is to use Frontier or Morden specification and tweak it for your needs. Parity repo contains examples and actual frontier/morden specifications [here](https://github.com/ethcore/parity/tree/master/ethcore/res/ethereum). You can also set up a [Proof of Authority Chain](https://github.com/ethcore/parity/wiki/Proof-of-Authority-Chains).

### Notes

The chain specification format is a work in progress and was changed a number of times between Parity releases. Currently the `beta` branch of the repository contains spec files that are compatible with Parity 1.1 and `master` branch is compatible with Parity 1.2. E.g. this [morden.json] (https://github.com/ethcore/parity/blob/beta/ethcore/res/ethereum/morden.json) file can be used as reference for parity 1.1
and this [morden.json] (https://github.com/ethcore/parity/blob/master/ethcore/res/ethereum/morden.json) is compatible with the latest version.

### Example spec file for Parity 1.2

Here is an example file for private network. This a basic Morden config with a few parameters changed:

`frontierCompatibilityModeLimit` is set to 0 to enable frontier mode from the start.
`durationLimit` is set to 10 seconds.
`networkID` is changed to avoid clashing with the main network.
`nodes` contains a custom bootstrap node.
`accounts` contains a custom account with lots of Ether.

```json
{
	"name": "Morden",
	"engine": {
		"Ethash": {
			"params": {
				"gasLimitBoundDivisor": "0x0400",
				"minimumDifficulty": "0x020000",
				"difficultyBoundDivisor": "0x0800",
				"durationLimit": "0x0a",
				"blockReward": "0x4563918244F40000",
				"registrar": "",
				"frontierCompatibilityModeLimit": "0x0"
			}
		}
	},
	"params": {
		"accountStartNonce": "0x0100000",
		"maximumExtraDataSize": "0x20",
		"minGasLimit": "0x1388",
		"networkID" : "0x42"
	},
	"genesis": {
		"seal": {
			"ethereum": {
				"nonce": "0x00006d6f7264656e",
				"mixHash": "0x00000000000000000000000000000000000000647572616c65787365646c6578"
			}
		},
		"difficulty": "0x20000",
		"author": "0x0000000000000000000000000000000000000000",
		"timestamp": "0x00",
		"parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
		"extraData": "0x",
		"gasLimit": "0x2fefd8"
	},
	"nodes": [
		"enode:////c2328c3e7857106585dbb59b712ac2ab9443d4f0b55b77451fbf33c0dda58b882f0683c4c9222cbf8d1d6893e7f926d487630810202a2c75ec6dd996dbe84715@192.168.0.12:30303"
	],
	"accounts": {
		"0000000000000000000000000000000000000001": { "balance": "1", "nonce": "1048576", "builtin": { "name": "ecrecover", "pricing": { "linear": { "base": 3000, "word": 0 } } } },
		"0000000000000000000000000000000000000002": { "balance": "1", "nonce": "1048576", "builtin": { "name": "sha256", "pricing": { "linear": { "base": 60, "word": 12 } } } },
		"0000000000000000000000000000000000000003": { "balance": "1", "nonce": "1048576", "builtin": { "name": "ripemd160", "pricing": { "linear": { "base": 600, "word": 120 } } } },
		"0000000000000000000000000000000000000004": { "balance": "1", "nonce": "1048576", "builtin": { "name": "identity", "pricing": { "linear": { "base": 15, "word": 3 } } } },
		"16a9dfd266e3229f05a2704c13bf2e16ea23e7c3": { "balance": "1606938044258990275541962092341162602522202993782792835301376", "nonce": "1048576" }
	}
}
```

