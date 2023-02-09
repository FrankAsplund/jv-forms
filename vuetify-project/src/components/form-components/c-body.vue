<template>
    <div>
        <h3 class="label mb-4">{{ body }}</h3>
    </div>
</template>
    
    
    <script>
    export default {
      name: "Form-body-text",
      props: {
        body: {
          type: String,
        }
      },
    };
    </script>
    
    <style>
    .label {
        font-family: 'Poppins', sans-serif;
    
    }
    </style>