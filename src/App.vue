<template>
    <div>  
        <SearchBar @termChange="onTermChange"></SearchBar>
    </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
const API_KEY = 'AIzaSyBeMpoEm3DZR9vMuQVuA7hiImVyn4MG3cs';

export default{
    name: 'App',
    components: {
        SearchBar,
    },
    methods: {
        onTermChange(searchTerm) {
            axios.get('https://www.googleapis.com/youtube/v3/search', {
                params: {
                    key: API_KEY,
                    type: 'video',
                    part: 'snippet',
                    q: searchTerm,
                }
            })
            .then(res => console.log(res));
        },
    }
}
</script>

