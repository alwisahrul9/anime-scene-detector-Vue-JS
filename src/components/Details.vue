<template>
    <div :class="show ? 'w-full flex justify-center' : 'hidden'">
        <ul>
            <li class="text-2xl font-light mb-4 flex flex-col items-center">
                <span class="font-bold text-[19px]">Title : </span>
                <span class="text-center">{{ judul }}</span>
                <span class="text-center font-medium italic">({{ alias }})</span>
            </li>
            <li class="text-2xl font-light mb-4 flex flex-col items-center"><span class="font-bold text-[19px]">Episode : </span>{{ episode }}</li>
            <li class="text-2xl font-light mb-4 flex flex-col items-center"><span class="font-bold text-[19px]">Start From (Minute) : </span>{{ awal }}</li>
            <li class="text-2xl font-light mb-4 flex flex-col items-center"><span class="font-bold text-[19px]">End To (Minute) : </span>{{ akhir }}</li>
            <li class="text-2xl font-light mb-4 flex flex-col items-center">
                <span class="font-bold text-[19px]">Clip :</span>
                <video :src="clip" controls class="aspect-video"></video>
            </li>
            <li class="text-2xl font-light flex flex-col items-center">
                <span class="font-bold text-[19px]">Image :</span>
                <img :src="image" alt="" srcset="">
            </li>
        </ul>
    </div>
</template>
<script>
export default {
    props:{
        judul: String,
        alias: String,
        episode: Number,
        awal: String,
        akhir: String,
        image: String,
        clip: String,
        show: Boolean
    }
}
</script>
<style>
    
</style>