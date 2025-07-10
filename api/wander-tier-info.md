---
description: Wander Injected API getWanderTierInfo() function
---

# Wander Tier

Some applications may request access to the Wander tier information of the user. The `getWanderTierInfo()` function returns the [result](wander-tier-info.md#result) from the API call.

{% hint style="info" %}
**Note:** This function requires the [`ACCESS_ADDRESS`](connect.md#permissions) permission.
{% endhint %}

## Result

The `getWanderTierInfo()` function returns an object with the user's tier information. The `tier` property is a string representing the user's tier. The `balance` property is a string representing the user's balance. The `rank` property is a number representing the user's rank in the balance leaderboard. The `progress` property is a number representing the user's progress in the tier system. The `snapshotTimestamp` property is a number representing the timestamp of the snapshot. The `totalHolders` property is a number representing the total number of WNDR holders in the snapshot.

```typescript
type Tier = "Prime" | "Edge" | "Reserve" | "Select" | "Core";

type WanderTierInfo = {
  tier: Tier;
  balance: string;
  rank: number;
  progress: number;
  snapshotTimestamp: number;
  totalHolders: number;
}
```

## Example usage

```ts
// Connect to the extension and request access to the ACCESS_ADDRESS permission
await window.arweaveWallet.connect(["ACCESS_ADDRESS"]);

// Retrieve the tier of the user
const info = await window.arweaveWallet.getWanderTierInfo();
console.log("Tier of the user: ", info.tier);
console.log("Balance: ", info.balance);
console.log("Rank: ", info.rank);
console.log("Progress: ", info.progress);
console.log("Snapshot timestamp: ", info.snapshotTimestamp);
console.log("Total holders: ", info.totalHolders);
```

## Dryrun from the process

The following is an example of how to get the tier information of a user using the dryrun function from the process. Please make sure to cache the tier information in your application to avoid unnecessary calls to the process as the information is updated every 24 hours at 4:00 PM GMT. The `getWanderTierInfo` function returns `snapshotTimestamp` which is the timestamp of the snapshot. You can use this to check if the tier information is up to date and cache for the next 24 hours.

```ts
import { dryrun } from "@permaweb/aoconnect";

const tierIdToTierName = {
  1: "Prime",
  2: "Edge",
  3: "Reserve",
  4: "Select",
  5: "Core",
};

async function getWanderTierInfo(walletAddress: string): Promise<WanderTierInfo> {
  const dryrunRes = await dryrun(
    Owner: walletAddress,
    process: "rkAezEIgacJZ_dVuZHOKJR8WKpSDqLGfgPJrs_Es7CA",
    tags: [{ name: "Action", value: "Get-Wallet-Info" }]
  );

  const message = dryrunRes.Messages?.[0];
  const data = JSON.parse(message?.Data || "{}");

  if (data?.tier === undefined || data?.tier === null) {
    throw new Error("No tier data found");
  }

  const tierInfo = {
    ...data,
    tier: tierIdToTierName[data.tier],
  } satisfies WanderTierInfo;

  return tierInfo;
}


const walletAddress = "...";
const tierInfo = await getWanderTierInfo(walletAddress);
console.log(tierInfo);
```
