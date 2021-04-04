<template>
  <v-list
    two-line
  >
    <v-list-item-group>
      <template
        v-for="(statement, index) in statements"
      >
        <v-list-item
          v-if="statement.subject"
          :key="statement.id"
          :ripple="false"
          :to="`/resources/${statement.subject.id}`"
          @click="onClick(statement.subject.id)"
        >
          <v-list-item-content
            class="text-left"
          >
            <span
              v-text="`${statement.subject.name} ${statement.predicate.name}...`"
            />
          </v-list-item-content>
        </v-list-item>
        <v-list-item
          v-if="statement.object"
          :key="statement.id"
          :ripple="false"
          :to="`/resources/${statement.object.id}`"
          @click="onClick(statement.object.id)"
        >
          <v-list-item-content
            class="text-left"
          >
            <span
              v-text="`...${statement.predicate.name} ${statement.object.name}`"
            />
          </v-list-item-content>
        </v-list-item>
        <v-divider
          v-if="index < statements.length - 1"
          :key="`divider-${index}`"
        />
      </template>
    </v-list-item-group>
  </v-list>
</template>

<script>
export default {
  name: 'StatementList',
  props: {
    statements: {
      type: Array,
      required: true,
    },
    onClick: {
      type: Function,
      required: true,
    },
  },
};
</script>
