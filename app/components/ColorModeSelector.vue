<template>
    <!-- <ClientOnly v-if="!colorMode?.forced"> -->
        <div class="flex gap-2 items-center">
            <!-- <div class="text-neutral-500 text-xs" v-if="showNextModelLabel">Change to {{ nextMode }}</div> -->
            <button
            class="hover:bg-neutral-200 dark:hover:bg-neutral-600 px-2 py-1 text-neutral-500" 
            @click="toggleMode" @mouseenter="showNextModelLabel = true" @mouseleave="showNextModelLabel = false">
            {{ nextModeIcon }}</button>

            <!-- <Icon name="line-md:moon-filled-alt-to-sunny-filled-loop-transition" style="color: white" /> -->
        </div>
    <!-- </ClientOnly> -->
</template>

<script setup>

const showNextModelLabel = ref(false)
const colorMode = useColorMode()

const modes =[
    'system',
    'light',
    'dark',
]

const nextModeIcons = {
    system: <UIcon name='lucide:sun-medium' size={5}/>,
    light: <UIcon name='lucide:sun-medium' size={5}/>,
    dark: <UIcon name='lucide:moon' size={5}/>,
}

const nextMode = computed(() => {
    const currentModeIndex = modes.indexOf(colorMode.preference)
    let nextModeIndex = null
    if (currentModeIndex + 1 === modes.length) nextModeIndex = 0
    else nextModeIndex = currentModeIndex + 1

    return modes[nextModeIndex]
})

const nextModeIcon = computed(() => {
    return nextModeIcons[nextMode.value]
})

const toggleMode = () => colorMode.preference = nextMode.value
</script>