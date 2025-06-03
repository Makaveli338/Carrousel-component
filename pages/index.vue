<template>
    <Transition name="fade">
      <div class="flex min-h-full items-center justify-center p-4 text-center sm:p-0">
        <div
          class="relative transform overflow-hidden rounded-lg bg-white z-20 text-left shadow-xl transition-all sm:my-8 sm:w-full sm:max-w-xl md:max-w-[477px] pb-4"
        >
          <div class="flex justify-end p-2  bg-white relative z-50">
            <button @click="closePopup" class="rounded-full p-1 hover:bg-gray-200">
                <svg width="29" height="30" viewBox="0 0 29 30" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path
                      d="M21.5468 8.02612L7.32019 22.2527M7.32019 8.02612L21.5468 22.2527"
                      stroke="#546512"
                      stroke-width="2.37109"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                    />
                  </svg>
            </button>
          </div>

          <!-- New Popup Content -->
          <div class="bg-white">
            
            <Transition name="fade" mode="out-in">
              <div :key="currentSlide" class="space-y-5 w-full">
                <!-- Image -->
                <div class="relative">
                    <div
                    class="h-[594px] bg-cover bg-center"
                    :style="{ backgroundImage: `url(${heroSlides[currentSlide].image})` }"
                    ></div>
                    <div class="absolute bottom-0 left-0 right-0 h-24 bg-gradient-to-b from-transparent to-white"></div>
                </div>

                <h1
                  :class="heroSlides[currentSlide].id === 1 && 'max-w-[477px]'"
                  class="text-[#231F20] font-medium text-center px-6 mt-6 text-[22px]"
                >
                  {{ heroSlides[currentSlide].title }}
                </h1>
                <div class="text-[#231F20] font-medium text-lg text-center">
                  <p v-for="(desc, index) in heroSlides[currentSlide].description" :key="index">
                    {{ desc }}
                  </p>
                </div>

                <div
                  v-if="heroSlides[currentSlide].id === 1 || heroSlides[currentSlide].id === 4"
                  class="flex gap-4 justify-center"
                >
                  <a @click=" " class="rounded-full bg-[#546512] hover:bg-[#2e3514] py-[13px] px-[32px] text-white text-[21px] font-semibold cursor-pointer"> Purchase promo ticket</a>
                 
                </div>
                
                <div
                  v-if="heroSlides[currentSlide].id === 2 || heroSlides[currentSlide].id === 5"
                  class="flex gap-4 justify-center"
                >
                  <a @click=" " class="rounded-full bg-[#546512] hover:bg-[#2e3514] py-[13px] px-[32px] text-white text-[21px] font-semibold cursor-pointer"> Purchase  ticket</a>
                 
                </div>
              </div>
            </Transition>
          </div>
          <!-- End New Popup Content -->
        </div>
      </div>
    </Transition>

  </template>
  
  <script setup>
  import { ref, onMounted, onUnmounted } from 'vue';
import {
  Dialog,
  DialogPanel,
  Menu,
  MenuButton,
  MenuItem,
  MenuItems,
  Switch,
  TransitionChild,
  TransitionRoot,
  Popover
} from '@headlessui/vue';
  
  const heroSlides = ref([
    {
      id: 1,
      title: 'Enjoy discounted prices for school students.',
      description: [
        'between 1st June - 31st July 2025',
      ],
      image: '/School-trip.png'
    },
    {
      id: 2,
      title: 'Enjoy discounted prices for school students.',
      description: [
        'between 1st June - 31st July 2025'
      ],
      image: '/School-trip.png'
    }
  ]);
  
  const currentSlide = ref(0);
  const slideInterval = ref(null);
  
  const nextSlide = () => {
    currentSlide.value = (currentSlide.value + 1) % heroSlides.value.length;
  };
  
  const prevSlide = () => {
    currentSlide.value =
      currentSlide.value === 0 ? heroSlides.value.length - 1 : currentSlide.value - 1;
  };
  
  onMounted(() => {
    slideInterval.value = setInterval(nextSlide, 8000);
  });
  
  onUnmounted(() => {
    if (slideInterval.value) clearInterval(slideInterval.value);
  });
  </script>