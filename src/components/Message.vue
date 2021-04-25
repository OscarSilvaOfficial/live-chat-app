<template>
  <v-card class="mx-auto" color="#26c6da" dark max-width="400" id="message-box">
    <v-card-text class="headline font-weight-bold">
      "{{ message }}"
    </v-card-text>

    <v-card-actions>
      <v-list-item class="grow">
        <v-list-item-avatar color="grey darken-3">
          <v-img
            class="elevation-6"
            alt=""
            src="https://avataaars.io/?avatarStyle=Transparent&topType=ShortHairShortCurly&accessoriesType=Prescription02&hairColor=Black&facialHairType=Blank&clotheType=Hoodie&clotheColor=White&eyeType=Default&eyebrowType=DefaultNatural&mouthType=Default&skinColor=Light"
          ></v-img>
        </v-list-item-avatar>

        <v-list-item-content>
          <v-list-item-title>{{ name }}</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
    </v-card-actions>
  </v-card>
</template>
<script>
export default {
  props: ["name", "message"],
};
</script>
<style lang="scss" scope>
#message-box {
  margin-bottom: 1rem;
  width: 800px;
  max-width: 800px !important;
}
</style>
