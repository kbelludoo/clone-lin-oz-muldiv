# clone-lin-oz-muldiv

Experimental i64-scale LIN clone of [OpenZeppelin/openzeppelin-contracts](https://github.com/OpenZeppelin/openzeppelin-contracts) tag `v5.0.2` `Math.mulDiv` + `Rounding` (`contracts/utils/math/Math.sol`, MIT).

- **LIN clone:** [`src/lin_openzeppelin_muldiv.lin`](src/lin_openzeppelin_muldiv.lin)
- **Proofs (results only) live in lin-open:** https://github.com/kbelludoo/lin-open/tree/master/examples/openzeppelin_muldiv
- **Event receipt:** `docs/events/EVENT_OPENZEPPELIN_MULDIV_CLONE_LIN.rulel` in lin-open

This repository is the standalone LIN copy. It is **not** a vault, **not** OpenZeppelin Contracts, and does **not** claim Solidity uint256 / 512-bit CRT parity.

Canonical goldens (uint64-scale, 128-bit product):

- `mulDiv(100,200,50,Floor)` = **400**
- `mulDiv(7,9,2,Floor)` = **31** remainder **1**
- `mulDiv(7,9,2,Ceil)` = **32**
- `mulDiv(7,9,2,Trunc)` = **31** (unsigned Floor==Trunc)
- `mulDiv(7,9,2,Expand)` = **32** (unsigned Ceil==Expand)
- `mulDiv(1,1,2,Floor)` = **0**; Ceil = **1**
- `1e18 * 1e18 / 1` fail-closes to **0** (quotient does not fit uint64)
- named contrast: `ceilDiv(7,3)=3` != `mulDiv(7,2,3,Ceil)=5`
- ERC-4626-style: `convertToShares(100,50,200)=25` Floor; `previewMint(1,3,100)=34` Ceil
- flags outside `{0,1,2,3}` or negative inputs fail-close to **0**
