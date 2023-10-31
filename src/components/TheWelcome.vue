<script setup>
</script>

<template>
  <div className="bg-black min-h-screen flex justify-center items-center">
    <div className="bg-purple-500 p-8 rounded-md">
      <form>
        <div className="mb-4">
          <label className="block text-white mb-2" htmlFor="firstName">
            First Name
          </label>
          <input className="p-2 w-full rounded-md" type="text" id="firstName" name="firstName" />
        </div>
        <div className="mb-4">
          <label className="block text-white mb-2" htmlFor="lastName">
            Last Name
          </label>
          <input className="p-2 w-full rounded-md" type="text" id="lastName" name="lastName" />
        </div>
        <div className="mb-4">
          <label className="block text-white mb-2" htmlFor="username">
            Username
          </label>
          <input className="p-2 w-full rounded-md" type="text" id="username" name="username" />
        </div>
        <div className="mb-4">
          <label className="block text-white mb-2" htmlFor="email">
            Email
          </label>
          <input className="p-2 w-full rounded-md" type="email" id="email" name="email" />
        </div>
        <button className="block w-full bg-purple-700 p-2 rounded-md text-white mb-4 hover:bg-purple-600">
          Register
        </button>
        <button className="block w-full bg-purple-700 p-2 rounded-md text-white hover:bg-purple-600">
          Login
        </button>
      </form>
    </div>
  </div>
</template>
