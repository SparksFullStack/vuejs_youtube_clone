<template>
    <div class='container'>  
        <SearchBar @termChange="onTermChange"></SearchBar>
        <div class='row'>
            <VideoDetail :video="selectedVideo" />
            <VideoList :videos="videos" @videoSelect='onVideoSelect'></VideoList>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';

const API_KEY = 'AIzaSyBeMpoEm3DZR9vMuQVuA7hiImVyn4MG3cs';

export default{
    name: 'App',
    components: {
        SearchBar,
        VideoList,
        VideoDetail,
    },
    data(){
        return {
            videos: [],
            selectedVideo: null,
        }
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
            .then(res => this.videos = res.data.items);
        },
        onVideoSelect(video){
            this.selectedVideo = video;
        },
    },
}
</script>