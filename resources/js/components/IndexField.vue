<template>
    <div>
        <span :key="index" v-for="(childField, index) in field.fields">
            <router-link
                v-if="childField.value && childField.belongsToId"
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
            <span v-if="showSeparator(index)">
                {{ field.separator }}
            </span>
        </span>
    </div>
</template>

<script>
export default {
  props: ['resource', 'resourceName', 'resourceId', 'field'],

  methods: {
      showSeparator(index) {
          return index < this.field.fields.length - 1 && this.field.fields[index + 1].value
      }
  }
};
</script>
