<template>
  <div>
    <div class="bg-white px-4 py-5 border-b border-gray-200 sm:px-6">
      <div
        class="-ml-4 -mt-2 flex items-center justify-between flex-wrap sm:flex-nowrap"
      >
        <div class="ml-4 mt-2">
          <h3 class="text-lg leading-6 font-medium text-gray-900">
            Engelske produkter
          </h3>
        </div>
        <div class="ml-4 mt-2 flex-shrink-0">
          <div>
            <label for="search" class="sr-only">Søg</label>
            <input
              id="search"
              v-model="search"
              type="text"
              name="search"
              class="shadow-sm focus:ring-indigo-500 focus:border-indigo-500 block w-full sm:text-sm border-gray-300 rounded-md"
            />
          </div>
        </div>
      </div>
    </div>

    <ul>
      <li
        v-for="product of products"
        :key="product.slug"
        class="hover:bg-gray-50"
      >
        <NuxtLink
          v-if="product.sku.toLowerCase().includes(search)"
          :to="product.slug"
          class="flex items-center px-4 py-4 sm:px-6"
        >
          <div>
            <h2 class="text-sm font-medium text-indigo-600 truncate">
              {{ product.name }}
            </h2>
            <p class="flex items-center text-sm text-gray-500">
              Varenr. {{ product.sku }}
            </p>
          </div>
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const products = await $content('products', params.slug)
      .only(['name', 'sku', 'slug'])
      .sortBy('slug', 'asc')
      .fetch()

    return {
      products,
    }
  },
  data() {
    return {
      search: '',
    }
  },
}
</script>
