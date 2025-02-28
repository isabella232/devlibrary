<!--
 Copyright 2021 Google LLC

 Licensed under the Apache License, Version 2.0 (the "License");
 you may not use this file except in compliance with the License.
 You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

 Unless required by applicable law or agreed to in writing, software
 distributed under the License is distributed on an "AS IS" BASIS,
 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 See the License for the specific language governing permissions and
 limitations under the License.
-->

<template>
  <div
    class="flex flex-row rounded overflow-hidden border border-gray-50 shadow transition-shadow hover:shadow-lg"
  >
    <!-- GitHub Sidebar -->
    <div class="px-1 flex flex-col justify-center text-white bg-gray-900">
      <font-awesome-icon :icon="['fab', 'github']" size="lg" fixed-width />
    </div>

    <div class="pt-1 flex-grow flex flex-col">
      <!-- Top Section -->
      <div class="flex-grow card-top-grid pl-3 pr-2 mb-4">
        <!-- Title and Description -->
        <router-link :to="link" class="text-base">
          <div class="font-medium">{{ repo.metadata.repo }}</div>
          <div class="wrap-lines-1">
            {{ repo.metadata.shortDescription }}
          </div>
        </router-link>

        <!-- Stats -->
        <div class="whitespace-nowrap">
          <span class="text-sm">{{ repo.stats.stars }}</span>
          <font-awesome-icon icon="star" size="sm" class="ml-1" />
        </div>
      </div>

      <!-- Timestamp and Buttons -->
      <div class="flex flex-row pl-3 items-baseline">
        <span class="flex-grow text-sm text-gray-500 wrap-lines-1"
          >updated {{ renderDaysAgo(repo.stats.lastUpdated) }}</span
        >
        <router-link :to="link"
          ><MaterialButton type="text">Learn More</MaterialButton></router-link
        >
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";

import { RepoData } from "../../../shared/types";
import MaterialButton from "@/components/MaterialButton.vue";

import * as dates from "@/plugins/dates";

@Component({
  components: {
    MaterialButton,
  },
})
export default class SmallRepoCard extends Vue {
  @Prop() repo!: RepoData;

  public renderDaysAgo(lastUpdated: number) {
    return dates.renderDaysAgo(lastUpdated);
  }

  get link() {
    return `/products/${this.repo.product}/repos/${this.repo.id}`;
  }
}
</script>

<style scoped lang="postcss">
.card-top-grid {
  @apply gap-2;
  display: grid;
  grid-template-columns: 1fr min-content;
}
</style>
