<template>
    <div>
        <ContextMenuRoot>
            <ContextMenuTrigger>
                <div class="border rounded w-[200px] h-[100px] flex items-center justify-center focus:border-blue-500">
                    <span class="select-none">{{ props.slide }}</span>
                </div>
            </ContextMenuTrigger>
    
            <ContextMenuPortal>
                <ContextMenuContent class="border w-[200px] p-2 text-sm bg-white">
                    <ContextMenuItem @select="emits('before')" value="add slide before" class="flex justify-between items-center hover:bg-gray-100 px-2 py-1 cursor-pointer outline-none">
                        <span>Add Slide Before</span>
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-4 h-4">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M9 9l6-6m0 0l6 6m-6-6v12a6 6 0 01-12 0v-3" />
                        </svg>                      
                    </ContextMenuItem>
                    <ContextMenuItem @select="emits('after')" value="add slide after" class="flex justify-between items-center hover:bg-gray-100 px-2 py-1 cursor-pointer outline-none">
                        <span>Add Slide After</span>
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-4 h-4 rotate-180">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M9 9l6-6m0 0l6 6m-6-6v12a6 6 0 01-12 0v-3" />
                        </svg>                      
                    </ContextMenuItem>
                    <ContextMenuItem @select="emits('delete')" value="delete slide" class="flex justify-between items-center hover:bg-gray-100 px-2 py-1 cursor-pointer outline-none">
                        <span>Delete Slide</span>
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-4 h-4">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M14.74 9l-.346 9m-4.788 0L9.26 9m9.968-3.21c.342.052.682.107 1.022.166m-1.022-.165L18.16 19.673a2.25 2.25 0 01-2.244 2.077H8.084a2.25 2.25 0 01-2.244-2.077L4.772 5.79m14.456 0a48.108 48.108 0 00-3.478-.397m-12 .562c.34-.059.68-.114 1.022-.165m0 0a48.11 48.11 0 013.478-.397m7.5 0v-.916c0-1.18-.91-2.164-2.09-2.201a51.964 51.964 0 00-3.32 0c-1.18.037-2.09 1.022-2.09 2.201v.916m7.5 0a48.667 48.667 0 00-7.5 0" />
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

// props & emits
const emits = defineEmits<{
    after: [],
    before:[],
    delete: [],
    // dragstart: [],
}>();

const props = defineProps<{
    slide: any
}>()


// variables

// computed & watchers

// functions

// lifecycles


</script>

<style lang="postcss" scoped>

</style>