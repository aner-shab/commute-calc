<template>
    <div class="container" id="commute-calculator">
        <div class="row">
            <div class="col mr-auto ml-auto">
                <h2 class="text-center total-title">
                    How long do you spend on the road?
                </h2>
                <br>
                <label>I work for ...</label>
                <div class="input-group mb-3">
                    <input type="number" min="1" max="7" v-model="days" class="form-control" id="days" aria-describedby="days">
                    <span class="input-group-addon" id="days">days a week</span>
                </div>

                <div class="input-group mb-3">
                    <input type="number" min="1" max="52" v-model="weeks" class="form-control" id="weeks" aria-describedby="weeks">
                    <span class="input-group-addon" id="weeks">weeks in a year</span>
                </div>

                <div class="input-group mb-3">
                    <span class="input-group-addon" id="minutes">My total commute time (both ways) is:</span>
                    <input type="number" min="1" v-model="travel_time" class="form-control" id="minutes" aria-describedby="minutes">
                    <span class="input-group-addon">minutes long</span>
                </div>
            </div>
        </div>

        <transition name="fade">
        <template v-if="weeks > 0 && days > 0 && travel_time > 0">
            <div class="row total">
                <div class="col-md-10 mr-auto ml-auto">
                    <h2 class="text-center total-title">
                        Your yearly commute is:
                    </h2>

                    <br>

                    <ul class="list-group">
                        <li class="list-group-item"><strong>{{ total_minutes }}</strong> minutes</li>
                        <li class="list-group-item" v-if="parseFloat(total_hours) > 0"><strong>{{ total_hours }}</strong> hours</li>
                        <li class="list-group-item" v-if="parseFloat(total_days) > 0"><strong>{{ total_days }}</strong> days</li>
                        <li class="list-group-item" v-if="parseFloat(total_days) > 0"><strong>{{ total_weeks }}</strong> weeks</li>

                        <li class="list-group-item" v-if="parseFloat(total_nights) > 0"><strong>{{ total_nights }}</strong> nights of sleep</li>
                        <li class="list-group-item" v-if="parseFloat(total_seinfeld) > 0"><strong>{{ total_seinfeld }}</strong> episodes of Seinfeld</li>
                        <li class="list-group-item" v-if="parseFloat(total_avengers) > 0"><strong>{{ total_avengers }}</strong> Infinity Wars</li>
                        <li class="list-group-item" v-if="parseFloat(total_scaramuccis) > 0"><strong>{{ total_scaramuccis }}</strong> Mooches</li>
                     </ul>
                </div>
                <div class="col-md-10 mr-auto ml-auto">
                <div class="hint">* A 'Mooch' is a unit of time equal to ten days, derived from the duration Anthony Scaramucci spent as the Trump Administration's communications director.</div>
                </div>
            </div>
        </template>
        </transition>
    </div>
</template>

<script>
    export default {
        name: 'Commute',
        props: {
        },
        data: function() {
            return {
                weeks: null,
                days: null,
                travel_time: null
            }
        },
        computed: {
            minutes: function() {
                let minutes = parseInt(this.travel_time);
                let weeks = parseInt(this.weeks);
                let days = parseInt(this.days);
                let total_time = minutes * days * weeks;
                return total_time;
            },
            hours: function() { return this.minutes / 60; },
            total_minutes: function() { return this.addCommas(this.minutes); },
            total_hours: function() { return this.addCommas(this.minutes / 60); },
            total_days: function() { return this.addCommas(this.hours / 24); },
            total_weeks: function() { return this.addCommas(this.hours / 24 / 7); },
            total_nights: function() { return this.addCommas(this.hours / 7.5); },
            total_seinfeld: function() { return this.addCommas(this.minutes / 23); },
            total_avengers: function() { return this.addCommas(this.minutes / 160); },
            total_scaramuccis: function() { return this.addCommas(this.hours / 24 / 10); }
        },
        methods: {
            addCommas(nStr) {
                nStr = nStr.toFixed(1);
                nStr += '';
                let x = nStr.split('.');
                let x1 = x[0];
                let x2 = x.length > 1 ? '.' + x[1] : '';
                var rgx = /(\d+)(\d{3})/;
                while (rgx.test(x1)) { x1 = x1.replace(rgx, '$1' + ',' + '$2'); }

                return (x1 + x2);
                }
            }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
    body {
        padding: 1rem;
        color: #fbf6ef;
        background-color: #222023;
    }

    .total {
        padding: 1.5rem 2rem;
        color: #222023;
        background-color: #464a4e;
        border-radius: 2rem;
    }
    .total-title{
        color: whitesmoke;
    }
    .hint{
        padding-top: 1.5rem;
        color: whitesmoke;
        opacity: 0.5;
        font-size: 0.7rem;
    }
    .fade-enter-active, .fade-leave-active {
        transition: opacity .5s;
    }
    .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
        opacity: 0;
    }
</style>
