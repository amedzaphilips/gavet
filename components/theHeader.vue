<template>
  <div>
    <nav class="navbar navbar-expand-lg lg bg-indigo-darken-1">
      <div class="container-fluid">
        <NuxtLink class="navbar-brand" to="/">
          <img :src="logo" height="80px" width="auto" alt="" />
        </NuxtLink>
        <button class="navbar-toggler" type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasNavbar"
          aria-controls="offcanvasNavbar" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon" is-nav></span>
        </button>
        <div class="offcanvas offcanvas-end bg-indigo-lighten-4" id="offcanvasNavbar" tabindex="-1">
          <div class="offcanvas-header">
            <button type="button" class="btn-close" data-bs-dismiss="offcanvas" aria-label="Close"></button>
          </div>
          <div class="offcanvas-body" id="navbarScroll">
            <ul class="navbar-nav text-white justify-content-start flex-grow-1 pe-3">
              <li class="nav-item">
                <NuxtLink class="nav-link text-white" aria-current="page" to="/">Home</NuxtLink>
              </li>
              <li class="nav-item">
                <NuxtLink class="nav-link text-white" to="/about">
                  About
                </NuxtLink>
              </li>
              <li class="nav-item">
                <NuxtLink v-if="user == null" class="nav-link text-white" to="/login">
                  Accounts Details
                </NuxtLink>
                <NuxtLink v-else class="nav-link text-white" to="/transac">
                  Accounts Details
                </NuxtLink>
              </li>

              

              <li class="nav-item">
                <NuxtLink v-if="user == null" class="nav-link text-white" to="/login">
                  TollBooth
                </NuxtLink>
                <NuxtLink v-else class="nav-link text-white" to="/deductions">
                  TollBooth
                </NuxtLink>
              </li>
              <li class="nav-item">
                <NuxtLink v-if="user == null" class="nav-link text-white" to="/login">
                  Deposite
                </NuxtLink>
                <NuxtLink v-else class="nav-link text-white" to="/payment">
                  Deposite
                </NuxtLink>
              </li>

          


              <li class="nav-item">
                <NuxtLink v-if="user == null" class="nav-link text-white" to="/login">Contact Us</NuxtLink>
                <NuxtLink v-else class="nav-link text-white" to="/contact">Contact Us</NuxtLink>
              </li>
              <li class="nav-item">
                <a class="nav-link text-white" @click="toggleSearch">
                  <v-icon>mdi-magnify</v-icon>
                </a>
                <input v-show="isSearchVisible" type="text" class="form-control" placeholder="Search"
                  @blur="toggleSearch" />
              </li>
            </ul>


            <!-- Search icon and input -->

            <v-spacer></v-spacer>
            <div v-if="!user == true">
              <v-row>
                <v-col>
                  <v-btn to="/login">Login</v-btn>
                </v-col>
                <v-col>
                  <v-btn to="/signup">Register</v-btn>
                </v-col>
              </v-row>
            </div>
            <div v-else>
              <avatar />
            </div>

          </div>
        </div>
      </div>
    </nav>
  </div>
</template>



<style>
.bg-faded {
  background: none;
}
</style>



<script setup>
import logo from '../assets/img/A-transformed.png'
// import { ref } from "vue";
const { auth } = useSupabaseClient()
const user = useSupabaseUser();
const isSearchVisible = ref(false);

const toggleSearch = () => {
  isSearchVisible.value = !isSearchVisible.value;
};
// function canvaHide()




const isMenuOpen = ref(false);

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};

const logout = async () => {
  await auth.signOut();
}
// Close the dropdown menu when clicking outside of it
onMounted(() => {
  window.addEventListener('click', (event) => {
    if (isMenuOpen.value && !event.target.closest('.menu-container')) {
      isMenuOpen.value = false;
    }
  });
});
</script>
