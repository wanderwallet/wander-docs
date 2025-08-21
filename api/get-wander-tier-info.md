---
description: Wander Injected API getWanderTierInfo() function
---

# Get Wander tier info

Some applications may request access to the Wander tier information of the user. The `getWanderTierInfo()` function returns detailed information about the user's tier, balance, rank, and other related metrics in the Wander ecosystem.

{% hint style="info" %}
**Note:** This function requires the [`ACCESS_ADDRESS`](connect.md#permissions) permission.
{% endhint %}

## Result

The `getWanderTierInfo()` function returns an object containing comprehensive tier information for the user.

{% hint style="warning" %}
**Note**: This function throws an error if there is an issue retrieving the tier information. Please make sure to handle such cases in your code.
{% endhint %}

```typescript
type Tier = "Prime" | "Edge" | "Reserve" | "Select" | "Core";

interface WanderTierInfo {
  tier: Tier;                    // User's current tier
  balance: string;               // User's WNDR token balance from the snapshot
  rank: "" | number;             // User's rank in the balance leaderboard (empty string if not ranked)
  progress: number;              // User's progress within the tier system (0-100)
  snapshotTimestamp: number;     // Timestamp of the last snapshot update (in milliseconds)
  totalHolders: number;          // Total number of WNDR token holders in the snapshot
}
```

## Example usage

```ts
// Connect to the extension and request access to the ACCESS_ADDRESS permission
await window.arweaveWallet.connect(["ACCESS_ADDRESS"]);

try {
  // Retrieve the tier information of the user
  const tierInfo = await window.arweaveWallet.getWanderTierInfo();
  
  console.log("Tier:", tierInfo.tier);
  console.log("Balance:", tierInfo.balance);
  console.log("Rank:", tierInfo.rank);
  console.log("Progress:", tierInfo.progress);
  console.log("Snapshot timestamp:", tierInfo.snapshotTimestamp);
  console.log("Total holders:", tierInfo.totalHolders);
} catch (error) {
  console.error("Error fetching tier information:", error);
}
```

## Alternative implementation via dryrun

For applications that need to query tier information for any wallet address (not just the connected user), you can also use the dryrun approach to query the Wander leaderboard process directly.

{% hint style="info" %}
**Note:** The tier information is updated every 24 hours at 4:00 PM GMT. Make sure to cache the results using the `snapshotTimestamp` to avoid unnecessary calls to the process.
{% endhint %}

### Single wallet query

```ts
import { dryrun } from "@permaweb/aoconnect";

type Tier = "Prime" | "Edge" | "Reserve" | "Select" | "Core";

interface WanderTierInfo {
  tier: Tier;                    
  balance: string;               
  rank: "" | number;             
  progress: number;              
  snapshotTimestamp: number;     
  totalHolders: number;          
}

type WanderTierInfoFromApi = Omit<WanderTierInfo, "tier"> & {
  tier: number;
}

const TIER_ID_TO_NAME = {
  1: "Prime",
  2: "Edge", 
  3: "Reserve",
  4: "Select",
  5: "Core",
} as const;

function isValidTierInfo(data: WanderTierInfoFromApi): data is WanderTierInfoFromApi {
  return (
    data &&
    typeof data === "object" &&
    typeof data.tier === "number" &&
    typeof data.balance === "string" &&
    typeof data.rank === "number" &&
    typeof data.progress === "number" &&
    typeof data.snapshotTimestamp === "number" &&
    typeof data.totalHolders === "number"
  );
}

// Single wallet query
async function getWanderTierInfo(walletAddress: string): Promise<WanderTierInfo> {
  let data: WanderTierInfoFromApi;
  try {
    const response = await fetch(`https://cache.wander.app/api/tier-info?address=${walletAddress}`);
    if (!response.ok) {
      throw new Error("Failed to fetch tier info from cache API");
    }

    const responseData = await response.json();

    if (!isValidTierInfo(responseData)) {
      throw new Error("Invalid tier info data format from cache API");
    }

    data = responseData;
  } catch {
    const dryrunRes = await dryrun({
      Owner: walletAddress,
      process: "rkAezEIgacJZ_dVuZHOKJR8WKpSDqLGfgPJrs_Es7CA",
      tags: [{ name: "Action", value: "Get-Wallet-Info" }]
    });

    const message = dryrunRes.Messages?.[0];
    const parsedData = JSON.parse(message?.Data || "{}");

    if (!isValidTierInfo(parsedData)) {
      throw new Error("Invalid tier info data from WNDR tier process");
    }

    data = parsedData;
  }

  const tierInfo: WanderTierInfo = {
    ...data,
    tier: TIER_ID_TO_NAME[data.tier as keyof typeof TIER_ID_TO_NAME],
  };

  return tierInfo;
}

const walletAddress = "your-wallet-address-here";
try {
  const tierInfo = await getWanderTierInfo(walletAddress);
  console.log("Tier information:", tierInfo);
} catch (error) {
  console.error("Failed to retrieve tier information:", error);
}
```

### Batch wallet query

```ts
import { dryrun } from "@permaweb/aoconnect";

type Tier = "Prime" | "Edge" | "Reserve" | "Select" | "Core";

interface WanderTierInfo {
  tier: Tier;                    
  balance: string;               
  rank: "" | number;             
  progress: number;              
  snapshotTimestamp: number;     
  totalHolders: number;          
}

type WanderTierInfoFromApi = Omit<WanderTierInfo, "tier"> & {
  tier: number;
}

const TIER_ID_TO_NAME = {
  1: "Prime",
  2: "Edge", 
  3: "Reserve",
  4: "Select",
  5: "Core",
} as const;

// Batch wallet query
async function getBatchWanderTierInfo(walletAddresses: string[]): Promise<Record<string, WanderTierInfo>> {
  let data: Record<string, WanderTierInfoFromApi>;

  try {
    const response = await fetch(`https://cache.wander.app/api/tier-info?addresses=${walletAddresses.join(",")}`);
    if (!response.ok) {
      throw new Error("Failed to fetch tier info from cache API");
    }

    data = await response.json();
  } catch {
    const dryrunRes = await dryrun({
      process: "rkAezEIgacJZ_dVuZHOKJR8WKpSDqLGfgPJrs_Es7CA",
      data: JSON.stringify(walletAddresses),
      tags: [{ name: "Action", value: "Get-Wallets-Info" }],
    });

    if (dryrunRes.Error) throw new Error(dryrunRes.Error);

    const message = dryrunRes.Messages?.[0];
    data = JSON.parse(message?.Data || "{}");
  }

  const batchTierInfo: Record<string, WanderTierInfo> = {};

  for (const [walletAddress, walletData] of Object.entries<any>(data)) {
    batchTierInfo[walletAddress] = {
      ...walletData,
      tier: TIER_ID_TO_NAME[walletData.tier as keyof typeof TIER_ID_TO_NAME],
    };
  }

  return batchTierInfo;
}

const walletAddresses = [
  "wallet-address-1",
  "wallet-address-2", 
  "wallet-address-3"
];

try {
  const batchTierInfo = await getBatchWanderTierInfo(walletAddresses);
  
  for (const [address, tierInfo] of Object.entries(batchTierInfo)) {
    console.log(`Tier info for ${address}: `, tierInfo);
  }
} catch (error) {
  console.error("Failed to retrieve batch tier information:", error);
}
```
