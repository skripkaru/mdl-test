<template>
  <DefaultLayout>
    <section class="preferences">
      <Heading
        title="Preferences"
        text="On this page you can configure the main system parameters available for customization"
      />
      <form class="preferences__form preferences-form">
        <div class="preferences-form__control">
          <p class="preferences-form__label">Company Title</p>
          <Input
            type="text"
            name="companyTitle"
            placeholder="Enter title"
            v-model="companyTitle"
          />
        </div>
        <div class="preferences-form__control">
          <p class="preferences-form__label">First Day</p>
          <VSelect
            :options="days"
            @select="selectDay"
          />
        </div>
        <div class="preferences-form__control">
          <p class="preferences-form__label">Container Width</p>
          <VSelect
            :options="width"
            @select="selectWidth"
          />
        </div>
        <div class="preferences-form__control">
          <p class="preferences-form__label">Homepage</p>
          <VSelect
            :options="pages"
            @select="selectPage"
          />
        </div>
        <div class="preferences-form__control">
          <p class="preferences-form__label">Indent Size</p>
          <Input
            type="number"
            name="indent_size"
            placeholder="Enter size"
            v-model="indent_size"
          />
        </div>
        <div class="preferences-form__control">
          <p class="preferences-form__label">Personal Code</p>
          <div class="preferences-form__group">
            <Input
              type="number"
              name="code_first_val"
              v-model="code_part_01"
            />
            -
            <Input
              type="number"
              name="code_second_val"
              v-model="code_part_02"
            />
            -
            <Input
              type="number"
              name="code_third_val"
              v-model="code_part_03"
            />
          </div>
        </div>
        <div class="preferences-form__control preferences-form__control_start">
          <p class="preferences-form__label">Theme</p>
          <div class="preferences-form__radio-group">
            <div class="preferences-form__radio">
              <Radio
                label="Light"
                name="theme"
                value="light"
                v-model="theme"
              />
            </div>
            <div class="preferences-form__radio">
              <Radio
                label="Dark"
                name="theme"
                value="dark"
                v-model="theme"
              />
            </div>
          </div>
        </div>
        <div class="preferences-form__btns">
          <Button variant="fill" @click.prevent="handleSubmit">Apply and Save</Button>
          <Button variant="outline">Cancel</Button>
        </div>
      </form>
    </section>
  </DefaultLayout>
</template>

<script>

import Heading from "@/components/Heading";
import DefaultLayout from "@/layouts/DefaultLayout";
import Input from "@/components/Input";
import Button from "@/components/Button";
import VSelect from "@/components/VSelect";
import Radio from "@/components/Radio";

export default {
  name: 'App',
  components: {
    Button,
    DefaultLayout,
    Heading,
    Input,
    VSelect,
    Radio,
  },
  data() {
    return {
      days: [
        {value: '1', label: 'Monday'},
        {value: '2', label: 'Sunday'},
        {value: '3', label: 'System'},
      ],
      width: [
        {value: '1', label: 'Fixed'},
        {value: '2', label: 'Responsive'},
      ],
      pages: [
        {value: '1', label: 'Starred Projects'},
        {value: '2', label: 'Shared Projects'},
      ],
      companyTitle: '',
      firstDay: '',
      containerWidth: '',
      homepage: '',
      indent_size: null,
      code_part_01: null,
      code_part_02: null,
      code_part_03: null,
      personal_code: null,
      theme: localStorage.getItem('theme') || 'light',
      preferences: null,
    }
  },
  methods: {
    selectDay(option) {
      this.firstDay = option.label
    },
    selectWidth(option) {
      this.containerWidth = option.label
    },
    selectPage(option) {
      this.homepage = option.label
    },
    switchTheme() {
      if (this.theme === 'dark') {
        document.documentElement.setAttribute('theme', 'dark');
        localStorage.setItem('theme', 'dark')
      } else {
        document.documentElement.removeAttribute('theme');
        localStorage.removeItem('theme')
      }
    },
    saveToLS(key, obj) {
      localStorage.setItem(key, JSON.stringify(obj))
    },
    getToLS(key) {
      return JSON.parse(localStorage.getItem(key))
    },
    handleSubmit() {
      const data = {
        companyTitle: this.companyTitle,
        firstDay: this.firstDay,
        containerWidth: this.containerWidth,
        homepage: this.homepage,
        indent_size: this.indent_size,
        code_part_01: this.code_part_01,
        code_part_02: this.code_part_02,
        code_part_03: this.code_part_03,
        personal_code: `${this.code_part_01}-${this.code_part_02}-${this.code_part_03}`,
      }

      this.saveToLS('preferences', data)
      this.switchTheme()
    },
  },
  mounted() {
    this.companyTitle = this.getToLS('preferences').companyTitle || ''
    this.firstDay = this.getToLS('preferences').firstDay
    this.containerWidth = this.getToLS('preferences').containerWidth || ''
    this.homepage = this.getToLS('preferences').homepage || ''
    this.indent_size = this.getToLS('preferences').indent_size || ''
    this.code_part_01 = this.getToLS('preferences').code_part_01 || ''
    this.code_part_02 = this.getToLS('preferences').code_part_02 || ''
    this.code_part_03 = this.getToLS('preferences').code_part_03 || ''
    this.personal_code = this.getToLS('preferences').personal_code || ''
    this.theme = localStorage.getItem('theme') || 'light'
    this.preferences = this.getToLS('preferences') || null

    if (this.theme === 'dark') {
      this.switchTheme()
    }
  }
}
</script>

<style lang="scss">

.preferences {
  padding: 2rem;
}

.preferences-form {
  max-width: 320px;

  &__label {
    font-size: 0.875rem;
    line-height: 16px;
    color: var(--color-text-500);
  }

  &__control {
    display: grid;
    grid-template-columns: 1fr 196px;
    gap: 1rem;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1.5rem;

    &_start {
      align-items: flex-start;
    }
  }

  &__group {
    display: flex;
    align-items: center;
    gap: .5rem;
  }

  &__radio-group {
    display: flex;
    flex-direction: column;
  }

  &__radio {

    &:not(:last-child) {
      margin-bottom: .5rem;
    }
  }

  &__btns {
    margin-top: 2rem;
    display: flex;
    gap: 1rem;
  }
}

</style>
