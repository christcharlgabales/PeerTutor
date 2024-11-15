<script setup>
import { ref } from 'vue'
import { useField, useForm } from 'vee-validate'

const { handleSubmit } = useForm({
  validationSchema: {
    firstName(value) {
      return value?.length >= 2 || 'First Name needs to be at least 2 characters.'
    },
    lastName(value) {
      return value?.length >= 2 || 'Last Name needs to be at least 2 characters.'
    },
    password(value) {
      return /^[0-9-]{7,}$/.test(value) || 'Password needs to be at least 7 digits.'
    },
    email(value) {
      return /^[a-z.-]+@[a-z.-]+\.[a-z]+$/i.test(value) || 'Must be a valid e-mail.'
    },
    role(value) {
      return value || 'Select a role.'
    },
    occupation(value) {
      return value || 'Select a occupation.'
    }
  }
})

// Form fields
const visible = ref(false)
const repeatVisible = ref(false)

const firstName = useField('firstName')
const lastName = useField('lastName')
const password = useField('password')
const email = useField('email')
const role = useField('role')
const occupation = useField('occupation')

const items = ref(['Student', 'Tutor'])
const occupationItems = ref([
  'Teacher',
  'Tutor',
  'Student',
  'Professor',
  'Online Instructor',
  'Education Consultant',
  'School Administrator',
  'Curriculum Developer',
  'Learning Facilitator',
  'Private Tutor',
  'Training Specialist',
  'Subject Matter Expert',
  'Mentor',
  'Coach',
  'Librarian',
  'Research Assistant',
  'Guidance Counselor',
  'Special Education Teacher',
  'Vocational Trainer',
  'Child Care Worker',
  'Other'
])
const loading = ref(false)

// Form submission
const submit = handleSubmit((values) => {
  alert(JSON.stringify(values, null, 2))
})
</script>

<template>
  <v-form @submit.prevent="submit" fast-fail>
    <v-row class="d-flex mx-auto" align="center" justify="center">
      <!-- First Name and Last Name -->
      <v-col cols="12" md="6">
        <v-text-field
          variant="outlined"
          prepend-inner-icon="mdi-badge-account-outline"
          density="compact"
          :error-messages="firstName.errorMessage"
          placeholder="First Name"
          label="First Name"
          hide-details="auto"
          clearable
        ></v-text-field>
      </v-col>

      <v-col cols="12" md="6">
        <v-text-field
          variant="outlined"
          density="compact"
          :error-messages="lastName.errorMessage"
          placeholder="Last Name"
          label="Last Name"
          hide-details="auto"
          clearable
        ></v-text-field>
      </v-col>

      <!-- Email Field -->
      <v-col cols="12">
        <v-text-field
          variant="outlined"
          prepend-inner-icon="mdi-email"
          density="compact"
          :error-messages="email.errorMessage"
          placeholder="user@gmail.com"
          label="Email"
          hide-details="auto"
          clearable
        ></v-text-field>
      </v-col>

      <!-- Password Fields -->
      <v-col cols="12" md="6">
        <v-text-field
          density="compact"
          variant="outlined"
          prepend-inner-icon="mdi-lock"
          :append-inner-icon="visible ? 'mdi-eye-off' : 'mdi-eye'"
          :type="visible ? 'text' : 'password'"
          @click:append-inner="visible = !visible"
          :error-messages="password.errorMessage"
          label="Password"
          placeholder="Enter your password"
          hide-details="auto"
          clearable
        ></v-text-field>
      </v-col>

      <v-col cols="12" md="6">
        <v-text-field
          density="compact"
          variant="outlined"
          prepend-inner-icon="mdi-lock-check"
          :append-inner-icon="repeatVisible ? 'mdi-eye-off' : 'mdi-eye'"
          :type="repeatVisible ? 'text' : 'password'"
          @click:append-inner="repeatVisible = !repeatVisible"
          label="Repeat Password"
          placeholder="Repeat your password"
          hide-details="auto"
          clearable
        ></v-text-field>
      </v-col>

      <!-- Occupation and Role Fields -->
      <v-col cols="12" md="7">
        <v-select
          :error-messages="occupation.errorMessage"
          :items="occupationItems"
          label="Occupation"
          variant="outlined"
          density="compact"
        ></v-select>
      </v-col>

      <v-col cols="12" md="5">
        <v-select
          :error-messages="role.errorMessage"
          :items="items"
          label="Role"
          variant="outlined"
          density="compact"
        ></v-select>
      </v-col>

      <!-- Submit Button -->

      <v-container width="200" class="mb-3">
        <v-btn
          :loading="loading"
          color="teal-darken-2"
          size="large"
          type="submit"
          variant="elevated"
          block
          elevation="10"
          style="border-radius: 30px"
        >
          <span style="color: #80cbc4">Create</span>
        </v-btn>
      </v-container>
    </v-row>
  </v-form>
</template>
