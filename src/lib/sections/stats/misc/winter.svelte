<script lang="ts">
  import { getMiscContext } from "$ctx";
  import { SectionSubtitle } from "$lib/components/sections";
  import { AdditionStat } from "$lib/components/stats";
  import GiftIcon from "@lucide/svelte/icons/gift";
  import SnowflakeIcon from "@lucide/svelte/icons/snowflake";
  import { format } from "numerable";

  const misc = $derived(getMiscContext().misc);
  const gifts = $derived(misc?.gifts);
  const season_of_jerry = $derived(misc?.season_of_jerry);
</script>

{#if misc && (gifts || season_of_jerry) != null}
  <div class="border p-4 rounded-xl space-y-4">
    <SectionSubtitle>Winter</SectionSubtitle>
    <div class="grid grid-cols-1 gap-4 sm:grid-cols-2">
      {#if gifts}
        <div class="flex flex-col gap-1 rounded-xl bg-background/50 p-4 border">
          <SectionSubtitle>
            <div class="flex items-center gap-2">
              <GiftIcon class="size-5 text-accent-2" />
              Gifts
            </div>
          </SectionSubtitle>
          <div class="space-y-0.5">
            {#each Object.entries(gifts) as [text, data], index (index)}
              <AdditionStat text={text.replaceAll("_", " ")} data={format(data)} />
            {/each}
          </div>
        </div>
      {/if}
      {#if season_of_jerry}
        <div class="flex flex-col gap-1 rounded-xl bg-background/50 p-4 border">
          <SectionSubtitle>
            <div class="flex items-center gap-2">
              <SnowflakeIcon class="size-5 text-minecraft-b" />
              Season of Jerry
            </div>
          </SectionSubtitle>
          <div class="space-y-0.5">
            {#each Object.entries(season_of_jerry) as [text, data], index (index)}
              <AdditionStat text={text.replaceAll("_", " ")} data={format(data)} />
            {/each}
          </div>
        </div>
      {/if}
    </div>
  </div>
{/if}
