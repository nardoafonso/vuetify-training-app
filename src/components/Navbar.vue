<template>
   <nav>
       <v-snackbar v-model="snackbar" :timeout="4000" top color="success"> 
           <span>New Project Added</span>
           <v-btn text color="white" @click="snackbar=false">Close</v-btn>
       </v-snackbar>
        <v-app-bar flat>
            <v-app-bar-nav-icon class="grey--text" @click="drawer=!drawer"></v-app-bar-nav-icon>
            <v-toolbar-title class="text-uppercase grey--text">
                <span class="font-weight-light">Todo</span>
                <span class="">Ninja</span>
            </v-toolbar-title>
            <v-spacer></v-spacer>

            <!-- drop-down menu -->
            <v-menu offset-y>
                <template v-slot:activator="{ on }">
                    <v-btn text color="grey" v-on="on"> 
                        <v-icon left>mdi-chevron-down</v-icon>
                        <span>Menu</span>
                    </v-btn>
                </template>
                <v-list>
                    <v-list-item v-for="(link, index) in links" :key="index" @click="menu=!menu"  route :to="link.route" >
                        <v-list-item-title >{{ link.text }}</v-list-item-title>
                    </v-list-item>
                </v-list>
            </v-menu>

            <v-btn text color="grey">
                <span>Sign Out</span>
                <v-icon>mdi-exit-to-app</v-icon>
            </v-btn>
        </v-app-bar>

        <v-navigation-drawer app v-model="drawer" class="primary">
            <v-row>
                <v-col align="center" class="mt-5">
                    <v-avatar size="100">
                        <img :src="'/avatar-1.png'" alt=""/>
                    </v-avatar>
                    <p class="white--text sibtitle-1 mt-1"> The Net Ninja</p>
                    <Popup @closedPopUpEvent="snackbar = true" />
                </v-col>
            </v-row>
            <v-list>
                <v-list-item v-for="link in links" :key="link.text" router :to="link.route">
                    <v-list-item-action>
                        <v-icon class="white--text">mdi-{{link.icon}}</v-icon>
                    </v-list-item-action>
                    <v-list-item-content>
                        <v-list-item-title class="white--text">{{link.text}}</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>
   </nav>
</template>
<script>
import Popup from '@/components/Popup.vue';
export default {
    data(){
        return {
            drawer:false,
            menu:false,
            snackbar:false,
            links: [
                { icon: 'view-dashboard', text: 'Dashboard', route: '/' },
                { icon: 'folder', text: 'My Projects', route: '/projects' },
                { icon: 'account', text: 'Team', route: '/team' },
            ]
        }
    },
    components:{
        Popup:Popup
    }
}
</script>

