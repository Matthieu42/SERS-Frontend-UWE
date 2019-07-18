<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <b-navbar-brand href="/">SRES</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="/student/1">Student</b-nav-item>
        </b-navbar-nav>
        <b-navbar-nav>
          <b-nav-item-dropdown text="Administration" right>
            <b-dropdown-item href="/admin/addUser">Add User</b-dropdown-item>
            <b-dropdown-item href="/admin/users">List User</b-dropdown-item>
            <b-dropdown-item href="/admin/modules">List Modules</b-dropdown-item>
            <b-dropdown-item href="/admin/charts">Charts</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-item-dropdown right>
            <!-- Using 'button-content' slot -->
            <template slot="button-content">
              <em>User</em>
            </template>
            <b-dropdown-item href="#">Profile</b-dropdown-item>
            <b-dropdown-item href="#">Sign Out</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
</script>

<style>
</style>