<template>
    <v-app>
        <v-content>
            <Content></Content>
        </v-content>
    </v-app>
</template>

<script>
    import Content from './components/Content';

    export default {
        name: 'App',

        components: {
            Content,
        },

        data: () => ({

        }),
    };

</script>
