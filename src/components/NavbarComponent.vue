<script setup>
import { useDark, useToggle } from "@vueuse/core";
import { Toggle } from "@/components/ui/toggle";

const isDark = useDark();
const toggleDark = useToggle(isDark);
</script>

<template>
  <nav class="bg-white border-gray-200 dark:bg-gray-900 dark:border-gray-700">
    <div
      class="flex flex-wrap items-center justify-between max-w-screen-xl p-4 mx-auto"
    >
      <a href="#" class="flex items-center space-x-3 rtl:space-x-reverse">
        <img
          width="64"
          height="64"
          src="https://img.icons8.com/nolan/64/laravel.png"
          alt="laravel"
        />
        <span
          class="self-center text-2xl font-semibold whitespace-nowrap dark:text-white"
          >Todo</span
        >
        <img
          width="63"
          height="63"
          src="https://img.icons8.com/external-tal-revivo-green-tal-revivo/36/external-vuejs-an-open-source-javascript-framework-for-building-user-interfaces-and-single-page-applications-logo-green-tal-revivo.png"
          alt="external-vuejs-an-open-source-javascript-framework-for-building-user-interfaces-and-single-page-applications-logo-green-tal-revivo"
        />
        <span
          class="self-center text-2xl font-semibold whitespace-nowrap dark:text-white"
          >Task</span
        >
        <img width="63" height="63" src="https://code.benco.io/icon-collection/other/aml-auto-ml.svg" />
      </a>
      <button
        data-collapse-toggle="navbar-dropdown"
        type="button"
        class="inline-flex items-center justify-center w-10 h-10 p-2 text-sm text-gray-500 rounded-lg md:hidden hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-gray-200 dark:text-gray-400 dark:hover:bg-gray-700 dark:focus:ring-gray-600"
        aria-controls="navbar-dropdown"
        aria-expanded="false"
      >
        <span class="sr-only">Open main menu</span>

      </button>

      <div class="hidden w-full md:block md:w-auto" id="navbar-dropdown">
        <ul
          class="flex flex-col p-4 mt-4 font-medium border border-gray-100 rounded-lg md:p-0 bg-gray-50 md:space-x-8 rtl:space-x-reverse md:flex-row md:mt-0 md:border-0 md:bg-white dark:bg-gray-800 md:dark:bg-gray-900 dark:border-gray-700"
        >
          <li>
            <a
              href="#"
              class="block px-3 py-2 text-white bg-blue-700 rounded md:bg-transparent md:text-blue-700 md:p-0 md:dark:text-blue-500 dark:bg-blue-600 md:dark:bg-transparent"
              aria-current="page"
              >Home</a
            >
          </li>
          <li>
            <!-- <button
              id="dropdownNavbarLink"
              data-dropdown-toggle="dropdownNavbar"
              class="flex items-center justify-between w-full px-3 py-2 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0 md:w-auto dark:text-white md:dark:hover:text-blue-500 dark:focus:text-white dark:border-gray-700 dark:hover:bg-gray-700 md:dark:hover:bg-transparent"
            >
              Dropdown
              <svg
                class="w-2.5 h-2.5 ms-2.5"
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 10 6"
              >
                <path
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="m1 1 4 4 4-4"
                />
              </svg>
            </button> -->
            <!-- Dropdown menu -->
            <div
              id="dropdownNavbar"
              class="z-10 hidden font-normal bg-white divide-y divide-gray-100 rounded-lg shadow w-44 dark:bg-gray-700 dark:divide-gray-600"
            >
              <ul
                class="py-2 text-sm text-gray-700 dark:text-gray-400"
                aria-labelledby="dropdownLargeButton"
              >
                <li>
                  <a
                    href="#"
                    class="block px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white"
                    >Dashboard</a
                  >
                </li>
                <li>
                  <a
                    href="#"
                    class="block px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white"
                    >Settings</a
                  >
                </li>
                <li>
                  <a
                    href="#"
                    class="block px-4 py-2 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white"
                    >Earnings</a
                  >
                </li>
              </ul>
              <div class="py-1">
                <a
                  href="#"
                  class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:hover:bg-gray-600 dark:text-gray-200 dark:hover:text-white"
                  >Sign out</a
                >
              </div>
            </div>
          </li>
          <li>
            <a
              href="#"
              class="block px-3 py-2 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent"
              >Services</a
            >
          </li>
          <li>
            <a
              href="#"
              class="block px-3 py-2 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent"
              >Pricing</a
            >
          </li>
          <li>
            <a
              href="#"
              class="block px-3 py-2 text-gray-900 rounded hover:bg-gray-100 md:hover:bg-transparent md:border-0 md:hover:text-blue-700 md:p-0 dark:text-white md:dark:hover:text-blue-500 dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent"
              >Contact</a
            >
          </li>
          <li>
            <Toggle aria-label="Toggle bold">
              <button @click="toggleDark()">
                <img
                  width="24"
                  height="24"
                  src="https://img.icons8.com/external-kiranshastry-gradient-kiranshastry/64/external-torch-interface-kiranshastry-gradient-kiranshastry.png"
                  alt="external-torch-interface-kiranshastry-gradient-kiranshastry"
                />
              </button>
            </Toggle>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>
