<template>
    <nav 
        :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar','navbar-expand-lg']"
    >
        <a class="navbar-brand" href="#">Navbar</a>
        <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">

                <navbar-link
                    v-for="(page, index) in publishedPages" class="nav-item" :key="index"
                    :page="page"
                    :index="index"
                ></navbar-link>

                <li>
                    <router-link 
                        to="/pages/create"
                        class="nav-link"
                        active-class="active"
                        aria-current="page"
                        >Create Page
                    </router-link >
                </li>


            </ul>
            <form class="d-flex">
                <button
                    class="btn btn-primary"
                    @click.prevent="changeTheme()"
                >
                    Change Theme 
                </button>
            </form>
        </div>
    </nav>
</template>

<script>
import NavbarLink from './NavbarLink.vue';
export default {
    components: {
        NavbarLink
    },
    created(){
        this.getThemeSetting();
        this.pages = this.$pages.getAllPages();
    },
    computed: {
        publishedPages(){
            return this.pages.filter(p => p.published);
        }
    },

    data(){
        return{
            theme: 'dark',
            pages: []
        }
    },
    methods: {
        changeTheme() {
            let theme = 'light';
            if (this.theme == 'light') {
                theme = 'dark';
            }
            this.theme = theme;
            this.storeThemeSetting();
        },
        storeThemeSetting() {
            localStorage.setItem('theme', this.theme);
        },
        getThemeSetting() {
            let theme = localStorage.getItem('theme')
            if (theme) {
                this.theme = theme;
            }
        }
    }
            }
</script>