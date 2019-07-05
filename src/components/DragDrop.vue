<template>
  <div class="hello">
    <div id="drag-drop-area">
      <div class="drag-drop-inside">
        <p class="drag-drop-info">ここにファイルをドロップ</p>
        <p>または</p>
        <p class="drag-drop-file">ファイルを選択</p>
      </div>
      <p class="drag-drop-buttons">
        <input id="fileInput" type="file" value="ファイルを選択" :name="name" :required="required" :multiple="multiple">
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DragDrop',
  props: {
    name: String,
    required: String,
    multiple: String,
  },
  data() {
    return {
      FileData: {}
    }
  },
  mounted() {
    var fileArea = document.getElementById('drag-drop-area');
    var fileInput = document.getElementById('fileInput');

    document.addEventListener('dragstart', function(event) {
      const draggable = event.target.getAttribute('draggable');
      if (!draggable || draggable === 'auto') {
        event.preventDefault();
      }
    });

    fileArea.addEventListener('dragover', function(event){
      event.preventDefault();
      fileArea.classList.add('dragover');
    });

    fileArea.addEventListener('dragleave', function(event){
      event.preventDefault();
      fileArea.classList.remove('dragover');
    });

    fileArea.addEventListener('drop', (event)=> {
      event.preventDefault();
      fileArea.classList.remove('dragover');

      var files = event.dataTransfer.files;
      fileInput.files = files;

      this.FileData = fileInput.files;

      this.$emit('checkResult', this.FileData);
    });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#drag-drop-area {
  background-color: #eee;
  width: 100%;
  height: 100%;
  padding: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: #666;
  position: relative;
  border-radius: 20px;

  &:before {
    transition: all 0.2s ease;
    transform: translate(-50%,-50%);
    content: '';
    display: block;
    position: absolute; top: 50%; left: 50%;
    border: 5px solid #ddd;
    border-radius: 20px;
    width: 100%; height: 100%;
    box-sizing: border-box;
  }

  &:hover,
  &.dragover {
    &:before {
      border-color: rgb(255, 135, 135);
      border-width: 10px;
    }
  }

  .drag-drop-inside {
    position: relative;
    z-index: 2;
  }

  .drag-drop-info {
    font-size: 1.6rem;
    font-weight: bold;
    margin-bottom: 20px;
  }
  .drag-drop-file {
    font-size: 1.6rem;
    font-weight: bold;
    margin-top: 20px;
  }

  .drag-drop-buttons {
    position: absolute; top: 0; left: 0;
    opacity: 0;
    width: 100%; height: 100%;
    z-index: 2;

    input {
      cursor: pointer;
      width: 100%; height: 100%;
      display: block;
      appearance: none;
    }
  }
}

*[draggable=true] {
  cursor: pointer;
}

.not_select {
  user-select: none;
}
</style>
