<script lang="ts">
  import { getMiscContext } from "$ctx";
  import { SectionSubtitle } from "$lib/components/sections";
  import { AdditionStat } from "$lib/components/stats";
  import EggIcon from "@lucide/svelte/icons/egg";
  import MountainIcon from "@lucide/svelte/icons/mountain";
  import { format } from "numerable";

  const misc = $derived(getMiscContext().misc);
  const dragons = $derived(misc?.dragons);
  const endstone_protector = $derived(misc?.endstone_protector);
</script>

{#if misc && (dragons || endstone_protector) != null}
  <div class="border p-4 rounded-xl space-y-4">
    <SectionSubtitle>End</SectionSubtitle>
    <div class="grid grid-cols-1 gap-4 sm:grid-cols-2">
      {#if dragons}
        <div class="flex flex-col gap-1 rounded-xl bg-background/50 p-4 border">
          <SectionSubtitle>
            <div class="flex items-center gap-2">
              <EggIcon class="size-5 text-minecraft-5" />
              Dragons
            </div>
          </SectionSubtitle>
          <div class="space-y-0.5">
            {#each Object.entries(dragons) as [text, data], index (index)}
              <AdditionStat text={text.replaceAll("_", " ")} data={format(data)} />
            {/each}
          </div>
        </div>
      {/if}
      {#if endstone_protector}
        <div class="flex flex-col gap-1 rounded-xl bg-background/50 p-4 border">
          <SectionSubtitle>
            <div class="flex items-center gap-2">
              <MountainIcon class="size-5 text-accent-5" />
              Endstone Protector
            </div>
          </SectionSubtitle>
          <div class="space-y-0.5">
            {#each Object.entries(endstone_protector) as [text, data], index (index)}
              <AdditionStat text={text.replaceAll("_", " ")} data={format(data)} />
            {/each}
          </div>
        </div>
      {/if}
    </div>
  </div>
{/if}
