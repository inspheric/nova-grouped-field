<template>
    <div>
        <div class="flex border-b border-40">
            <div class="w-1/4 py-4">
                <h4 class="font-normal text-80">
                    <p>{{ field.name }}</p>
                </h4>
            </div>
            <div class="w-3/4 py-4">
               <p class="text-90">
                <span :key="index" v-for="(childField, index) in field.fields">
                    <router-link
                        v-if="childField.value && childField.belongsToId && ! field.removeLinks"
                        :to="{name: 'detail', params: {
                            resourceName: childField.resourceName,
                            resourceId: childField.belongsToId
                        }}"
                        class="no-underline font-bold dim text-primary"
                    >
                        <span v-if="field.showLabels">{{ childField.name }}: </span>
                        {{ childField.value }}
                    </router-link>
                    <span v-else>
                        <span v-if="field.showLabels">{{ childField.name }}: </span>
                        {{ childField.value }}
                    </span>
                    <span v-if="showSeparator(index)"> //FIXME
                        {{ field.separator }}
                    </span>
                </span>
            </p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  props: ['resource', 'resourceName', 'resourceId', 'field'],

  methods: {
      showSeparator(index) {
          return index < this.field.fields.length - 1 && this.field.fields[index + 1].value //FIXME
      }
  }
};
</script>
