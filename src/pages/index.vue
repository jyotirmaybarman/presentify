<template>
    <div class="flex justify-between h-full">
        <div class="w-[500px] h-full border p-4">
            <ContextMenuRoot>
                <ContextMenuTrigger>

                    <p class="text-center py-4">Slides</p>

                    <div class="drag-container flex justify-center flex-col items-center gap-4"
                        @dragover.prevent="onDragOver" @dragenter.prevent>

                        <Slide class="draggable relative" :class="dragging == index ? 'dragging' : ''"
                            v-for="(slide, index) in slides" :key="index" @after="addSlide('after', index)"
                            @before="addSlide('before', index)" @delete="deleteSlide(index)" :slide="slide" draggable="true"
                            @dragstart="startDrag($event, index)" @dragend="endDrag($event, index)" />

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

// props & emits

// variables
const slides = ref<number[]>([1, 2, 3])
const dragging = ref<number>(-1)

// computed & watchers

// functions
// function handleSelect(e: Event){
//     console.log(e);

// }

function addSlide(position: "bottom" | "after" | "before" = "bottom", index: number = -1) {
    console.log(index);


    if (position == 'after') {
        console.log(position);
        slides.value.splice(index + 1, 0, slides.value.length + 1);

    }

    if (position == 'before') {
        console.log(position);
        slides.value.splice(index, 0, slides.value.length + 1);

    }

    if (position == 'bottom') {
        slides.value.push(slides.value.length + 1);
    }


}

function deleteSlide(index: number) {
    slides.value.splice(index, 1)
}

function startDrag(event: DragEvent, index: number) {
    dragging.value = index


    if (event.dataTransfer) {
        event.dataTransfer.dropEffect = "move";
        event.dataTransfer.effectAllowed = "move"
        event.dataTransfer.setData('index', index.toString());
    }


}

function endDrag(event: DragEvent, index: number) {
    dragging.value = -1

    console.log(event);
    console.log(index);

}

// function onDrop(event: DragEvent) {
//     if (event.dataTransfer) {
//         // const idx = event.dataTransfer.getData('index')
//         // const item = slides.value.find((_, index) => index.toString() == idx)

//     }
// }

function onDragOver(event: DragEvent) {
    const afterElement = getDragAfterElement(event.clientY)
    const draggable = document.querySelector('.dragging')
    const container = document.querySelector('.drag-container');

    if (container && draggable) {
        if (afterElement == null) {
            container.appendChild(draggable)
        } else {
            container.insertBefore(draggable, afterElement)
        }

    }


}

function getDragAfterElement(y: number) {
    const draggableElements = [...document.querySelectorAll('.draggable:not(.dragging)')]

    const obj = draggableElements.reduce<{ offset: number, element?: HTMLElement }>((closest: any, child) => {
        const box = child.getBoundingClientRect()
        const offset = y - box.top - box.height / 2
        if (offset < 0 && offset > closest.offset) {
            return { offset: offset, element: child }
        } else {
            return closest
        }

    }, { offset: Number.NEGATIVE_INFINITY, element: undefined })

    return obj.element;
}

// lifecycles


</script>

<style lang="postcss" scoped>
.dragging {
    @apply bg-gray-100
}
</style>