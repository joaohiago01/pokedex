<template>
  <div id="pokemon">
    <div class="card">
        <div class="card-image">
            <figure>
            <img :src="currentImg" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
            <div class="media-content">
                <p class="title is-4">{{name | upper}}</p>
                <p class="subtitle is-6">{{pokeInfo.type | upper}}</p>
            </div>
            </div>
            <div class="content">
                <button @click="changeSprite" class="button is-success is-rounded">Change Sprite</button>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
    created() {
        axios.get(this.url)
            .then(resolve => {
                this.pokeInfo.type = resolve.data.types[0].type.name;
                this.pokeInfo.front = resolve.data.sprites.front_default;
                this.pokeInfo.back = resolve.data.sprites.back_default;
                this.currentImg = this.pokeInfo.front;
            })
    },
    data() {
        return {
            isFront: true,
            currentImg: '',
            pokeInfo: {
                type: '',
                front: '',
                back: ''
            }
        }
    },
    props: {
        name: String,
        url: String
    },
    filters: {
        upper: function(value) {
            var newName = value[0].toUpperCase() + value.slice(1);
            return newName;
        }
    },
    methods: {
        changeSprite() {
            if (this.isFront) {
                this.isFront = false;
                this.currentImg = this.pokeInfo.back;
            } else {
                this.isFront = true;
                this.currentImg = this.pokeInfo.front;
            }
        }
    }
}
</script>

<style>
    #pokemon {
        margin-top: 2%;
    }
</style>