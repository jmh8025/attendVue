<template>
  <v-app >
         <nav>
            <v-toolbar dark color="primary">
                <v-toolbar-title>
                  <div>면접평가시스템</div>
                </v-toolbar-title>
                <v-spacer></v-spacer>
                <v-toolbar-items>
                    <v-btn text nuxt to="/signup" :style="{display:'flex', alignItems:'center'}">
                       <v-icon>mdi-help</v-icon>
                    </v-btn>
                </v-toolbar-items>
            </v-toolbar>
        </nav> 
        <nuxt/>
    </v-app>
</template>

<script>
export default {

  data () {
    return {
    }
  }
}
</script>
