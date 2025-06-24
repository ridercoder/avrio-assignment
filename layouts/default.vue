<template>
  <div class="flex h-screen bg-gray-50 font-inter text-gray-800">
    <!-- Sidebar -->
    <aside class="w-64 bg-white border-r shadow-sm hidden md:flex flex-col p-6">
      <h2 class="text-2xl font-bold text-blue-600 mb-8">Avrio</h2>
      <nav class="flex flex-col space-y-4 text-base">
        <a href="#" class="flex items-center gap-2 text-gray-600 hover:text-blue-600 transition">
          <span>📊</span><span>Dashboard</span>
        </a>
        <a href="#" class="flex items-center gap-2 text-gray-600 hover:text-blue-600 transition">
          <span>📁</span><span>Files</span>
        </a>
        <a href="#" class="flex items-center gap-2 text-gray-600 hover:text-blue-600 transition">
          <span>⚙️</span><span>Settings</span>
        </a>
      </nav>
    </aside>

    <!-- Main content -->
    <main class="flex-1 flex flex-col overflow-y-auto">
      <!-- Topbar -->
      <header class="bg-gradient-to-r from-blue-600 to-blue-500 text-white shadow px-6 py-4 flex justify-between items-center">
        <h1 class="text-xl font-semibold">Welcome, Devansh 👋</h1>
        <button class="bg-white text-blue-600 px-4 py-1 rounded shadow hover:bg-gray-100 transition">
          Logout
        </button>
      </header>

      <!-- Main Page Content -->
      <div class="p-6 space-y-6">
        <slot />
      </div>
    </main>
  </div>
</template>

<style scoped>
body {
  font-family: 'Inter', sans-serif;
}
</style>
