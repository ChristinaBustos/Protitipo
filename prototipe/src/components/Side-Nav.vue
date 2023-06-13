<template>
    <div>
      <nav class="sidebar">
        <ul class="nav flex-column">
          <li class="nav-item" v-for="item in items" :key="item.id">
            <a class="nav-link" @click="toggleDropdown(item.id)" :class="{ 'active': isDropdownOpen(item.id) }">
              {{ item.label }}
              <i class="fas fa-chevron-down float-right" :class="{ 'fa-rotate-180': isDropdownOpen(item.id) }"></i>
            </a>
            <ul class="nav flex-column" v-show="isDropdownOpen(item.id)">
              <li class="nav-item" v-for="subItem in item.subItems" :key="subItem.id">
                <a class="nav-link" href="#">{{ subItem.label }}</a>
              </li>
            </ul>
          </li>
        </ul>
      </nav>
      <div class="content">
        <!-- Contenido principal de la página -->
      </div>
    </div>
  </template>
  
  <script >
  export default {
    name:'sideNav',
    data() {
      return {
        items: [
          {
            id: 1,
            label: 'Plan Desarrollo Docente',
            subItems: [
              { id: 1, label: 'Subitem 1.1' },
              { id: 2, label: 'Subitem 1.2' },
              { id: 3, label: 'Subitem 1.3' }
            ]
          },
          {
            id: 2,
            label: 'Capacitaciones',
            subItems: [
              { id: 4, label: 'Subitem 2.1' },
              { id: 5, label: 'Subitem 2.2' },
              { id: 6, label: 'Subitem 2.3' }
            ]
          },
          {
            id: 3,
            label: 'Reportes',
            subItems: [
              { id: 4, label: 'Subitem 2.1' },
              { id: 5, label: 'Subitem 2.2' },
              { id: 6, label: 'Subitem 2.3' }
            ]
          },
          {
            id: 4,
            label: 'Reportes',
            subItems: [
              { id: 4, label: 'Subitem 2.1' },
              { id: 5, label: 'Subitem 2.2' },
              { id: 6, label: 'Subitem 2.3' }
            ]
          },
          {
            id: 5,
            label: 'Área Gestora',
            subItems: [
              { id: 4, label: 'Subitem 2.1' },
              { id: 5, label: 'Subitem 2.2' },
              { id: 6, label: 'Subitem 2.3' }
            ]
          },
          {
            id: 6,
            label: 'Programa Educativo',
            subItems: [
              { id: 4, label: 'Subitem 2.1' },
              { id: 5, label: 'Subitem 2.2' },
              { id: 6, label: 'Subitem 2.3' }
            ]
          }
        ],
        dropdowns: {}
      };
    },
    methods: {
      toggleDropdown(id) {
        this.$set(this.dropdowns, id, !this.dropdowns[id]);
      },
      isDropdownOpen(id) {
        return this.dropdowns[id];
      }
    }
  };
  </script>
  
  <style>
  .sidebar {
    position: fixed;
    top: 80;
    left: 0;
    width: 300px;
    height: 200px;
    background-color: #ffffff;
    color: #00AD8A;
    padding-top: 100px;
  }
  
  .sidebar .nav-link.active {
    background-color: #00AD8A;
    color: #ffffff; /* Cambia el color de fondo del elemento seleccionado */
  }
  
  .content {
    margin-left: 200px;
    padding: 15px;
  }

  .bgsecondary{
  background-color: #00AD8A;
}

  </style>
  