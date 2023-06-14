<template>
    <div>
      <nav class="sidebar">
        <ul class="nav flex-column">
          <li class="nav-item" v-for="item in items" :key="item.id">
            <a
              class="nav-link"
              @click="toggleDropdown(item.id)"
              @dblclick="closeDropdown(item.id)"
              :class="{ active: isDropdownOpen(item.id) }"
            >
              {{ item.label }}
              <i
                class="fas fa-chevron-down float-right"
                :class="{ 'fa-rotate-180': isDropdownOpen(item.id) }"
              ></i>
            </a>
            <transition name="fade">
              <ul class="nav flex-column" v-if="isDropdownOpen(item.id)">
                <li
                  class="nav-item"
                  v-for="subItem in item.subItems"
                  :key="subItem.id"
                >
                  <a class="nav-link" href="#">
                    {{ subItem.label }}</a>
                </li>
              </ul>
            </transition>
          </li>
        </ul>
      </nav>
      <div class="content">
        <!-- Contenido principal de la página -->
      </div>
    </div>
  </template>
  
  <script lang="ts">
  import Vue from "vue";
  export default Vue.extend({
    name: "sideNav",
    data() {
      return {
        items: [
          {
            id: 1,
            label: "Plan Desarrollo Docente",
            subItems: [
              { id: 1, label: "Subitem 1.1" },
              { id: 2, label: "Subitem 1.2" },
              { id: 3, label: "Subitem 1.3" },
            ],
          },
          {
            id: 2,
            label: "Capacitaciones",
            subItems: [
              { id: 4, label: "Subitem 2.1" },
              { id: 5, label: "Subitem 2.2" },
              { id: 6, label: "Subitem 2.3" },
            ],
          },
          {
            id: 3,
            label: "Reportes",
            subItems: [
              { id: 7, label: "Subitem 3.1" },
              { id: 8, label: "Subitem 3.2" },
              { id: 9, label: "Subitem 3.3" },
            ],
          },
        ],
        dropdowns: {} as { [key: number]: boolean },
      };
    },
    methods: {
      closeDropdown(id: number) {
        this.$set(this.dropdowns, id, false);
      },
      isDropdownOpen(id: number) {
        return this.dropdowns[id];
      },
      toggleDropdown(id: number) {
        for (const dropdownId in this.dropdowns) {
          if (Number(dropdownId) !== id) {
            this.closeDropdown(Number(dropdownId));
          }
        }
        if (this.dropdowns[id]) {
          this.closeDropdown(id);
        } else {
          this.$set(this.dropdowns, id, true);
        }
      },
    },
  });
  </script>
  
  <style>
  .sidebar {
    position: fixed;
    top: 80px;
    left: 0;
    width: 300px;
    height: 200px;
    background-color: #ffffff;
    color: #00ad8a;
    padding-top: 100px;
  }
  
  .sidebar .nav-link.active {
    transition-duration: 0.4s;
    background-color: #00ad8a;
    color: #ffffff;
  }
  
  .sidebar .nav-link {
    text-align: left;
  }
  
  .content {
    margin-left: 200px;
    padding: 15px;
  }
  
  .fade-enter-active{
    /* transition: opacity 0.4s; */
    
    background: #fff;
    color: #666;
    padding: 0.1px;
    /* border: 1px solid #888; */
  
    transition-property: all;
    transition-duration: 0.4s; 
    transition-timing-function: linear;
  }
  
  
  .fade-enter,
  .fade-leave-to {
    opacity: 0;
  }
  </style>
  