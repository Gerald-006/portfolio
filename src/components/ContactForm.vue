<template>
  <div class="fixed top-0 bg-white h-screen w-screen bg-opacity-50 m">
    <form
      @submit.prevent="submitForm"
      class="h-4/5 w-full md:w-96 mx-auto mt-16 bg-white rounded-lg border-2"
    >
      <div class="flex justify-end mt-2 mr-2">
        <i @click="hideForm"
          class="hover:bg-blue-200 text-center border-2 rounded-full h-8 w-8 text-blue-800 text-lg fa-solid fa-xmark"
        ></i>
      </div>
      <div class="text-2xl ml-7">Get in touch</div>
      <div class="flex flex-col">
        <label class="mt-8 text-xs text-custom-blue font-bold pl-6">NAME</label>
        <input v-model="formData.name" class="border-b-2 mt-2 pl-2" type="text" />
      </div>
      <div class="flex flex-col">
        <label class="mt-4 text-xs text-custom-blue font-bold pl-6"
          >Email</label
        >
        <input v-model="formData.email" class="border-b-2 mt-2 pl-2" type="email " required />
      </div>
      <div class="flex flex-col">
        <label class="mt-4 text-xs text-custom-blue font-bold pl-6"
          >Subject</label
        >
        <input v-model="formData.subject" class="border-b-2 mt-2 pl-2" type="text" />
      </div>
      <div class="flex flex-col">
        <label class="mt-2 text-xs text-custom-blue font-bold pl-6 mb-2"
          >Message</label
        >
        <textarea v-model="formData.message" class=" pl-2 pt-2" rows="4" cols="50"></textarea>
      </div>
      <div class="flex justify-center mt-5 " >
        <button  class="customcolor text-xl p-4 text-white rounded-lg">send</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formData: {
        name: '',
        email: '',
        message: '',
        subject: '',
      },
    };
  },
  methods: {
    hideForm() {
      this.$emit('closeForm');
    },
    async submitForm() {
      
      try {
        const response = await fetch('https://formspree.io/f/mqkvedaa', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify(this.formData),
        });

        if (response.ok) {
          
          this.formData.name = '';
          this.formData.email = '';
          this.formData.message = '';
          this.formData.subject = '';
          this.$emit('closeForm');
          
          alert('Thank you for Contacting me! I will get back shortly');
        } else {
         
          alert('Error sending the message. Please try again later.');
        }
      } catch (error) {
       
        alert('An error occurred. Please try again later.');
      }
    },
  
  }
};
</script>
