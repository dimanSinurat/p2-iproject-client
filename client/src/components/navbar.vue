<template>
  <div class="header">
    <div class="menu-circle"></div>
    <div class="header-menu">
      <p>Hai, welcome {{get_name}}</p>
    </div>
    <div class="search-bar" style="margin-left: 280px">
      <input type="text" placeholder="Search" />
    </div>
    <div class="header-profile">
      <div class="notification">
        <span class="notification-number">3</span>
        <svg
          viewBox="0 0 24 24"
          fill="currentColor"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
          class="feather feather-bell"
        >
          <path
            d="M18 8A6 6 0 006 8c0 7-3 9-3 9h18s-3-2-3-9M13.73 21a2 2 0 01-3.46 0"
          />
        </svg>
      </div>

      <a href="">
          <img
          class="profile-img"
          src="https://images.unsplash.com/photo-1600353068440-6361ef3a86e8?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=1000&q=80"
          alt=""
          @click.prevent="logout"
        />
      </a>

    </div>
  </div>
</template>

<script>
export default {
  name: 'navbar',
  computed: {
    get_name(){
      return this.$store.state.username
    }
  },
  methods: {
    logout () {
      localStorage.clear();
      this.$store.commit('LOGINEXE', false)
      this.$router.push('/login')
    }
  }
}
</script>

<style scoped>
.header {
  display: flex;
  align-items: center;
  flex-shrink: 0;
  height: 58px;
  width: 100%;
  border-bottom: 1px solid var(--border-color);
  padding: 0 30px;
  white-space: nowrap;
}
@media screen and (max-width: 480px) {
  .header {
    padding: 0 16px;
  }
}
.header-menu {
  display: flex;
  align-items: center;
}
.header-menu a {
  padding: 20px 30px;
  text-decoration: none;
  color: var(--inactive-color);
  border-bottom: 2px solid transparent;
  transition: 0.3s;
}
@media screen and (max-width: 610px) {
  .header-menu a:not(.main-header-link) {
    display: none;
  }
}
.header-menu a.is-active,
.header-menu a:hover {
  color: var(--theme-color);
  border-bottom: 2px solid var(--theme-color);
}
.notify {
  position: relative;
}
.notify:before {
  content: "";
  position: absolute;
  background-color: #3a6df0;
  width: 6px;
  height: 6px;
  border-radius: 50%;
  right: 20px;
  top: 16px;
}
@media screen and (max-width: 1055px) {
  .notify {
    display: none;
  }
}
.menu-circle {
  width: 15px;
  height: 15px;
  background-color: #f96057;
  border-radius: 50%;
  box-shadow: 24px 0 0 0 #f8ce52, 48px 0 0 0 #5fcf65;
  margin-right: 195px;
  flex-shrink: 0;
}
@media screen and (max-width: 945px) {
  .menu-circle {
    display: none;
  }
}
.search-bar {
  height: 40px;
  display: flex;
  width: 100%;
  max-width: 400px;
  padding-left: 16px;
  border-radius: 4px;
}
.search-bar input {
  width: 100%;
  height: 100%;
  border: none;
  background-color: var(--search-bg);
  border-radius: 4px;
  font-family: var(--body-font);
  font-size: 15px;
  font-weight: 500;
  padding: 0 20px 0 40px;
  box-shadow: 0 0 0 2px #000;
  background-image: url("data:image/svg+xml");
  background-size: 14px;
  background-repeat: no-repeat;
  background-position: 16px 48%;
  color: var(--theme-color);
  /* charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 56.966 56.966' fill='%23717790c7'%3e%3cpath d='M55.146 51.887L41.588 37.786A22.926 22.926 0 0046.984 23c0-12.682-10.318-23-23-23s-23 10.318-23 23 10.318 23 23 23c4.761 0 9.298-1.436 13.177-4.162l13.661 14.208c.571.593 1.339.92 2.162.92.779 0 1.518-.297 2.079-.837a3.004 3.004 0 00.083-4.242zM23.984 6c9.374 0 17 7.626 17 17s-7.626 17-17 17-17-7.626-17-17 7.626-17 17-17z'/%3e%3c/svg%3e"); */
}
.search-bar input::placeholder {
  font-family: var(--body-font);
  color: var(--inactive-color);
  font-size: 15px;
  font-weight: 500;
}
.header-profile {
  display: flex;
  align-items: center;
  padding: 0 16px 0 40px;
  margin-left: auto;
  flex-shrink: 0;
}
.header-profile svg {
  width: 22px;
  color: #f9fafb;
  flex-shrink: 0;
}
.notification {
  position: relative;
}
.notification-number {
  position: absolute;
  background-color: #3a6df0;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  font-size: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  right: -6px;
  top: -6px;
}
.notification + svg {
  margin-left: 22px;
}
@media screen and (max-width: 945px) {
  .notification + svg {
    display: none;
  }
}
.profile-img {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid var(--theme-color);
  margin-left: 22px;
}
.wide .header-menu,
.wide .header-profile {
  display: none;
}
.wide .search-bar {
  max-width: 600px;
  margin: auto;
  transition: 0.4s;
  box-shadow: 0 0 0 1px var(--border-color);
  padding-left: 0;
}
.wide .menu-circle {
  margin-right: 0;
}
</style>
