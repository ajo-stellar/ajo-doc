# Architecture

<div class="project-brand">
  <img class="brand-light" src="brand/logo.svg" alt="Ajo" width="360">
  <img class="brand-dark" src="brand/logo-dark.svg" alt="Ajo" width="360">
</div>


The browser calls Soroban directly; wallets provide public addresses and signed transactions. There is no backend. Network configuration comes from environment values and refuses other networks (`ajo-app/src/lib/network.ts`).

Five public methods are declared in `ajo-contracts/src/lib.rs`. `circles.rs` implements bounded circles of 2–20 unique members, fixed payout order, authorized contributions and permissionless settlement only after everyone pays. `types.rs` defines stored types, errors and events; `storage.rs` owns keys and TTL renewal.

Per-circle accounting is `balance = received_total - paid_total`. `three_members_three_rounds_full_accounting` checks after every contribution and payout. `sequential_ids_do_not_mix_circle_balances` verifies isolation. Token failures roll back all state changes. The shared contract token balance represents all outstanding pots plus any unsolicited transfers; individual circles only pay their own tracked pot.

Round length guides storage retention, not payment deadlines. Persistent entries renew on access, but inactive state may archive. The app cannot restore archived entries.

The browser reads through RPC simulation. Simulated reads do not commit TTL extensions on-chain; successful submitted contract transactions do. A displayed circle is not evidence that its archival retention has been renewed.
