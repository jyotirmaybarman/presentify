<template>
    <div class="flex justify-between h-full">
        <div class="w-[500px] h-full border p-4">
            <ContextMenuRoot>
                <ContextMenuTrigger>

                    <p class="text-center py-4">Slides</p>

                    <div class="drag-container flex justify-center flex-col items-center">

                        <draggable 
                            v-model="slides" 
                            group="people"
                            class="flex flex-col gap-4"
                            item-key="id"
                            @end="onDragEnd"
                            @start="onDragStart"
                        >
                            <template #item="{element:slide, index}">
                                <div>
                                    <Slide class="draggable border relative"
                                        @click="selected = index"
                                        :class="{
                                            'bg-gray-100 border-blue-500': selected == index,
                                        }"
                                        @after="addSlide('after', index)"
                                        @before="addSlide('before', index)" 
                                        @delete="deleteSlide(index)" 
                                        :slide="slide.content" 
                                    />

                                </div>
                            </template>
                        </draggable>


                    </div>

                    
                </ContextMenuTrigger>

                <ContextMenuPortal>
                    <ContextMenuContent class="border w-[300px] p-2 text-sm bg-white">
                        <ContextMenuItem @select="addSlide()" value="New Tab"
                            class="flex justify-between items-center hover:bg-gray-100 px-2 py-1 cursor-pointer outline-none">
                            <span>Add Slide</span>
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
                                stroke="currentColor" class="w-4 h-4">
                                <path stroke-linecap="round" stroke-linejoin="round" d="M12 6v12m6-6H6" />
                            </svg>
                        </ContextMenuItem>

                        <!-- <ContextMenuSeparator class="h-[1px] bg-gray-300 m-[5px]" /> -->

                        <!-- <ContextMenuSub>
                            <ContextMenuSubTrigger value="New Tab" class="flex relative  justify-between items-start hover:bg-gray-100 px-2 py-1 cursor-pointer">
                                <span>New Tab</span>
                                <div class="">
                                    >
                                </div>
                            </ContextMenuSubTrigger>
                            <ContextMenuPortal>
                              <ContextMenuSubContent class="bg-white border p-2 flex flex-col gap-1 w-[150px]  text-sm " :side-offset="2" :align-offset="-5" >
                                <ContextMenuItem @select="handleSelect" value="New Tab" class="flex justify-between items-start hover:bg-gray-100 px-2 py-1 cursor-pointer">
                                    <span>New Tab</span>
                                    <div class="">
                                        ⌘+T
                                    </div>
                                </ContextMenuItem>
                                
                                <ContextMenuItem value="New Tab" class="flex justify-between items-start hover:bg-gray-100 px-2 py-1 cursor-pointer">
                                    <span>New Tab</span>
                                    <div class="">
                                        ⌘+T
                                    </div>
                                </ContextMenuItem>
                                <ContextMenuItem value="New Tab" class="flex justify-between items-start hover:bg-gray-100 px-2 py-1 cursor-pointer">
                                    <span>New Tab</span>
                                    <div class="">
                                        ⌘+T
                                    </div>
                                </ContextMenuItem>
                              </ContextMenuSubContent>
                            </ContextMenuPortal>
                        </ContextMenuSub> -->
                    </ContextMenuContent>
                </ContextMenuPortal>
            </ContextMenuRoot>
        </div>

        <div class="border w-full p-3 h-full">
            sdfsdf
        </div>

    </div>
</template>

<script setup lang="ts">
import draggable from 'vuedraggable'
import {
    ContextMenuRoot,
    ContextMenuContent,
    // ContextMenuCheckboxItem,
    // ContextMenuGroup,
    ContextMenuItem,
    // ContextMenuItemIndicator,
    // ContextMenuLabel,
    ContextMenuPortal,
    // ContextMenuRadioGroup,
    // ContextMenuRadioItem,
    // ContextMenuSeparator,
    // ContextMenuSub,
    // ContextMenuSubContent,
    // ContextMenuSubTrigger,
    ContextMenuTrigger,
} from 'radix-vue'
import { ref } from 'vue';
import Slide from '@/components/Slide.vue';

// props & emitsarea-down

// variables
const slides = ref([
    {
        id: 1,
        content: "slide 1"
    },
    {
        id: 2,
        content: "slide 2"
    },
    {
        id: 3,
        content: "slide 3"
    },
])
const selected = ref<number|null>(null)

// computed & watchers

// functions

function addSlide(position: "bottom" | "after" | "before" = "bottom", index: number = -1) {
    if (position == 'after') {
        console.log(position);
        slides.value.splice(index + 1, 0, { content: "slide " + (slides.value.length + 1), id: slides.value.length + 1 });

    }

    if (position == 'before') {
        console.log(position);
        slides.value.splice(index, 0, { content: "slide " + (slides.value.length + 1), id: slides.value.length + 1 });

    }

    if (position == 'bottom') {
        slides.value.push({ content: "slide " + (slides.value.length + 1), id: slides.value.length + 1 });
    }
}

function deleteSlide(index: number) {
    slides.value.splice(index, 1)
}

function onDragStart(event:any){
    selected.value = event.oldIndex
}

function onDragEnd(event:any){
    selected.value = event.newIndex
}

// lifecycles


</script>

<style lang="postcss" scoped>
.dragging {
    @apply bg-gray-100
}

.area-top,
.area-down{
    position: relative;
}
.area-top::before{
    position: absolute;
    content: "";
    width: 100%;
    margin-bottom: 15px;
    top: -6px;
    left: 0;
    border: 1px solid blue;
}

.area-down::after{
    position: absolute;
    content: "";
    width: 100%;
    margin-bottom: 15px;
    left: 0;
    bottom: -20px;
    border: 1px solid blue;
}
</style>