<script lang="ts">
  import { getMiscContext } from "$ctx";
  import { SectionSubtitle } from "$lib/components/sections";
  import { AdditionStat } from "$lib/components/stats";
  import { RARITY_COLORS } from "$lib/shared/constants/rarities";
  import { Label } from "$ui/label";
  import GavelIcon from "@lucide/svelte/icons/gavel";
  import ShoppingCartIcon from "@lucide/svelte/icons/shopping-cart";
  import { format } from "numerable";

  const misc = $derived(getMiscContext().misc);
  const auctions = $derived(misc?.auctions);
</script>

{#if misc && auctions != null}
  <div class="border p-4 rounded-xl space-y-4">
    <SectionSubtitle>Auctions</SectionSubtitle>
    <div class="grid grid-cols-1 gap-4 sm:grid-cols-2">
      <div class="flex flex-col gap-1 rounded-xl bg-background/50 p-4 border space-y-0.5">
        <SectionSubtitle>
          <div class="flex items-center gap-2">
            <GavelIcon class="size-5 text-accent-2" />
            Sold
          </div>
        </SectionSubtitle>
        <AdditionStat text="Fees" data={format(auctions.fees)} />
        <AdditionStat text="Coins Earned" data={format(auctions.gold_earned)} />
        {#if auctions.total_sold && auctions.total_sold.total !== 0}
          <AdditionStat text="Items Sold" data={format(auctions.total_sold.total)} asterisk={true}>
            <div class="space-y-1">
              {#each Object.entries(auctions.total_sold) as [rarity, amount], index (index)}
                {#if rarity !== "total"}
                  <Label class="gap-1 capitalize">
                    <span style="color: var(--§{RARITY_COLORS[rarity.toLowerCase()]})">{rarity.replaceAll("_", " ").toLowerCase()}:</span>
                    <span class="font-bold">{format(amount)}</span>
                  </Label>
                {/if}
              {/each}
            </div>
          </AdditionStat>
        {/if}
      </div>
      <div class="flex flex-col gap-1 rounded-xl bg-background/50 p-4 border space-y-0.5">
        <SectionSubtitle>
          <div class="flex items-center gap-2">
            <ShoppingCartIcon class="size-5 text-minecraft-9" />
            Bought
          </div>
        </SectionSubtitle>
        <AdditionStat text="Bids" data={format(auctions.bids)} />
        <AdditionStat text="Highest Bid" data={format(auctions.highest_bid)} />
        <AdditionStat text="Won" data={format(auctions.won)} />
        <AdditionStat text="Coins Spent" data={format(auctions.gold_spent)} />
        {#if auctions.total_bought && auctions.total_bought.total !== 0}
          <AdditionStat text="Items Bought" data={format(auctions.total_bought.total)} asterisk={true}>
            <div class="space-y-1">
              {#each Object.entries(auctions.total_bought) as [rarity, amount], index (index)}
                {#if rarity !== "total"}
                  <Label class="gap-1 capitalize">
                    <span style="color: var(--§{RARITY_COLORS[rarity.toLowerCase()]})">{rarity.replaceAll("_", " ").toLowerCase()}:</span>
                    <span class="font-bold">{format(amount)}</span>
                  </Label>
                {/if}
              {/each}
            </div>
          </AdditionStat>
        {/if}
      </div>
    </div>
  </div>
{/if}
