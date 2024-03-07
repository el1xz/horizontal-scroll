<template>
    <header class="pt-[40px] flex justify-between items-center">
        <div class="flex gap-[20px] items-center">
            <nuxt-link to="/">
                <img src="~/assets/img/logo/main-logo.svg" alt="logo">
            </nuxt-link>
            <div class="bg-[#313131] bg-opacity-[40%] w-[1px] h-[60px]" />
            <a href="https://zemlya-rt.ru/" target="_blank">
                <img src="~/assets/img/logo/m2-asg-logo.svg" alt="m2-logo">
            </a>
        </div>
        <nav>
            <ul class="flex gap-[20px] text-[14px] font-medium uppercase">
                <li>
                    <nuxt-link to="/">О посёлке</nuxt-link>
                </li>
                <li>
                    <nuxt-link to="/about">Генплан</nuxt-link>
                </li>
                <li>
                    <nuxt-link to="/contacts">Расположение</nuxt-link>
                </li>
                <li>
                    <nuxt-link to="/contacts">Контакты</nuxt-link>
                </li>
            </ul>
        </nav>
        <div class="flex items-center gap-[10px] text-[14px] font-medium">
            <a class="flex items-center text-[#05807C] bg-white px-[18px] h-[47px] rounded-[10px]" href="tel:+78432024197">
                +7(843) 202-41-97
            </a>
            <button class="flex items-center text-white bg-[#05807C] px-[18px] h-[47px] rounded-[10px] uppercase">
                Написать нам
            </button>
        </div>
    </header>
</template>
<script>
export default {
    
}
</script>