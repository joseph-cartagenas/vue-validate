<script setup>
  import { ref } from "vue";

  // Form fields
  const form = ref({
    name: "",
    email: "",
    password: "",
  });

  // Error messages
  const errors = ref({
    name: "",
    email: "",
    password: "",
  });

  // Validation function
  const validateForm = () => {
    let valid = true;

    // Reset errors
    errors.value = { name: "", email: "", password: "" };

    // Name validation
    if (!form.value.name) {
      errors.value.name = "Name is required";
      valid = false;
    }

    // Email validation
    if (!form.value.email) {
      errors.value.email = "Email is required";
      valid = false;
    } else if (!/^\S+@\S+\.\S+$/.test(form.value.email)) {
      errors.value.email = "Invalid email format";
      valid = false;
    }

    // Password validation
    if (!form.value.password) {
      errors.value.password = "Password is required";
      valid = false;
    } else if (form.value.password.length < 6) {
      errors.value.password = "Password must be at least 6 characters";
      valid = false;
    }

    return valid;
  };

  // Form submission
  const submitForm = () => {
    if (validateForm()) {
      alert("Form submitted successfully!");
      console.log(form.value); // Replace with API call
    }
  };
</script>

<template>
  <div class="container mt-5 mb-5 w-50">
    <div class="card p-4 shadow">
      <h2 class="text-center text-primary">Form Validation with Bootstrap</h2>

      <form @submit.prevent="submitForm">
        <!-- Name Field -->
        <div class="mb-3">
          <label class="form-label">Name</label>
          <input v-model="form.name" type="text" class="form-control" :class="{ 'is-invalid': errors.name }" />
          <div v-if="errors.name" class="invalid-feedback">{{ errors.name }}</div>
        </div>

        <!-- Email Field -->
        <div class="mb-3">
          <label class="form-label">Email</label>
          <input v-model="form.email" type="text" class="form-control" :class="{ 'is-invalid': errors.email }" />
          <div v-if="errors.email" class="invalid-feedback">{{ errors.email }}</div>
        </div>

        <!-- Password Field -->
        <div class="mb-3">
          <label class="form-label">Password</label>
          <input v-model="form.password" type="password" class="form-control" :class="{ 'is-invalid': errors.password }" />
          <div v-if="errors.password" class="invalid-feedback">{{ errors.password }}</div>
        </div>

        <!-- Submit Button -->
        <button type="submit" class="btn btn-primary w-100">Submit</button>
      </form>
    </div>
  </div>
</template>
