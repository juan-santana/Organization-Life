<template>
    <header>
        <img src="../assets/original.jpg" />

        <h1>
            <i>{{ items.tituloheader }}</i>
        </h1>
        <div class="audio">
            <audio src="audio.mp3" preload="none" controls></audio>
        </div>
        <hr />
        <h2 class="titulodoc"><i>{{ items.titulodoc }}</i></h2>
    </header>

    <!--Body-->
    <div class="conteiner">

        <div class="columna-izquierda">
            <div class="articulocontenedor">

                <ul class="ullist">
                    <li class="listadoc">
                        <a href="#">Index</a>
                    </li>
                    <li class="listadoc">
                        <a href="#">Reading directory</a>
                    </li>
                    <li class="listadoc">
                        <a href="#">$$$</a>
                    </li>
                    <li class="listadoc">
                        <a href="#">watch list</a>
                    </li>
                </ul>
                <div class="divbacklog">

                    <h2 class="Backlog">
                        <i>{{ items.backlog }}</i>
                    </h2>
                    <ul class="ullist">
                        <li class="listadoc">
                            <a href="#">Academia</a>
                        </li>
                    </ul>
                    <img class="imgarticle" src="../assets/leftimg.png" />
                    <textarea class="texto-backlog" rows="4"
                        cols="50">"The optimist sees opportunity in every difficulty"</textarea>

                </div>
            </div>
        </div>
        <div class="columna-centro">
            <img class="img2" src="../assets/centerimg.jpg" />

            <h2 class="titutlo-daily"><i>{{ items.titulodaily }}</i></h2>

            <ul class="ullist">
                <li class="listadoc">
                    <a href="#">Habit Tracker</a>
                </li>
                <li class="listadoc">
                    <a href="#">Morning Routine</a>
                </li>
                <li class="listadoc">
                    <a href="#">Academia</a>
                </li>
                <li class="listadoc">
                    <a href="#">Academia</a>
                </li>
            </ul>
            
        </div>
        <div class="columna-derecha">
            <h2 class="titutlo-Faith"><i>{{ items.tituloFaith }}</i></h2>

            <ul class="ullist">
                <li class="listadoc">
                    <a href="#">Divine Love</a>
                </li>
                <li class="listadoc">
                    <a href="#">Daily Widsdom-Quran</a>
                </li>
                <li class="listadoc">
                    <a href="#">Daily Wdisdom-Prophet</a>
                </li>
                <li class="listadoc">
                    <a href="#">PrayerLog</a>
                </li>
            </ul>
            <div class="Plans">
                <h2 class="titutlo-Plans"><i>{{ items.titutloPlans }}</i></h2>
                <ul class="ullist">
                        <li class="listadoc">
                            <a href="#">Calendar</a>
                        </li>
                    </ul>
            </div>
            <div class="Playlist">
                <h2 class="titutlo-Playlist"><i>{{ items.titutloPlaylist }}</i></h2>
                <img class="imgplaylist" src="../assets/Playlist.png"/>
            </div>
        </div>

    </div>


</template>

<script>
export default {
    name: "IndexComponent",
    data() {
        return {
            items: {
                                tituloheader: "- LIFE ORGANIZATION",
                titulodoc: '- Documentation',
                backlog: "- Backlog",
                titulodaily: "- Daily",
                tituloFaith : "- Faith",
                titutloPlans : "- Plans + Work",
                titutloPlaylist: "- Playlist"
            }
        };
        
    },
    
};
</script>
<style>
@import "../assets/css/estilo.css";

</style>
