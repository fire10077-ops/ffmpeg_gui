<template>
  <div class="container">
    <h1>🎬 FFmpeg GUI Converter</h1>
    
    <!-- Выбор файла -->
    <div class="file-selector">
      <h2>📁 Выберите файл для конвертации</h2>
      <button @click="selectFile">Выбрать файл</button>
      <div class="file-info" v-if="selectedFile">
        Выбран: {{ selectedFile.name }}
        <br>
        <small>Путь: {{ selectedFile.path }}</small>
      </div>
    </div>

    <!-- Выбор формата -->
    <div class="format-selector">
      <h2>🔄 Выберите формат</h2>
      <select v-model="selectedFormat">
        <option value="mp4">MP4 (видео)</option>
        <option value="gif">GIF (анимация)</option>
        <option value="mp3">MP3 (аудио)</option>
        <option value="avi">AVI (видео)</option>
      </select>
    </div>

    <!-- Кнопка конвертации -->
    <div class="actions">
      <button 
        @click="convertFile" 
        :disabled="!selectedFile"
        class="convert-btn"
      >
        🚀 Конвертировать
      </button>
    </div>

    <!-- Прогресс -->
    <div class="progress" v-if="isConverting">
      <div class="progress-bar">
        <div class="progress-fill" :style="{ width: progress + '%' }"></div>
      </div>
      <div class="progress-text">{{ progress }}%</div>
    </div>
  </div>
</template>

<script>
// ВАРИАНТ 1: С импортами (если установил plugin-dialog)
// import { open } from '@tauri-apps/plugin-dialog'
// import { invoke } from '@tauri-apps/api/core'

export default {
  data() {
    return {
      selectedFile: null,
      selectedFormat: 'mp4',
      isConverting: false,
      progress: 0
    }
  },
  methods: {
    async selectFile() {
      try {
        // ВАРИАНТ 1: Настоящий выбор файла (раскомментировать после установки)
        // const selected = await open({
        //   multiple: false,
        //   filters: [{
        //     name: 'Media Files',
        //     extensions: ['mp4', 'avi', 'mov', 'mkv', 'mp3', 'wav', 'gif']
        //   }]
        // })
        // 
        // if (selected) {
        //   this.selectedFile = {
        //     name: selected.split('\\').pop(),
        //     path: selected
        //   }
        // }
        
        // ВАРИАНТ 2: Временная заглушка (используй этот пока)
        console.log('Выбор файла...')
        this.selectedFile = {
          name: 'test_video.mp4',
          path: 'C:/Users/fire1/Videos/test.mp4'
        }
        
      } catch (error) {
        console.error('Ошибка:', error)
      }
    },
    
    async convertFile() {
      if (!this.selectedFile) return
      
      this.isConverting = true
      this.progress = 0
      
      try {
        // ВАРИАНТ 1: Настоящая конвертация (позже)
        // await invoke('convert_video', {
        //   inputPath: this.selectedFile.path,
        //   outputFormat: this.selectedFormat
        // })
        
        // ВАРИАНТ 2: Симуляция прогресса (используй этот пока)
        const interval = setInterval(() => {
          this.progress += 10
          if (this.progress >= 100) {
            clearInterval(interval)
            this.isConverting = false
            alert('✅ Конвертация завершена!')
          }
        }, 300)
        
      } catch (error) {
        alert('❌ Ошибка: ' + error)
        this.isConverting = false
      }
    }
  }
}
</script>

<style>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

h1 {
  color: #333;
  text-align: center;
  margin-bottom: 30px;
}

.file-selector, .format-selector, .actions {
  margin-bottom: 30px;
  padding: 20px;
  background: #f5f5f5;
  border-radius: 8px;
}

h2 {
  margin-top: 0;
  color: #555;
}

button {
  padding: 10px 20px;
  background: #007acc;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

button:hover {
  background: #005a9e;
}

button:disabled {
  background: #ccc;
  cursor: not-allowed;
}

.convert-btn {
  background: #28a745;
  font-size: 18px;
  padding: 15px 30px;
}

.convert-btn:hover {
  background: #218838;
}

.file-info {
  margin-top: 10px;
  padding: 10px;
  background: #e9ecef;
  border-radius: 4px;
}

select {
  padding: 10px;
  font-size: 16px;
  border-radius: 4px;
  border: 1px solid #ccc;
  width: 200px;
}

.progress {
  margin-top: 30px;
}

.progress-bar {
  height: 20px;
  background: #e9ecef;
  border-radius: 10px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background: #28a745;
  transition: width 0.3s;
}

.progress-text {
  text-align: center;
  margin-top: 10px;
  font-weight: bold;
}
</style>
