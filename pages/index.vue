<script setup lang="ts">
import { components } from "~/slices";

const prismic = usePrismic();
const { data: page } = useAsyncData("index", () =>
  prismic.client.getSingle("home", {
    fetchLinks: [
      "testimonial.quote",
      "testimonial.avatar",
      "testimonial.name",
      "testimonial.title",
    ],
  })
);

useSeoMeta({
  title: page.value?.data.meta_title ?? undefined,
  description: page.value?.data.meta_description ?? undefined,
});
</script>

<template>
  <SliceZone
    wrapper="main"
    :slices="page?.data.slices ?? []"
    :components="components"
  />
</template>
