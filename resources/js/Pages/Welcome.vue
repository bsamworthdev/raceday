<template>
    <div class="relative flex items-end justify-center min-h-screen bg-blue-amstrad  sm:items-end sm:pt-0">
        <div class="max-w-6xl mx-auto sm:px-6 lg:px-8 mb-8">

            <div class="mt-8 text-m text-center p-2 pr-6 pl-6 border-8 border-red-600 text-blue-amstrad bg-lightblue-amstrad overflow-hidden shadow">
                <p class="text-xl tracking-widest">CASCADE 1985</p>
                <p class="text-xl tracking-widest">DAY AT THE RACES</p>
                <p class="mt-3">Can you pick the right horses and place the right bets</p>
                <SecondaryButton @click="start" class="mt-6 text-2xl">
                    Press Any Key
                </SecondaryButton>
            </div>
        </div>
    </div>
</template>

<style scoped>
    div {
        font-family: 'Amstrad CPC464', Arial, Helvetica, sans-serif; 
    }
    .bg-gray-100 {
        background-color: #f7fafc;
        background-color: rgba(247, 250, 252, var(--tw-bg-opacity));
    }

    .border-gray-200 {
        border-color: #edf2f7;
        border-color: rgba(237, 242, 247, var(--tw-border-opacity));
    }

    .text-gray-400 {
        color: #cbd5e0;
        color: rgba(203, 213, 224, var(--tw-text-opacity));
    }

    .text-gray-500 {
        color: #a0aec0;
        color: rgba(160, 174, 192, var(--tw-text-opacity));
    }

    .text-gray-600 {
        color: #718096;
        color: rgba(113, 128, 150, var(--tw-text-opacity));
    }

    .text-gray-700 {
        color: #4a5568;
        color: rgba(74, 85, 104, var(--tw-text-opacity));
    }

    .text-gray-900 {
        color: #1a202c;
        color: rgba(26, 32, 44, var(--tw-text-opacity));
    }

    @media (prefers-color-scheme: dark) {
        .dark\:bg-gray-800 {
            background-color: #2d3748;
            background-color: rgba(45, 55, 72, var(--tw-bg-opacity));
        }

        .dark\:bg-gray-900 {
            background-color: #1a202c;
            background-color: rgba(26, 32, 44, var(--tw-bg-opacity));
        }

        .dark\:border-gray-700 {
            border-color: #4a5568;
            border-color: rgba(74, 85, 104, var(--tw-border-opacity));
        }

        .dark\:text-white {
            color: #fff;
            color: rgba(255, 255, 255, var(--tw-text-opacity));
        }

        .dark\:text-gray-400 {
            color: #cbd5e0;
            color: rgba(203, 213, 224, var(--tw-text-opacity));
        }
    }
</style>

<script>
    import JetApplicationLogo from '@/Jetstream/ApplicationLogo'
    import SecondaryButton from '@/Jetstream/SecondaryButton'
    export default {
        props: {
            canLogin: Boolean,
            canRegister: Boolean,
            laravelVersion: String,
            phpVersion: String,
        },
        components: {
            JetApplicationLogo,
            SecondaryButton
        },
        methods: {
            start: function(){
                location.href="/dashboard";
            },
        }
    }
</script>
