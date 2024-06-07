---
order: 900
---

# ERC-2981 Royalties

For v3.2+ contracts (all Studio contracts, Engine contracts deployed after May 2024), Art Blocks contracts conform to the ERC-2981 standard for royalties.

> Note: All versions of Art Blocks core contracts integrate seamlessly with the Royalty Registry, which is supported by all major secondary marketplaces.

The ERC-2981 standard requires that royalty payments be made to a single address. Art Blocks contracts support this standard by integrating with 0xSplits to facilitate multi-party royalty payments to multiple addresses, all funneled through a single, permissionless, immutable "splitter contract" address.

Artists may view their current royalty splitter address in the Art Blocks Creator Dashboard. The royalty splitter address is deployed and set automatically by the v3.2+ Art Blocks core contract when payment information is configured. A link to the current splitter is available in the dashboard, and distribution of funds in the splitter may be viewed and executed via the 0xSplits website. Note that 0xSplits provides a user-friendly interface for viewing splitter balances and executing distributions, as well as robust report generation tooling.

> Note: 0xSplits is a third-party service and is not affiliated with Art Blocks.
