<script setup lang="ts">
  import Title from '../../components/Title.vue'
  import Divider from '../../components/Divider.vue'
  import { useSettingsStore } from '../../stores/settings'
  import SelectInput from '../../components/SelectInput.vue'
  import TextInput from '../../components/TextInput.vue'
  import { ref } from 'vue'
  import ToastAlert from '@/components/ToastAlert.vue'

  const saved = ref(false)
  const showToast = ref(false)
  const settingsStore = useSettingsStore()

  const saveSettings = () => {
    saved.value = true
    showToast.value = true
    settingsStore.update()
    setTimeout(() => {
      saved.value = false
      showToast.value = false
    }, 2000)
  }
</script>

<template>
  <div>
    <ToastAlert v-if="showToast" title="Settings Saved" />
    <div class="flex items-center justify-between">
      <Title>Editor</Title>
    </div>
    <Divider class="mt-3" />
    <div class="mt-3 grid grid-cols-2 items-center">
      <div>Editor font size</div>
      <TextInput id="editor-font-size" v-model="settingsStore.settings.editorFontSize" @change="saveSettings()" />
    </div>
    <Divider class="mt-3" />
    <div class="mt-3 grid grid-cols-2 items-center">
      <div>Editor word wrap</div>
      <SelectInput
        id="editor-word-wrap"
        v-model="settingsStore.settings.editorWordWrap"
        @change="saveSettings()"
        placeholder="Select"
      >
        <option value="on">Wrap</option>
        <option value="off">No Wrap</option>
      </SelectInput>
    </div>
    <Divider class="mt-3" />
    <div class="mt-3 grid grid-cols-2 items-center">
      <div>Line numbers</div>
      <SelectInput
        id="editor-line-numbers"
        v-model="settingsStore.settings.editorLineNumbers"
        @change="saveSettings()"
        placeholder="Select"
      >
        <option value="on">Enabled</option>
        <option value="off">Disabled</option>
      </SelectInput>
    </div>
    <Divider class="mt-3" />
    <div class="mt-3 grid grid-cols-2 items-center">
      <div>Indentation guides</div>
      <SelectInput
        id="editor-indent-guides"
        v-model="settingsStore.settings.editorIndentGuides"
        @change="saveSettings()"
        placeholder="Select"
      >
        <option value="on">Enabled</option>
        <option value="off">Disabled</option>
      </SelectInput>
    </div>
    <Divider class="mt-3" />
    <div class="mt-3 grid grid-cols-2 items-center">
      <div>Vim mode</div>
      <SelectInput
        id="editor-vim-mode"
        v-model="settingsStore.settings.vimMode"
        @change="saveSettings()"
        placeholder="Select"
      >
        <option value="on">Enabled</option>
        <option value="off">Disabled</option>
      </SelectInput>
    </div>
  </div>
</template>

<style scoped></style>
