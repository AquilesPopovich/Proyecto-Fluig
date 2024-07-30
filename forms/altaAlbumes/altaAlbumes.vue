<template>
  <div v-if="isVisible" class="modal-overlay">
    <div :class="['form-container', getBg(color)]">
      <form name="form" role="form" @submit.prevent="handleSubmit">
        <h2>Carga de Álbum</h2>

        <div class="form-group">
          <label for="fechaCarga">Fecha de Carga</label>
          <input type="text" id="fechaCarga" v-model="fechaCarga" readonly />
        </div>

        <div class="form-group">
          <label>responsable</label>
            <input class="form-control" type="zoom" name="responsable" id="responsable"
              data-zoom="{
              'datasetId':'AprobadorGrupo',
              'fields':[ {
              'field':'nombre',
              'label':'Aprobador',
              'standard':'true',
              'search':'true'
              },
              {
              'field':'mail',
              'label':'mail'
              }
              ]}" />
        </div>

        <div class="form-group">
          <label for="nombreAlbum">Nombre de Álbum</label>
          <input type="text" id="nombreAlbum" v-model="nombreAlbum" required />
        </div>

        <div class="form-group">
          <label for="artista">Artista</label>
          <input type="text" id="artista" v-model="artista" required />
        </div>

        <div class="form-group">
          <label for="color">Color</label>
          <select v-model="color" id="color">
            <option value="gris">⚫ Gris</option>
            <option value="amarillo">🟡 Amarillo</option>
            <option value="rojo">🔴 Rojo</option>
            <option value="azul">🔵 Azul</option>
            <option value="verde">🟢 Verde</option>
          </select>
        </div>
        <button type="submit" class="submit-button">Enviar</button>
        <button type="button" @click="closeModal" class="cancel-button">Cancelar</button>
      </form>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  data() {
    return {
      isVisible: false,
      fechaCarga: new Date().toISOString().split('T')[0],
      usuario: '',
      nombreAlbum: '',
      artista: '',
      color: 'gris'
    };
  },
  methods: {
    getBg(bg) {
      switch (bg) {
        case 'gris':
          return 'bg-primary';
        case 'amarillo':
          return 'bg-warning';
        case 'rojo':
          return 'bg-danger';
        case 'azul':
          return 'bg-info';
        case 'verde':
          return 'bg-success';
        default:
          return '';
      }
    },
    handleSubmit() {
      console.log('fecha: ' + this.fechaCarga, 
                  'usuario: ' + this.usuario, 
                  'nombre album: ' + this.nombreAlbum, 
                  'artista: ' + this.artista, 
                  'color: ' + this.color);
      this.closeModal();
    },
    openModal() {
      this.isVisible = true;
    },
    closeModal() {
      this.isVisible = false;
      this.nombreAlbum = '';
      this.artista = '';
      this.color = 'gris';
    }
  }
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.4);
  display: flex;
  justify-content: center;
  align-items: center;
}

.form-container {
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  padding: 20px;
  max-width: 500px;
  width: 100%;
  box-sizing: border-box;
  transition: background-color 0.3s ease;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  font-size: 14px;
  color: #333;
  margin-bottom: 5px;
}

input[type="text"],
select {
  width: 100%;
  padding: 10px;
  font-size: 14px;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-sizing: border-box;
}

input[readonly] {
  background-color: #f9f9f9;
}

select {
  background-color: #fff;
}

input:focus,
select:focus {
  border-color: #007bff;
  outline: none;
}

.submit-button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 10px 15px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
}

.submit-button:hover {
  background-color: #0056b3;
}

.cancel-button {
  background-color: #f8f9fa;
  color: #333;
  border: 1px solid #ddd;
  padding: 10px 15px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
}

.cancel-button:hover {
  background-color: #e2e6ea;
}

.bg-primary {
  border: 2px solid #6c757d;
}

.bg-warning {
  border: 2px solid #ffc107;
}

.bg-danger {
  border: 2px solid #dc3545;
}

.bg-info {
  border: 2px solid #17a2b8;
}

.bg-success {
  border: 2px solid #28a745;
}
</style>
