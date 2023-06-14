
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
          </a>
          <transition name="fade">
            <ul class="nav flex-column" v-if="isDropdownOpen(item.id)">
              <li
                class="nav-item"
                v-for="subItem in item.subItems"
                :key="subItem.id"
              >
                <a
                  class="nav-link second"
                  @click="toggleSubmenu(item.id, subItem.id)"
                  @dblclick="closeSubmenu(item.id, subItem.id)"
                  :class="{ activesecond: isSubmenuOpen(item.id, subItem.id) }"
                >
                  {{ subItem.label }}
                </a>
                <transition name="fade">
                  <ul class="nav flex-column" v-if="isSubmenuOpen(item.id, subItem.id)">
                    <li
                      class="nav-item"
                      v-for="subMenu in subItem.subMenu"
                      :key="subMenu.id"
                    >
                      <a class="nav-link " href="#">{{ subMenu.label }}</a>
                    </li>
                  </ul>
                </transition>
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
            {
              id: 1,
              label: "Part1: Especializadas",
              subMenu: [
                { id: 1, label: "Plan inicial" },
                { id: 2, label: "Seguimiento" },
                { id: 3, label: "Cierre" },
                { id: 4, label: "Consulta" },
              ],
            },
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
      submenus: {} as { [key: number]: { [key: number]: boolean } },
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
    closeSubmenu(itemId: number, subItemId: number) {
      if (this.submenus[itemId]) {
        this.$set(this.submenus[itemId], subItemId, false);
      }
    },
    isSubmenuOpen(itemId: number, subItemId: number) {
      return this.submenus[itemId] && this.submenus[itemId][subItemId];
    },
    toggleSubmenu(itemId: number, subItemId: number) {
      if (!this.submenus[itemId]) {
        this.$set(this.submenus, itemId, {});
      }
      for (const submenuId in this.submenus[itemId]) {
        if (Number(submenuId) !== subItemId) {
          this.closeSubmenu(itemId, Number(submenuId));
        }
      }
      if (this.submenus[itemId][subItemId]) {
        this.closeSubmenu(itemId, subItemId);
      } else {
        this.$set(this.submenus[itemId], subItemId, true);
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

.sidebar .nav-link.activesecond {
  transition-duration: 0.4s;
  background-color: #ffffff;
  color: #000000;
}

.second{
  background-color: #d4d4d4;
}


.sidebar .nav-link {
  text-align: left;
}

.content {
  margin-left: 200px;
  padding: 15px;
}

.fade-enter-active {
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
